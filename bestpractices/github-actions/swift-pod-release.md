# Swift Pod Release Example

[Using Cocoapods](https://cocoapods.org/)

The current version of cocoapods requires the user to be on the ready when executing this Github action. Once the user pushes code to the master branch (or decides to use release tags to trigger the action) then the user should be ready to click a link in an email from Cocoapods Trunk in order to validate the session and publish the podspec. 

We typically use a deploy script. Example: 

deploy.sh
```sh
pod trunk register current.user@xyo.network 'Deploy' --description='Deploy Script'
pod lib lint
pod --allow-warnings trunk push sdk-core-swift.podspec
```

If you use the deploy script, you can run it in Github actions

```yaml
name: Release

on: 
  push:
    branches:
      - 'master'

jobs: 
  publish:

    runs-on: macOS-latest 

    steps:
      - uses: actions/checkout@v2
      - name: publish to cocoapod register
        run: cd $GITHUB_WORKSPACE && bash $GITHUB_WORKSPACE/scripts/deploy.sh
```

You also have the option of running the commands in the action directly: 

```yaml
name: Release

on: 
  push:
    branches:
      - 'master'

jobs: 
  publish:

    runs-on: macOS-latest 

    steps:
      - uses: actions/checkout@v2
      - name: publish to cocoapod register
        run: |
          pod trunk register current.user@xyo.network 'Deploy' --description='Deploy Script'
          pod lib lint
          pod --allow-warnings trunk push sdk-core-swift.podspec
          
```