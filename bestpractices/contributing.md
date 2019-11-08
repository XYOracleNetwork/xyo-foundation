# Contributing to an XYO Foundation Project

If you'd like to contribute to an XYO Project as a developer or just run the project, please adhere to these guidelines.

## Working with the repository

### Fork, do not clone

First, fork the repository. From here you are free to create your own branch from the `develop` branch of your forked repo. 

After forking the repo:

```sh
git clone <Your forked repo link>
```

Then check out the develop branch

```sh
git checkout develop
```

Create your own branch

```sh
git checkout -b <your-branch-name>
```

If you are able to specify the type of contribution you are making to the project, you can name your branch as such:

- Feature: `feature/<your-branch-name>`

- Fix: `fix/<your-branch-name>`

- Documentation: `docs/<your-branch-name>`

So your branch check out would look like this: 

```sh
git checkout -b feature/<your-branch-name>
```

Using this naming convention helps the dev team and community understand what your code means to address.

### Pushing your changes

Once you are ready to push your changes, you will start by pushing your code to your new branch. You can either commit one time, or you can commit regularly, we recommend the latter. Be sure to stick to the commit standard as described below. 

To add all of your code

```sh
git add .
```

Create a commit message, make sure that it is meaningful, and in the present tense

```sh
git commit -m "create a new schema"
```

You can also use a prefix for context, which is also useful in creating and maintaining a changelog

```sh
git commit -m "feat: create a new schema"
```

Then push to the branch

```sh
git push origin <your-branch-name>
```

After you have added, committed, and pushed your code to your branch, it is time to go into GitHub and create a pull request. 

When creating the pull request, make sure that you first check to see if it builds on your develop branch. Which means you should compare it to your `develop` branch first. If all checks out, then create another pull request. 

**NOTE** Please check the XYO source `develop` branch for any changes. Technically you should not work in parallel with any other contributors or our dev team, so the changes you bring in should not affect your work. We would advise you to add a remote branch which points to the source. 

```sh
git remote add source <link to source repo>
```

If you have a reference to our source repo **DO NOT** push any code to that, our `develop` branch will reject it. 

Once you have added the source repo, then pull in changes (only if needed)

```sh
git fetch source 

git pull source develop
```

Once you have all of the changes then go ahead and push your branch to your forked repo. 

This new pull request will be compared against our source `develop` branch. This pull request should include a description of what this code addresses, how you approached the problem, and any code affected.

Once this pull request is initiated, a code review will start from our dev team. This code review may be specific, or it may be a general approval which would then be merged. 

As with any contributions of code, there are additional standards you should apply, these are described in our [Developer Guide](developer-guide.md).

Once your code is merged, you have contributed to our open source!