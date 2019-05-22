# README GUIDE

The following is a guide to creating a readme for XYO projects.

Please follow this guide from the Logo on down to the credits. To use, you may copy this example below from the raw source. 

> **Company Logo First**

[example logo]: https://cdn.xy.company/img/brand/XY_Logo_GitHub.png

[![example logo]](https://xy.company)

## Status of the repo (build, code quality, chat option)

> Badges should only reflect the master branch, please avoid develop and master branch table.

**For more instruction on setting up badges, please [click here](badge-setup)**

> Your build branch status using Travis CI

[![Build Status](https://travis-ci.com/XYOracleNetwork/sdk-core-nodejs.svg?branch=develop)](https://travis-ci.com/XYOracleNetwork/sdk-core-nodejs)

> Dependency monitoring using david-dm

[![David Badge](https://david-dm.org/xyoraclenetwork/sdk-core-nodejs/status.svg)](https://david-dm.org/xyoraclenetwork/sdk-core-nodejs) [![David Badge](https://david-dm.org/xyoraclenetwork/sdk-core-nodejs/dev-status.svg)](https://david-dm.org/xyoraclenetwork/sdk-core-nodejs)

> Identify and remediate vulnerabilities using DepShield

[![DepShield Badge](https://depshield.sonatype.org/badges/XYOracleNetwork/sdk-core-nodejs/depshield.svg)](https://depshield.github.io)

> Quality of source code and bug detection using SonarCloud 

[![Sonarcloud Status](https://sonarcloud.io/api/project_badges/measure?project=XYOracleNetwork_sdk-core-nodejs&metric=alert_status)](https://sonarcloud.io/dashboard?id=XYOracleNetwork_sdk-core-nodejs) 

> Maintainability and test coverage using Code Climate

[![Maintainability](https://api.codeclimate.com/v1/badges/f3dd4f4d35e1bd9eeabc/maintainability)](https://codeclimate.com/github/XYOracleNetwork/sdk-core-nodejs/maintainability)

> Code review against engineering guidelines using Better Code Hub

[![BCH compliance](https://bettercodehub.com/edge/badge/XYOracleNetwork/sdk-core-nodejs?branch=develop)](https://bettercodehub.com/results/XYOracleNetwork/sdk-core-nodejs)

> Code review and monitoring of code quality over time using Codacy

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/1f31c7fa87694b8eab91a2d71f74b697)](https://www.codacy.com/app/arietrouw/app-xyo-nodejs?utm_source=github.com&utm_medium=referral&utm_content=XYOracleNetwork/app-xyo-nodejs&utm_campaign=Badge_Grade)

> If this repo is published on NPM 

[![NPM](https://nodei.co/npm/@xyo-network/app.png)](https://nodei.co/npm/@xyo-network/app/) 

> If you want to add a gitter chat link

<a href="https://gitter.im/XYOracleNetwork/Dev">
  <img alt="Gitter Chat" src="https://img.shields.io/gitter/room/XYOracleNetwork/Stardust.svg">
</a>

> If you are working on a dApp and implementing Web3 use Commitizen

<a href="http://commitizen.github.io/cz-cli/">
  <img alt="Commitizen friendly" src="https://img.shields.io/badge/web3-friendly-brightgreen.svg">
</a>

> Breakdown of badges based on language and/or platform

**Node.JS/Bootstrap/React**

-   Better Code Hub
-   SonarCloud (implementing SonarQube)
-   Code Climate
-   Codacy
-   DepSheild
-   David-dm
-   Travis-CI 
-   Nodei.com (NPM)

**Kotlin/Android/Java**

-   Better Code Hub
-   SonarCloud (implementing SonarQube)
-   Code Climate
-   Codacy
-   DepSheild
-   Travis-CI 
-   JitPack

**iOS/MacOS/Swift**

-   Better Code Hub
-   SonarCloud (implementing SonarQube)
-   Code Climate
-   Codacy
-   Travis-CI 
-   CocoaPod

**C/Firmware**

-   Better Code Hub
-   SonarCloud (implementing SonarQube)
-   Code Climate
-   Codacy
-   Travis-CI

> A Table of Contents **required**

## Table of Contents

> Stay consistent with Title and Installation/Usage/License/Credits

Table of Contents

-   [Sections](#sections)
-   [Title](#Simple-Consensus-Smart-Contract-Dapp-Library)
-   [Short Description](#short-description)
-   [Long Description](#long-description)
-   [Security](#security)
-   [Install](#install)
-   [Usage](#usage)
-   [Diviner Staking Walkthrough](#walkthrough)
-   [API](#api)
-   [Maintainers](#maintainers)
-   [Contributing](#contributing)
-   [License](#license)
-   [Credits](#credits)

## The Layout

> Sections - this is the primary header for the remainder of the readme - _required_

## Sections

> Title - **Required** Should be written with one hash (#) before the title

### Simple Consensus Smart Contract Dapp Library _(dapp-scsc-solidity)_

[![Build Status](https://travis-ci.com/XYOracleNetwork/dapp-scsc-solidity.svg?branch=develop)](https://travis-ci.com/XYOracleNetwork/dapp-scsc-solidity)[![David Badge](https://david-dm.org/xyoraclenetwork/dapp-scsc-solidity/status.svg)](https://david-dm.org/xyoraclenetwork/dapp-scsc-solidity) [![David Badge](https://david-dm.org/xyoraclenetwork/dapp-scsc-solidity/dev-status.svg)](https://david-dm.org/xyoraclenetwork/dapp-scsc-solidity) [![BCH compliance](https://bettercodehub.com/edge/badge/XYOracleNetwork/dapp-scsc-solidity?branch=master&token=02d25ea6874c74a77ffefc6157e0253305509033)](https://bettercodehub.com/results/XYOracleNetwork/dapp-scsc-solidity) <a href="http://commitizen.github.io/cz-cli/">
  <img alt="Commitizen friendly" src="https://img.shields.io/badge/web3-friendly-brightgreen.svg">
</a>

> Short Description - A one sentence description of the project - _required_

## Short Description

A Simple Consensus Smart Contract library for all nodes in XYO

> Long Description - A longer description of the project for more detail - _optional but recommended_

## Long Description

This package has been built to streamline the dApp build process for anyone ready to integrate XYO into their project. Especially crucial in this library are the `XyGovernance` and `XyStakingConsensus` contracts. The `XyPayOnDelivery` contract is a solid example of the execution of all nodes in XYO, and is used with our [Payable on Delivery Demo](https://developers.xyo.network/docs/en/payable-demo/). The package contains contracts that are upgradeable (with the exception of the Parameterizer) so that you can fix security vulnerabilities and introduce new features without migrating all of the data unecessarily. 

> **Suggestions** - Light or Stern suggestions as to what the developer should know prior to using or contributing to the project

## You should be familiar with

-   Solidity
-   Web3
-   Truffle
-   Ganache

> **Install** - Installation instructions _if necessary_. This can be called **Set Up** if there are no installation steps

## Install

> **Requirements: Make sure that the developer has the resources needed**
>
> -   In the command line go ahead and install using `npm`

```bash
npx zos link dapp-scsc-solidity
```

> Add any instrucions after installation here

-   Run

> How to use the application or SDK

### Usage

> Requirements before use

**Requirements:**

-   Watch this video on staking a node in XYO
-   Check out [dApper](https://github.com/XYOracleNetwork/tool-dapper-react)
    -   dApper allows you to interact with the smart contracts from the scsc library on the browser

> Suggestions of additional resources/knowledge prior to use

**Suggestions:**

-   Follow the walkthrough below to familiarize yourself with the scsc in the dApper environment. This is a good starting point to understanding how our scsc interacts with XYO.

> Walkthrough - An example of how to utilize the repo - **optional**

## Walkthrough

### How to add stake on XYO Diviner

### Access our SCSC library through IPFS

**use this hash `QmaHuJh3u5J4W8WYhJnfH1yZUWWwUaehsVLbUPMEd4ymqN`**

### Then direct your browser to use our dAppper tool

**with the hash**

`https://dapper.layerone.co/settings/QmaHuJh3u5J4W8WYhJnfH1yZUWWwUaehsVLbUPMEd4ymqN`

The contract will load, giving you access to the contracts through the contract simulator.

### Start with the XyERC20Token

### Connect your metamask wallet on the Kovan network

### Check your balance using the `balanceOf()` function from the ERC20 contract

**Once you have verified that you have enough balance to stake the diviner, select the XyStakingConsensus contract** This contract stores all the stake of the network

Approve the stake for the Diviner in the XyERC20 contract (make sure that you have the address for the XyStakingConsensus) using the `approve()` function.

Go through metamask to submit the transaction. You have now approved stake, let's keep going.

### Create a diviner

The diviner is represented by a **Stakable token**

-   Mint one token with your wallet address by selecting the XyStakableToken and the address below
-   Select the `mint()` function and paste your wallet address into the `beneficiary` field
-   Confirm the transaction on metamask

This will produce one non-fungible token (ERC721). This is unique to this specific diviner.

Then select the `tokenByIndex()` function and enter `0` for your token address.

Copy the token address, this is **virtual id of your diviner**

### Return to the **XyStakingConsensusContract** and select its address below

-   Select the `stake()` function 
-   Paste the **diviner id** into the stakee field
-   enter an amount to stake (make sure it is in your approved limits!)
-   Click `execute`

### You have just successfully added stake to a diviner

**note** you are the staker, and the **stakingId** is the ledger of the stake that you have in the diviner

To check out the data of the stake, select the `stakeData()` function, paste in the **stakingId** in the sole field.

You will now get a returned JSON object with your stake amount, the block it was staked on, the staker, and the stakee.

> API - _usually required, but can be optional if there is no API or if it is not ready_ 

## API

### XyERC20Token

`transfer` 

-   Sends a specific value of tokens from your XYO account to another

-   **parameters**
    -   `address _to`
    -   `uint256 _value`

`transferFrom`

-   Sends a specific value of tokens from one (not yours) XYO address to another XYO address

-   **parameters**

    -   `address _from`
    -   `address _to`
    -   `uint256 _value`

-   **returns**
    -   `bool success`

`approve`

-   Sets an allowance for tokens for another address **check out our staking walkthrough for an example**

-   **parameters**

    -   `address _spender`
    -   `uint256 _value`

-   **returns**
    -   `bool success`

`approveAndCall`

-   Sets an allowance for tokens for another address with a notification for the other contract

-   **parameters**

    -   `address _spender`
    -   `uint _value`
    -   `bytes memory _extraData`

-   **returns**
    -   `bool success` & `approval notification with _value and _extraData`

`burn`

-   destroys tokens

-   **parameters**

    -   `uint256 _value`

-   **returns**
    -   `bool success`

> A list of XYO team members who maintain this repo - **required**

## Maintainers

-   Kevin Weiler
-   Phillip Lorenzo

> Contributing - Instructions on how to contribute including notices on pre-commit builds, best practices, and necessary steps prior to a pull request.

## Contributing

If you'd like to contribute to the SCSC as a developer or just run the project from source the directions below should help you get started.

First, clone the repository. And set the branch to the develop branch

```sh
  git clone -b develop https://github.com/XYOracleNetwork/dapp-scsc-solidity
```

Then change working directory to that of the repository

```sh
  cd dapp-scsc-solidity
```

Download dependencies

```sh
  yarn install
```

After installing, go ahead and open in your favorite text editor, ours is [Visual Studio Code](https://code.visualstudio.com/)

```sh
 ➜ dapp-scsc-solidity code .
```

Execute these truffle steps:

Set up a local Ganache instance 

```sh
ganache-cli --port 8545 --deterministic < if you want to set the networkID --networkId idNumber>
```

Using the deterministic flag is a good way to keep consistent when in `development` mode

**keep this terminal window open!**

**In another terminal window (or tab)**

Compile the contracts

```sh
truffle compile
```

Migrate the contracts 

```sh
truffle migrate
```

You will see transactions for each contract in your Ganache instance and their addressess

Test the contracts

```sh
truffle test
```

Ganache will work again executing transactions while executing the unit tests.
**Note** if you did not `compile` or `migrate`, no worries, this command will do that for you. 

We recommend testing after any revisions you make to contracts. 

If you would like to know more about how the contracts are upgradeable, read the [PROXY.md](PROXY.md) file.

> Developer Guide - _optional, but recommended_ - Additional notes for developers
> Refer to the developer guide [here for an example](developer-guide.md)

## Developer Guide

Developers should conform to git flow workflow. Additionally, we should try to make sure
every commit builds. Commit messages should be meaningful serve as a meta history for the
repository. Please squash meaningless commits before submitting a pull-request.

> License - **required** - Will almost always be LGPL-3.0

## License

LGPL-3.0

> Credits - _required_ - This can include any third party libraries that you used that require a credit, and the exact sentence with graphic for XY as seen below

## Credits

Made with 🔥and ❄️ by [XY - The Persistent Company](https://www.xy.company)
