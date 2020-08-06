[logo]: https://cdn.xy.company/img/brand/XY_Logo_GitHub.png

![logo]

# DEPLOYMENT GUIDE

The following is a guide for deploying products in the XYO ecosystem.

**IMPORTANT** 

If you are unsure of your build process, or need help in creating your Github Action, please ask a peer or your PM. 

> For guidelines on creating a readme, please [click here](readme-guide.md)

## Github Actions

Before creating your Github Action Workflow folder and `yaml` files to start building, you should consult the Github Actions folder in `bestpractices` for templates. 

Templates included for:

- CI/Build
- Release
- Publishing

Our deployment process is as follows:

- All code that has passed build and review checks must always be pushed to the `release` branch (unless the repository doesn't contain one).
- Once the release branch has been updated and pre-release github actions are complete, then the release branch will be merged into master for final release. 

