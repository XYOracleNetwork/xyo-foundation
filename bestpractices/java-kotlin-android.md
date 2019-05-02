[logo]: https://cdn.xy.company/img/brand/XY_Logo_GitHub.png

# [![logo]](https://xy.company)

# XYO Best Practices (Java/Kotlin/Android)

## Editor/IDE (IntelliJ/Android Studio)

### Build (Gradle)

All of our builds are handled through [Gradle](https://gradle.org/). 

### Compiler (Java/Kotlin)

### Linter (Gradle?)

## Testing (?)

## Code Quality (CodeClimate/BetterCodeHub/Codeacy/SonarQube)

For XYO, we expect high quality standards in our code. That's why we utilize these tools to maintain that code quality

### CodeClimate

### BetterCodeHub

### Codeacy

### SonarQube

## Dependency Checking (?)

## CI/CD (Travis)

## Publishing (JitPack)

We publish all of our Java based projects using [JitPack](https://jitpack.io/). Simply add it into to the root build.gradle, instructions on this can be [found here](https://jitpack.io/).

## Runtime (Java)

## XYO Tools (sdk-base-java/sdk-base-kotlin/sdk-base-android)

## Logging (Firebase)

## Platforms

> These are all of the platforms that are supported by our Java/Kotlin based architectures

### Android

#### Native

#### Unity

#### Unreal

### OSX

#### JRE

### Linux

#### JRE

### Windows

#### JRE

## Source Control (GitHub)

### Git Branch Standards

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

### Git Flow

**NOTE: Only the Develop and Release Branch can be merged into Master**

In order to ensure that production-ready software is truly ready, we need to maintain a strong git flow. This means that we should only merge our develop or release branch into master - essentially we want to lock the `master`, `release` and `develop` branches. The `develop` branch should be the home for all tested and production ready code that is ready for a final review with included checks before being brought into master, we can also use `release` for production staging. All checks would include CI/CD and code quality. 

For feature branches, you should `git checkout -b feature/<what feature name you are working on>`
**NOTE** Feature branches should always and **only** be checked out from the latest develop branch. 

Bug fixes, documentation updates, and minor styling should be done through a `release` branch which would be checked out from the latest `develop` branch after all feature branches have been merged into the `develop` branch.

The `develop` branch should also be where we conduct full app testing, as opposed to feature specific. To test features, you should make sure that all feature specifc tests pass in the `feature` branch that you are working on.

If you feel you may need to do a `hot-fix` directly to master, please communicate when to do this. **Do Not Take Hot Fixes Lightly**

Here is a diagram of good git flow

![Screenshot](https://wac-cdn.atlassian.com/dam/jcr:a9cea7b7-23c3-41a7-a4e0-affa053d9ea7/04%20(1).svg?cdnVersion=le)

## Licensing

It is important to ensure that any licensing requirements are satisfied if using a third-party library that provides them. If you are unsure, consult with legal.

### Our Licenses

#### MIT

#### LGPL 3.0

#### Custom

### 3rd Party Licenses