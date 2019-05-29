# Setting Up Badges for Your Repository

> This is a guide for all possible badges. For your particular project, please go to the [readme guide](readme-guide) for the badges you need to include in your project

## Better Code Hub

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

## Travis CI

-   Go to **[travis-ci.org](https://travis-ci.org)**

-   Click on the `Sign in with GitHub` button 

-   Once you sign in you should see a page with a repository and its build status

-   You should also see a left side navigation with a list of the latest builds  of repositories in `XYOracleNetwork`

**Above the left side navigation, you should see a search bar which has the placeholder text: `Search all repositories`**

-   This is where you can search for all of your repositories where you have already setup a travis build

-   If you have a build for the repository you searched for, you should then be able to click on the status image next to the **GitHub** logo next to the name of the repo

**When you click on the status image, you will see a modal with the following**

-   branch - you can choose the branch you want the badge to represent, we should always select the `master` branch

-   A dropdown select with the starter selection `Image URL`

-   Select `Markdown`

-   Once you select markdown, you can copy the markdown text and paste it to your repository's readme file

## For Codacy, CodeClimate, and SonarCloud

> Check in with Phillip Lorenzo or Arie Trouw the current admins for these services

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
