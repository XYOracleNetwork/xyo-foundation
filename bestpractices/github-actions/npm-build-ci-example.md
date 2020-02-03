# Node Build/CI Example

Since we use `yarn`, we maintain all commands with Yarn, so that we do not mix lock files. 


``` yaml
name: CI

on:
  push: 
    branches-ignore: 
      'master'

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v1
    - name: Install
      run: yarn install
    - name: Build
      run: yarn build
    - name: Test
      run: yarn test

```