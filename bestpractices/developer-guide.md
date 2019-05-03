[logo]: https://cdn.xy.company/img/brand/XY_Logo_GitHub.png

![logo]

# DEVELOPER GUIDE
The following is a guide for all procedures, standards, and conduct while working on any developmnent projects at XYO.

While you own your assigned project, you do have decision making autonomy, however you should refer to this guide for key infrastructure so that your app is ready for the high standards here at XYO.

**IMPORTANT** 

This is a living guide for the overall standards that are vital for XYO products to maintain the highest level of quality. Your project will also need ***a developer guide to dictate best practices for contribution.*** Feel free to use this guide to help you form the guide specific to your project. 

## Git Branch Standards

**Make sure that the branch you are on is current and checked out from the most updated remote state**

A key while working in a project is to ensure that you have the **latest code from the other branches**. ***especially those that you have checked out from.*** 

Remember to frequently: 

`git fetch --all`
`git pull <remote name - ususally origin> <branch name>`

We would recommend that you do this before pushing your committed code. 

**NOTE** Related: make sure that you are in communication with your project team, and that you check GitHub for updates to the codebase, especially the branch that you are checked out from. 

### Naming Your Branches

When you are checkout out new branches and naming them, you should follow a solid **git flow** method as outlined below: 
- For **feature branches** `feature/<feature you are working on>`
- For **bug fix branches - hot** `hotfix/<hotfix you are working on>`
- For **bug fix branches** `fix/<fix you are working on>` **NOTE** Only if this bug-fix will not interfere with dev worklflow
- For **release branch** `release/<version number>` **NOTE** Only if your project is working off of a release before merge into master

## Git Flow

**NOTE: Only the Develop and Release Branch can be merged into Master**

In order to ensure that production-ready software is truly ready, we need to maintain a strong git flow. This means that we should only merge our develop or release branch into master - essentially we want to lock the `master`, `release` and `develop` branches. The `develop` branch should be the home for all tested and production ready code that is ready for a final review with included checks before being brought into master, we can also use `release` for production staging. All checks would include CI/CD and code quality. 

For feature branches, you should `git checkout -b feature/<what feature name you are working on>`
**NOTE** Feature branches should always and **only** be checked out from the latest develop branch. 

Bug fixes, documentation updates, and minor styling should be done through a `release` branch which would be checked out from the latest `develop` branch after all feature branches have been merged into the `develop` branch.

The `develop` branch should also be where we conduct full app testing, as opposed to feature specific. To test features, you should make sure that all feature specifc tests pass in the `feature` branch that you are working on.

If you feel you may need to do a `hot-fix` directly to master, please communicate when to do this. **Do Not Take Hot Fixes Lightly**

Here is a diagram of good git flow

![Screenshot](https://wac-cdn.atlassian.com/dam/jcr:a9cea7b7-23c3-41a7-a4e0-affa053d9ea7/04%20(1).svg?cdnVersion=le)

## Folder and File Structure

While we currently do not have a set standard naming convention for Folders and Files, we want to add a brief note on this. Depending on your project and these particular parameters: language, architecture pattern, and/or framework you are developing on, you should follow a folder/file structure that is appropriate to your chosen parameters. Also, important make sure your Folders and Files have standard naming conventions. If you have any questions, consult the product or project lead and/or a senior member of the team for a quick refresher.

## Add Needed Tools

In order for your project to fit in smoothly with the XY suite of products, it's important to add the right linters, CI/CD modules, and other needed software before your first merge into `master`.

All projects absolutely must have 
- [Code Climate](https://codeclimate.com/)
   - [Click here for a guide to set up Code Climate in the project](https://docs.codeclimate.com/docs/configuring-test-coverage)
- [Travis CI](https://travis-ci.com/)
  - [Click here for a guide to set up Travis in the project](https://docs.travis-ci.com/user/tutorial/)
- License (whether .md or .txt) - ***for open source projects***

**NOTE** This license will typically be an MIT license, but consult our product manager to confirm
- Linter configuration
- [Semantic Versioning](https://semver.org/)
- A `.gitignore` file
- A `README.md` file - [check out this guide on how to create a solid readme](https://gist.github.com/pllearns/79b3ab198490c5019b9a664fb9a2dc8b)

**NOTE** If you need any help with documentation, we have a technical writer on staff to help with Readmes, Getting Started Guides, Reference Documentation, and any additional end user instructions.

Here is a list of what you need to add per specific language/framework:

### Kotlin
- [JitPack](https://jitpack.io/)
- [Build Tools](https://kotlinlang.org/docs/tutorials/build-tools.html) **NOTE** Use `Gradle`

### Swift
- [Danger](https://danger.systems/swift/)
- [SwiftLint](https://github.com/realm/SwiftLint)
- [CocoaPods](https://cocoapods.org/)
- [Fastlane](https://fastlane.tools/)

**NOTE** For more info on iOS and MacOS Standards, consult the XY Company Wiki -> Departments -> Standards -> iOS & MacOS

### Node
- [yarn package manager](https://yarnpkg.com/en/)
- [eslint](https://eslint.org/)
- [tslint](https://palantir.github.io/tslint/)
- [typescript](https://www.typescriptlang.org/)

**NOTE** For our node libraries, our preferred language is [TypeScript](https://www.typescriptlang.org/)
To check out TypeScript in action - [you can play with the code here](https://www.typescriptlang.org/play/index.html)

### React
- [yarn package manager](https://yarnpkg.com/en/)
- [create-react-app](https://github.com/facebook/create-react-app) - which you can eject from 
- [eslint](https://eslint.org/) config set to `react-app`

**You may be asked to use TypeScript in your project**
- [tslint](https://palantir.github.io/tslint/)
- [typescript](https://www.typescriptlang.org/)
- Use `@storybook` dependencies 
- Use `@type` dependencies

### C
- [Clang](https://clang.llvm.org/)
- [CMake](https://cmake.org/)

**NOTE**

**These standards may change, so good practice is to have a brief check in with a product lead or an owner of a clean, fully functional project in your chosen language and/or framework before starting your project**

## Styling/UI

For styling client facing applications, we use [Bootstrap](https://getbootstrap.com/). Before you decide on other styling libraries or methodologies, you need to consult our Head of Creative, Paola Batiz on your reasoning. In general it would be good practice to consult with her before implementing the XYO style guide.

### A Note on Bootstrap

Here at XYO, we prefer not to use any specific frameworks on top of the already highly performant [Bootstrap library](https://getbootstrap.com/). So use of `reactstrap`, `react-bootstrap` or any other frameworks that sit on top of Bootstrap are not encouraged.

## Naming functions and variables

Code should be as easy to understand as possible - especially when onboarding a new team member, or getting someone on the team familiar with a codebase they have not been exposed to. Besides great documentation and a equally great walkthrough, sound naming conventions for functions and variables can help someone get familiar with your codebase.

Here are a few resources in how to name functions and variables
- [The Art of Naming Variables](https://hackernoon.com/the-art-of-naming-variables-52f44de00aad)
- [Meaningful names and functions](https://medium.com/coding-skills/clean-code-101-meaningful-names-and-functions-bf450456d90c)
- [Wikipedia Article on Naming Convention](https://en.wikipedia.org/wiki/Naming_convention_(programming))

**Of course as with any guideline here, please check in with your product lead and any contributors on the project about the best names for functions, variables, and any other property of the program**

## Tell The Story Through Strong Commit Messages

In order for a detailed history that can be explored by other developers on team and can be used to create an accurate and descriptive changelog, we need strong commits. 

To generate changelogs and to keep track of why code is being committed, we require this format for commit messages:

`type(category): description [flags]`

**EXAMPLES**
`"feat: add a modal [breaking]"` **if a breaking change**
`"refactor: simplified component structure"`

Where type can be: 

- `breaking`
- `build`
- `ci`
- `chore`
- `docs`
- `feat`
- `fix`
- `other`
- `perf`
- `refactor`
- `revert`
- `style`
- `test`

**NOTE** Style tag is for code style as opposed to UI/UX style. All of the other types are self-explanatory. If you are not sure if your commit fits any of these, you can use `other` with a strong and specific commit message. 

Besides helping to form the changelog, these type prefixes help keep the development specific, and tells a story to other developers as to what is happening in the branch. If you are in a `feature` branch, you can still add `fix`, `perf`, `refactor`, `chore`, and others as needed. The most important thing is that your commit tells a complete story of the branch from start to finish.

Here is the module that we plan to use for generating changelogs: [generate-changelog](https://www.npmjs.com/package/generate-changelog)

Here is an example of a small changelog that's generated by `generate-changelog`, as you may be able to associate the type designator with a specific heading in the changelog:

#### 2.2.1 (2019-04-01)

##### Chores

*  update dependencies and add changelog generator ([dcb1faea](https://github.com/xycorp/web-developer.xyo.network-react.git/commit/dcb1faea38aaacd346786fbcbdd378cf8dcb3e35))

##### Documentation Changes

*  update to payable demo, inidicate that this is sunsetting ([c275fbab](https://github.com/xycorp/web-developer.xyo.network-react.git/commit/c275fbabe30b7ea2d0504f38c382067be07d9884))
*  introduction to app and matrix guides ([1d34ab95](https://github.com/xycorp/web-developer.xyo.network-react.git/commit/1d34ab959c0ca508089d38b46c1a2555c9fc130b))
*  update for bridge and diviner ([682bb20f](https://github.com/xycorp/web-developer.xyo.network-react.git/commit/682bb20f09772f38de981e2eb857fa25400bbae4))

##### New Features

*  add dynamic product component replace static product table ([dc6d5440](https://github.com/xycorp/web-developer.xyo.network-react.git/commit/dc6d5440f1e9664e65058fde5aa6a811f79f4bcb))

##### Code Style Changes

*  update to guide sidebar ([c53ec1cf](https://github.com/xycorp/web-developer.xyo.network-react.git/commit/c53ec1cf862f49240488bf7477785dfb7841d724))

#### A Note on Making the Changelog Meaningful
This changelog tells us what has changed in the current version. **Important** in order for a version changelog to be meaningful, be sure to label only key commits, if you created a hotfix or a very minor style update it may not need to be included in the changelog. During the pull request review process, you should check in with the product lead on the commit. You could also squash commits to only include the most meaningful commits with the right type tags before merging.

## Editing the Changelog

If the changelog needs to be edited in any way, please notify me with your update. I also check the final version of the changelog before publishing. I will also include minor changes to make the changelog more readable since the generator needs some tweaking.

## Code Reviews

**IMPORTANT**
The ***Project Owner*** is the developer who owns an XYO project on either: Core - SDK - App Layer - UI. If you need any confirmation or clarification on who a project owner is, please consult Justin Fortier, Maryann Cummings, or Phillip Lorenzo.

An important part of the software development cycle are consistent, thorough, and thoughtful code reviews. Code reviews should be requested by the project owner to a peer who understands the languages/frameworks used and after that review an immediate project lead or product lead. The latter is for QA to ensure that thoughtful code reviews are happening on projects.

You should use a pull request to initiate a code review. This is especially important if you are merging a `feature` or `fix` into the `develop` branch. After you open a pull request in GitHub, before you create the request, you should click on the `reviewers` section (next to the settings wheel), here you can identify the dev team member to do the review. You can select multiple reviewers, however, it is suggested that you go through a code review one at a time so that the next reviewer can see the comments from a previous review. 

An important point to code reviews is that you are learning and understanding your software better and implementing sound practices that reduce or eliminate technical debt as well as stay in XYO's high quality standards. Great code is clean, performant, and modular when crafting software at XYO. Keep this in mind even before you submit for a code review. 

**NOTE** Do not look at code reviews as a punitive or judgemental process, this is a quality control process with learning components to make you a better developer!

**Merging a pull request should also never happen until a final review from the product lead checking that all request changes have been implemented and that all CI/CD, Code Climate, and other build steps have passed.** 


# Key Takeaways 

- **Git Discipline**
- **Adding the Required Tools**
- **Strong Commit History are Keys to a Successful Repository**
- **Thoughtful, thorough, and consistent code reviews**