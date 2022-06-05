## Overview
- [How to create Solana Token](https://moralis.io/how-to-create-a-solana-token-in-5-steps/)
- SOL is the cryptocurrency that runs on the Solana blockchain, and it also acts as a governance token
- Moreover, SOL is a so-called SPL token (token standard for the Solana blockchain). SPL tokens are to Solana what ERC-20, ERC-721, and ERC-1155 tokens are to the Ethereum network.
- The ERC-20 standard regulates fungible tokens, ERC-721 NFTs, and ERC-1155 semi-fungible tokens.
- In the Solana ecosystem, there is simply one program defining the common implementation of both fungible tokens and NFTs. For this reason, there is essentially one token standard regulating both token types. 

## Installation of Solana CLI
- Please refer document [here](https://docs.solana.com/cli/install-solana-cli-tools).
- `solana --version`
- `solana-install update`

## Installation of Rust
- https://rustup.rs/ OR
- `sudo curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`

## Installation of SPL CLI
- `sudo apt-get update`
- `sudo apt install build-essential`
- `sudo apt install libudev-dev`
- `sudo apt-get install pkg-config libssl-dev`
- `cargo install spl-token-cli`
- `spl-token --version`

## Create filesystem wallet
- `solana-keygen new`
- `solana balance`

## Change solana cluster
- `solana config get`
- `solana config set --url https://api.devnet.solana.com`
- `solana airdrop 1`

## Create fungible token
- `spl-token create-token` # create a new token
- `spl-token supply <tokenid>` # to check the balance of a token
- `spl-token create-account <tokenid>` # to create account for a token (required for minting)
- `spl-token accounts` # to list all the tokens having account associated.
- `spl-token mint <tokenid> <tokens_to_mint>` # to mint a number of tokens

## Create NFT token
- `spl-token create-token --decimals 0` # create a new NFT token
- `spl-token create-account <tokenid>` #  to create account for a token (required for minting)
- `spl-token supply <tokenid>` # to check the balance of a token
- `spl-token accounts` # to list all the tokens having account associated.
- `spl-token mint <tokenid> 1` # to mint a NFT token
- `spl-token authorize <tokenid> mint --disable` # to disable the mint.

## Transfer token from local wallet to phantom wallet
- `spl-token transfer <tokenid> ALL <phantom_wallet_address> --fund-recipient --allow-unfunded-recipient`

# Token-list
In Phantom wallet, to add Name, Symbol and Icon, please follow this https://github.com/solana-labs/token-list