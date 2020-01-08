# Gradle/Maven Build Example

This example includes a `branches-ignore` event configuration type so that if you are also including a release workflow you don't go through the build twice. 

``` yaml
name: Build

on:
  push: 
    branches-ignore: 
      - 'master'

jobs:
  build:

    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - name: pre-build
      run:  chmod +x ./gradlew
    - name: build
      run: ./gradlew clean assemble

```