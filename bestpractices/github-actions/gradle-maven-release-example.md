# Gradle/Maven Release Example

This example executes an install, build for release, and a bintray upload while creating a Github release draft, which can be edited with the current tag and release description. 

Currently for semver consistency, version numbers (inlcuding minor and patch updates) are manual. 

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
      - name: bintray upload
        env: 
          BINTRAY_USER: ${{ secrets.BINTRAY_USER }}
          BINTRAY_KEY: ${{ secrets.BINTRAY_KEY }}
        run: ./gradlew :xyo-android-library:bintrayUpload
      - name: Create Release
        id: create_release
        uses: actions/create-release@v1
        env: 
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with: 
          tag_name: ${{ github.ref }}
          release_name: Release ${{ github.ref }}
          draft: true
          prerelease: false
```