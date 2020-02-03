# Swift Pod Build Example

Full Example uses

- [Cocoapods](https://cocoapods.org/)
- [Slather](https://github.com/SlatherOrg/slather)
- [xcpretty](https://github.com/xcpretty/xcpretty)

In this workflow example, we are using Slather test coverage for CI along with Code Climate for overall code quality, Codacy for specific quality issues (including security and best practice validation), and xcpretty for formatting in `xcodebuild`. 

Note that we do create a fresh simulator to ensure build and test accuracy.

```yaml
name: Build

on: 
  push: 
    branches-ignore:
      - 'master'

jobs:
  build:
    runs-on: macos-latest
    strategy: 
      matrix:
        destination: ['platform=iOS Simulator,OS=latest,name=iPhone11']

    steps:
    - uses: actions/checkout@v2
    - name: set up pod, slather and xcpretty
      run: |
        gem install cocoapods --pr
        pod repo update
        gem install slather
        gem install xcpretty
    - name: code climate testing
      env:
        CC_TEST_REPORTER_ID: ${{ secrets.CC_TEST_REPORTER_ID }}
      run: |          
        curl -L https://codeclimate.com/downloads/test-reporter/test-reporter-0.6.3-darwin-amd64 > ./cc-test-reporter
        chmod 777 ./cc-test-reporter
        ./cc-test-reporter before-build
    - name: clear and prep
      run: | 
          pod deintegrate
    - name: build
      env: 
        destination: ${{ matrix.destination }}
      run: | 
        xcrun simctl create iPhone11 com.apple.CoreSimulator.SimDeviceType.iPhone-11 com.apple.CoreSimulator.SimRuntime.iOS-13-2
        pod install
        xcodebuild clean test -workspace sdk-core-swift.xcworkspace -scheme sdk-core-swift -destination "${destination}" -UseModernBuildSystem=NO | xcpretty
    - name: after build and analyze
      env:
        CC_TEST_REPORTER_ID: ${{ secrets.CC_TEST_REPORTER_ID }}
        CODACY_PROJECT_TOKEN: ${{ secrets.CODACY_PROJECT_TOKEN }}
      run: |
        slather coverage -x --scheme sdk-core-swift --workspace sdk-core-swift.xcworkspace sdk-core-swift.xcodeproj
        ./cc-test-reporter after-build
```
