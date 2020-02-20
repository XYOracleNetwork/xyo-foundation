# Setting Up Badges for Your Repository

> This is a guide for all possible badges. For your particular project, please go to the [readme guide](readme-guide) for the badges you need to include in your project. Although it is highly recommended that you use the badges mentioned in this guide.

Badges are an important indicator as to code, build, and release quality. These should give the end user an accurate representation as to the state of your code and put them at ease about installing and using your SDK and module with their project. 

## Github Actions

-   To use a Github actions badge, you will need to copy your repo path to the workflows folder and yaml file:
-   Example with a particular branch: 

    `![](https://github.com/XYOracleNetwork/client-xyo-nodejs/workflows/CI/badge.svg?branch=develop)`

    ![](https://github.com/XYOracleNetwork/client-xyo-nodejs/workflows/CI/badge.svg?branch=develop)


    - This badge gets its validation from the name portion of the `ci.yaml` file which is `CI`

-   Example for master build: 

    `![](https://github.com/XYOracleNetwork/client-xyo-nodejs/workflows/CI/badge.svg)`
    
    ![](https://github.com/XYOracleNetwork/client-xyo-nodejs/workflows/CI/badge.svg)


- With Github Actions, you can also document multiple badges for different worfklows, such as release, testing, etc. 

  - Example:  
  
    `![](https://github.com/XYOracleNetwork/sdk-base-android/workflows/Release/badge.svg?=?branch=develop)`

    ![](https://github.com/XYOracleNetwork/sdk-base-android/workflows/CI/badge.svg?branch=develop)


    `![](https://github.com/XYOracleNetwork/sdk-base-android/workflows/Release/badge.svg?branch=master)`

    ![](https://github.com/XYOracleNetwork/sdk-base-android/workflows/Release/badge.svg?branch=master)

This allows a user who is looking at the documentation repo to know the stages that are passing. 

## Better Code Hub

[![BCH compliance](https://bettercodehub.com/edge/badge/XYOracleNetwork/sdk-core-kotlin?branch=master)](https://bettercodehub.com/)


-   Go to **[bettercodehub.com](https://bettercodehub.com/)**

-   Click on the `Sign in with GitHub` button

-   Log in with your `GitHub` account

-   You should now see any organizations you belong to, including your own GitHub

-   Click on the **XYO Logo**

-   You should now be able to search for your project

**If your project does not have a numerical score**

-   Then click on the `play` button to analyze the repository

-   Once the analysis is complete you should see a numerical score

-   You should also see a series of icons that indicate successful or failed checks

**Once you have completed and verified the analysis of your project**

-   Click on the `settings` wheel

-   You should see a compliance badge with your score out of 10

-   There are two methods to get the badge, we want to grab the markdown version

-   Copy the markdown version and paste it in the readme for your repository

## For Codacy, CodeClimate, SonarCloud, and Snyk

> Check in with Phillip Lorenzo or Arie Trouw the current admins for these services. They will decide whether to give you permission to generate the badges, or whether admin would need to generate and place in documentation.

Your project will be complete and to standard once you have placed these badges in your documentation and `README.md` file

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/2fb2eb69c1db455299ffce57b0216aa6)](https://www.codacy.com/app/XYOracleNetwork/sdk-core-kotlin?utm_source=github.com&utm_medium=referral&utm_content=XYOracleNetwork/sdk-core-kotlin&utm_campaign=Badge_Grade) [![Maintainability](https://api.codeclimate.com/v1/badges/af641257b27ecea22a9f/maintainability)](https://codeclimate.com/github/XYOracleNetwork/sdk-core-kotlin/maintainability) [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=XYOracleNetwork_sdk-core-kotlin&metric=alert_status)](https://sonarcloud.io/dashboard?id=XYOracleNetwork_sdk-core-kotlin) [![Known Vulnerabilities](https://snyk.io/test/github/XYOracleNetwork/sdk-core-kotlin/badge.svg?targetFile=build.gradle)](https://snyk.io/test/github/XYOracleNetwork/sdk-core-kotlin?targetFile=build.gradle)


### Using remark for your project's markdown files

Markdown may be taken for granted in a project's readme or getting started guide, but to pass Codacy's guidelines and to have a clean markdown file, it is a good idea to use the `remark` code style linter.

For reference to this linter, [click here](https://github.com/remarkjs/remark-lint)

To use the remark linter cli (which we strongly recommend), install with the global tag 

```sh
npm install -g remark-cli
```

Create an empty `.remarkrc` file, especially if your project is not in `node.js`

`.remarkrc`
```rc
{
  // keep this empty
}
```

Then run the `remark` command either for one file or for an entire project:

```sh
remark [your-file-name].md
```
or for the whole file

```sh
remark . 
```

Once the command is executed you should get feedback indicating no issues: 

```sh
README.md: no issues found
bestpractices/badge-setup.md: no issues found
bestpractices/c-c++.md: no issues found
bestpractices/developer-guide.md: no issues found
bestpractices/java-kotlin-android.md: no issues found
bestpractices/nodejs.md: no issues found
bestpractices/objectivec-swift-ios-osx.md: no issues found
bestpractices/readme-guide.md: no issues found
repositories/applications.md: no issues found
repositories/dapps.md: no issues found
repositories/documentation.md: no issues found
repositories/pipeline.md: no issues found
repositories/sdks.md: no issues found
repositories/tools.md: no issues found
```

You can also run `remark` using the VSCode extension. There are instructions on how to do use this [click here](<https://marketplace.visualstudio.com/items?itemName=mrmlnc.vscode-remark>
)

Once you have taken this step, your repo should be free of any unecessary markdown issues when running through the Codacy check. 

### For Example Badges, check out the [readme guide](readme-guide)
