# Swift Build Example

[Using swift package manager ](https://github.com/apple/swift-package-manager)

Destination is kept here in case of a need to set a destination for a simulation build. 

This example includes a `branches-ignore` event configuration type so that if you are also including a release workflow you don't go through the build twice. 


``` yaml
name: SDK Build

on:
  push: 
    branches-ignore: 
      - 'master'


jobs:
  build:
    runs-on: macOS-latest
    strategy: 
      matrix:
        destination: ['platform=iOS Simulator,iOS=13.1,name=iPhone11']

    steps:
    - uses: actions/checkout@v2
    - name: Build
      run: |
            swift package init --type library
            swift package generate-xcodeproj
            swift build -v
      env: 
        destination: ${{ matrix.destination }}
```