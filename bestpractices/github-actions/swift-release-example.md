# Swift Release Example

[Using swift package manager ](https://github.com/apple/swift-package-manager)

Destination is kept here in case of a need to set a destination for a simulation build for any testing as part of the release workflow. 


``` yaml
name: SDK Release

on: 
  push:
    tags:
      - 'v*'

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
            swift build -c release
      env: 
        destination: ${{ matrix.destination }}
```