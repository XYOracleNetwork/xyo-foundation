[logo]: https://cdn.xy.company/img/brand/XY_Logo_GitHub.png

![logo]

# DEPLOYMENT GUIDE

The following is a guide for deploying products in the XYO ecosystem.

**IMPORTANT** 

If you are unsure of your build process, or need help in creating your Travis yaml, please ask a peer or your PM. 

> For guidelines on creating a readme, please [click here](readme-guide.md)

## Travis CI/CD

Before creating your `travis.yml` and start building, you should sign in and go through the Travis UI for information that you will need as you are building. 

-   Go to **[travis-ci.org](https://travis-ci.org)**

-   Click on the `Sign in with GitHub` button 

-   Once you sign in you should see a page with a repository and its build status

-   You should also see a left side navigation with a list of the latest builds  of repositories in `XYOracleNetwork`

**Above the left side navigation, you should see a search bar which has the placeholder text: `Search all repositories`**

-   This is where you can search for all of your repositories where you have already setup a travis build

-   If you have a build for the repository you searched for, you should then be able to click on the status image next to the **GitHub** logo next to the name of the repo

For Badge Setup with Travis, please refer to [badge-setup.md](badge-setup)

When setting up Travis, you should create a branch specifically for the setup, example: `feature/travis-setup`. This will allow you to create a pull request against the `develop` branch and execute a pull-request and branch build.

### Setting up your Travis yaml file

Continuous integration is important for repo integrity, and we need to add Continuous Deployment for versioning (numerical and semantic versioning instructions below example script) and automated deployment on a push to the `master` branch

We require that for the majority of projects `deploy` gets pointed to the `master` branch. If you do need to deploy from a `develop` branch, please check in with the dev team for your project.

Example `travis.yml`

In this example we have the core elements of a travis build script including
- `language`
- `cache`
- `addons`
- `install`
- `script`
- `deploy`

You can also add a `notifications` configuration if you choose to get notifications on slack in addition to your Travis email notifications


```yaml
language: node_js
node_js:

-   "10"
    cache:
      yarn: true
      directories:
    -   node_modules
        addons:
          sonarcloud:
            organization: xyo-network
        install:
-   npm install -g travis-ci-cloudfront-invalidation
-   yarn install
    script:
-   yarn build-release
    notifications:
      slack:
        on_success: always
        on_pull_requests: false
        rooms: 
          \- $SLACK_TOKEN
    deploy:
    -   provider: s3
        access_key_id: $AWS_KEY
        secret_access_key: $AWS_SECRET
        bucket: web-coinapp.co-bootstrap
        region: us-east-1
        skip_cleanup: true
        local-dir: dist/en
        default_text_charset: 'utf-8'
        cache_control: "max-age=60000"
        acl: public_read
        on:
          repo: xylabs/web-coinapp.co-bootstrap
          branch: master
    -   provider: s3
            access_key_id: $AWS_KEY
            secret_access_key: $AWS_SECRET
            bucket: dev.coinapp.co
            region: us-east-1
            skip_cleanup: true
            local-dir: dist/en
            default_text_charset: 'utf-8'
            cache_control: "max-age=0"
            acl: public_read
            on:
              repo: xylabs/web-coinapp.co-bootstrap
              branch: develop
        after_deploy:
    -   travis-ci-cloudfront-invalidation -a $AWS_KEY -s $AWS_SECRET -c $AWS_CLOUDFRONT_DIST_ID -i '/\*' -b $TRAVIS_BRANCH -p $TRAVIS_PULL_REQUEST -o master

```

Once you have configured your `yaml` file, you should do a pull request to the `develop` branch to insure that the code can build. 

Once all `required` tests pass on the `develop` branch, then you can create a pull request against the `master` branch

Once all tests pass, then you are ready to merge your code to the master branch and deploy to production.

For specific `yaml` configurations, please consult either the project lead on your particular project or the CTO.

