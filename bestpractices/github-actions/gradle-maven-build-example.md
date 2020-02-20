# Gradle/Maven Build Example

This example is for a push directly to the `develop` branch. 

This executes a gradle assemble build which triggers an automated `patch` version number bump. Then the action will add the version properties file that has been updated and push one last change to the `develop` branch. This entire action confirms the build passes and that it is ready for a pull request to `master` and eventual upload to bintray and github release. 

``` yaml
name: CI

on:
  push: 
    branches: 
      - 'develop'

jobs:
  build:

    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - name: pre-build
      run:  chmod +x ./gradlew
    - name: build
      run: ./gradlew :xyo-android-library:assemble
    - name: check in local changes
      run: |       
        git status
        git add xyo-android-library/version.properties
    - name: commit file
      run: |
        git config --local user.email "action@github.com"
        git config --local user.name "GitHub Action"
        git commit -m "version bump" -a
    - name: push changes
      uses: ad-m/github-push-action@master
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        branch: 'develop' 
```