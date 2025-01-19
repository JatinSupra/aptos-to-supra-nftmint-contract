# NFT Minting Template for Supra L1 MoveVM
This repository contains a modified version of the Aptos NFT minting dApp template, adapted for deployment on the Supra MoveVM

## Introduction
This project is based on the Aptos NFT minting dApp template. We have made necessary changes to the Move Source, Test contract, and `Move.toml` file, and dependencies to make it compatible with the Supra framework.

## Getting Started

### Prerequisites
Before you begin, ensure you have met the following requirements:

- Node.js and npm installed.

- Supra CLI Setup [From Here](https://docs.supra.com/move/getting-started/supra-cli-with-docker)

### Installation

1. **Create a new Aptos dApp**

Open your terminal, navigate to the directory where you want to create the dApp, and run the following command:

```bash
npx create-aptos-dapp@latest
```

2. **Select the NFT Minting dApp Template**

Follow the prompts and select the NFT minting dApp template. This will create the base structure of the Aptos dApp. [More Info Here](https://www.npmjs.com/package/create-aptos-dapp)

### Modifications for Supra Deployment.

**1.** Update the `Move.toml` file to include the correct dependencies for the Supra framework. Here is an example:

```toml
[dependencies.SupraFramework]
git = "https://github.com/Entropy-Foundation/aptos-core.git"
rev = "dev"
subdir = "aptos-move/framework/supra-framework"

[dependencies]
AptosTokenObjects = { git = "https://github.com/Entropy-Foundation/aptos-core.git", rev = "dev", subdir = "aptos-move/framework/aptos-token-objects" }

TokenMinter = { git = "https://github.com/JatinSupra/token-minter.git", rev = "main", subdir = "token-minter" }
```

**2.** Modify the Source Move contract to integrate with the Supra framework. Here is an **example** of how the framework part of the contract should look after Supra Framework Changes:

```move
    use supra_framework::supra_account;
    use supra_framework::event;
    use supra_framework::object::{Self, Object, ObjectCore};
    use supra_framework::timestamp;
```
**Kindly PLEASE Check the whole contract from `contract/sources/launchpad.move` for all the changes req in your contract.**

**3.** Update the Test Move contract to ensure compatibility with the Supra framework. Here is an **example** of how the framework part of the contract should look after Supra Framework Changes:

```move
    use supra_framework::supra_coin::{Self, SupraCoin};
    use supra_framework::coin;
    use supra_framework::account;
    use supra_framework::timestamp;
```

**Kindly PLEASE Check the whole contract from `contract/tests/test_end_to_end.move` for all the changes req in your contract.**

### Deployment

Deploy the Contract via the Supra MoveVM CLI, Commands to Compile, test, and Publishing on the Blockchain are:

**- Compile**
```sh
supra move tool compile --package-dir /supra/configs/move_workspace/<PROJECT_NAME>
```
**- Test**
```sh
supra move tool test --package-dir /supra/configs/move_workspace/<PROJECT_NAME>
```
**- Publish**
```sh
supra move tool publish --package-dir /supra/configs/move_workspace/<PROJECT_NAME> --profile <YOUR_PROFILE> --url <RPC_URL>
```

**- RPC to use (MoveVM Testnet):**
```
https://rpc-testnet.supra.com/
```


**NOTE:** Make sure you setup the CLI following the guide throughly [From Here](https://docs.supra.com/move/getting-started/supra-cli-with-docker)

## Conclusion
Following these steps will allow you to modify and deploy the Aptos NFT minting dApp template on the Supra MoveVM L1. If you encounter any issues or have further questions, feel free to open an issue or reach out for support.

## Contribution
Feel free to contribute to this project by submitting pull requests or opening issues, all contributions that enhance the functionality or user experience of this project are welcome.

