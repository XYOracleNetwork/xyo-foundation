# Node Publish Example - to npmjs

Since we use `yarn`, we maintain all commands with Yarn, so that we do not mix lock files. 

In order for this template to work, you would need to add `NPM_EMAIL` and `NPM_TOKEN` to the secrets in your Github repo. Once you do, you can access via env in the npm setup step. 

``` yaml
name: Publish

on: 
  push: 
    branches: 
      - "master"
  
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v1
        with: 
          node-version: '10.x'
      - run: |
          yarn install 
          yarn build

  publish-npm:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v1
        with: 
          node-version: '10.x'
          registry-url: https://registry.npmjs.org/
          scope: '@xyo-network'
      - run: |
          yarn install 
          yarn build
      - run: |
          echo "//registry.npmjs.org/:_authToken=$NODE_AUTH_TOKEN" > /home/runner/work/_temp/.npmrc
          echo "_auth=$NODE_AUTH_TOKEN" >>  /home/runner/work/_temp/.npmrc
          echo "email=$NPM_EMAIL" >>  /home/runner/work/_temp/.npmrc
          echo "always-auth=true" >>  /home/runner/work/_temp/.npmrc
        env:
            NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
            NPM_EMAIL: ${{ secrets.NPM_EMAIL }}
      - run: npm publish --access public

```