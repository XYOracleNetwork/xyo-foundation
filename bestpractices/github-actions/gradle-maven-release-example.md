# Gradle/Maven Release Example

This example executes an install, build for release, and a bintray upload while creating a Github release draft, which can be edited with the release description. Note that the pull request commit to `master` will populate the description. To minimize editing, the pull request description should be clear. 

We have updated semantic version as manual for `minor` and `major` updates, with automated `patch` bump for a push to the `develop` branch. 

The flow in this case would require that the `develop` branch pass all conditions from other branches before any pull request to `master` is allowed. 

The `master` branch does not increment the patch, that is done by the `develop` branch. The master executes a release assemble with the new patch (and any minor and/or major manual changes) along with an output set for the tag number to be read by the create-release action. 

```yaml
name: Release 

on: 
  push:
    branches:
      - 'master'

jobs:         
  publish:

    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@master
      - uses: actions/setup-java@v1
        with:
          java-version: 1.8
      - name: pre-build
        run: chmod +x gradlew
      - name: install
        run: ./gradlew install
      - name: assemble
        run: ./gradlew :xyo-android-library:assembleRelease
      - name: print version
        run: |
          echo "##[set-output name=version;]$(gradle -q printVersion)"
        id: release_version
      - name: bintray upload
        env: 
          BINTRAY_USER: ${{ secrets.BINTRAY_USER }}
          BINTRAY_KEY: ${{ secrets.BINTRAY_KEY }}
        run: ./gradlew :xyo-android-library:bintrayUpload
      - name: get commit message
        run: |
          echo ::set-env name=commitmsg::$(git log --format=%B -n 1 ${{ github.event.after }})
      - name: show commit message
        run: echo $commitmsg
      - name: Create Release
        id: create_release
        uses: actions/create-release@v1
        env: 
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with: 
          tag_name: ${{ steps.release_version.outputs.version }}
          release_name: Release ${{ env.commitmsg }}
          draft: true
          prerelease: false
```