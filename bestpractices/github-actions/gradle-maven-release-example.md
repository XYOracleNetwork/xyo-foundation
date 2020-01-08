# Gradle/Maven Release Example

This example fires the build and publish event only when a release tag is created. This does not trigger on the master branch. 

```yaml
name: Release 

on: 
  push:
    tags:
      - 'v*'

jobs:  
  publish:

    runs-on: ubuntu-latest

    steps: 
      - uses: actions/checkout@v2
      - uses: actions/setup-java@v1
        with:
          java-version: 1.8
      - name: Permission for gradlew
        run: chmod +x gradlew
      - name: Build
        run: ./gradlew assembleRelease
      - name: Publish
        env: 
          GITHUB_USERNAME: ${{ secrets.USERNAME }}
          GITHUB_TOKEN: ${{ secrets.NEW_TOKEN }}
        run: gradle publish

```