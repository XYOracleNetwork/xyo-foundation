# Node Release Example

Since we use `yarn`, we maintain all commands with Yarn, so that we do not mix lock files. 

``` yaml
name: Release 

on: 
  push:
    tags:
      - 'v*'

jobs: 
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v1
        with:
          node-version: 10.15.0
      - run: yarn install
      - run: yarn build
      - run: yarn test

  publish-gpr:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v1
        with:
          node-version: 10.15.0
          registry-url: <https://npm.pkg.github.com/>
          scope: '@xyoraclenetwork'
      - run: yarn install
      - run: yarn build
      - run: yarn publish
        env:
          NODE_AUTH_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```