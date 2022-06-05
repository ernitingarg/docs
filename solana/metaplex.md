## Metaplex Candy Machine 2

### Metaplex Setup
```
git clone https://github.com/metaplex-foundation/metaplex.git
cd js
yarn install && yarn bootstrap && yarn build
```

### Solana Airdop
```
solana config set --url https://api.devnet.solana.com
solana-keygen new --outfile ../.config/solana/devnet.json --force
solana config set --keypair ../.config/solana/devnet.json
solana airdrop 4
solana balance
```

### Configurations
- Create sub folder `assets` under same directoy.
- Under `assets` folder, keep all NFT images with name starting with index `0` (eg: 0.jpg...10.jpg)
- Under `assets` folder, keep corresponding metadata json for each NFT. (eg: 0.json...10.json)
```json
{
    "name": "Number #0001",
    "symbol": "FAM",
    "description": "Collection of 2 numbers of tom and jerry NFTs on the blockchain. This is the number 1/2.",
    "seller_fee_basis_points": 1000,
    "image": "0.png",
    "attributes": [
        {
            "trait_type": "Company",
            "value": "Final AIM"
        },
        {
            "trait_type": "Status",
            "value": "Demo"
        },
        {
            "trait_type": "Entertainment",
            "value": "Cartoon"
        }
    ],
    "properties": {
        "creators": [
            {
                "address": "AATSmMooiKqSmk7oV6Lc2gEXQqjuv8arPYM9eFYzyKaJ",
                "share": 100
            }
        ],
        "files": [
            {
                "uri": "0.png",
                "type": "image/png"
            }
        ]
    },
    "collection": {
        "name": "Tom and Jerry",
        "family": "Carton NFT"
    }
}
```
- In each metadata json, replace the `address` with public key of the wallet created above.
- Create metaplex `config.json` (in root directoy) required for candy machine defining NFT mint.
```json
{
    "price": 1.0,
    "number": 2,
    "gatekeeper": null,
    "solTreasuryAccount": "9eCPBzGfuFDB8cVTwxtFF8gUebuJzUyE5LGiQww3MJNV",
    "splTokenAccount": null,
    "splToken": null,
    "goLiveDate": "25 Dec 2021 00:00:00 GMT",
    "endSettings": null,
    "whitelistMintSettings": null,
    "hiddenSettings": null,
    "storage": "arweave",
    "ipfsInfuraProjectId": null,
    "ipfsInfuraSecret": null,
    "nftStorageKey": null,
    "awsS3Bucket": null,
    "noRetainAuthority": false,
    "noMutable": false
}
```
- Replace `solTreasuryAccount` with public key of the wallet created above.
- Replace `number` with actual number of NFTs to be uploaded.
- Replace all other required parameters (eg: price, storage provider, go-live date etc).

### Upload assets
```
ts-node js/packages/cli/src/candy-machine-v2-cli.ts upload -e devnet -k ../.config/solana/devnet.json -cp config.json -c example ./assets
```

### Verify uploads
```
ts-node js/packages/cli/src/candy-machine-v2-cli.ts verify_upload -e devnet -k ../.config/solana/devnet.json -cp config.json -c example
```

### Mint one token
```
ts-node js/packages/cli/src/candy-machine-v2-cli.ts mint_one_token -e devnet -k ../.config/solana/devnet.json -cp config.json -c example 
```

### Mint multiple tokens
```
ts-node js/packages/cli/src/candy-machine-v2-cli.ts mint_multiple_tokens -e devnet -k ../.config/solana/devnet.json -cp config.json -c example --number 2
```

### Update CM settings
```
ts-node js/packages/cli/src/candy-machine-v2-cli.ts update_candy_machine -e devnet -k ../.config/solana/devnet.json -cp config.json -c example
```

### Verify CM settings
```
ts-node js/packages/cli/src/candy-machine-v2-cli.ts show -e devnet -k ../.config/solana/devnet.json -c example
```

### Import wallet keys
- Login to phantom -> `Add/Connect Wallet` -> `Import Private Key`
- Copy private key content from `../.config/solana/devnet.json` and paste.

## Candy Machine Mint UI

### Candy Machine Mint UI local deployment
- Go to folder `js/packages/candy-machine-ui`
- Find file with extension `*.env` and rename it to just with `.env`
- `.env` file should have below contents
```env
REACT_APP_CANDY_MACHINE_ID=J4hFeorEW8TVyvJbt2cM1Jaz1Q3ChsQVWBoCikd8hFoJ
REACT_APP_SOLANA_NETWORK=devnet
REACT_APP_SOLANA_RPC_HOST=https://metaplex.devnet.rpcpool.com/
SKIP_PREFLIGHT_CHECK=true
``` 
- Replace `REACT_APP_CANDY_MACHINE_ID` with candy machine address which is generated during nft upload.
- You can also find candy machine address in file `.cache/devnet-example.json`
- Now, run below commands to launch mint UI
```
cd js/packages/candy-machine-ui
yarn install && yarn start
```

### Candy Machine Mint UI vercel deployment
- In Visual Studio code, open folder `metaplex\js\packages\candy-machine-ui`
- Open new terminal and run `yarn build`
- The above command will create a new deployment folder `build`
- Copy this folder and paster it somewhere else (eg: desktop)
- In open visual studio code, open this build folder
- Publish this folder in github
- In `vercel`, import your repository and deploy. 

## Metaplex Storefront

### Metaplex Storefront local deployment
- Fork repository `https://github.com/metaplex-foundation/metaplex` to your new repository.
- `git clone <your_repo> <local_path>`
- In `js/packages/web/.env`, update `REACT_APP_STORE_OWNER_ADDRESS_ADDRESS` with public key of your wallet.
- In Visual studio, Open terminal and run `cd js`
- `yarn install && yarn bootstrap`
- `yarn start`
- Access metaplex [url](http://localhost:3000/)

### Metaplex Storefront github deployment
- All below instructions can be found in official [page](https://docs.metaplex.com/storefront/deploy).
- In `js/packages/web/package.json`, update 
	- specify your repo URL instead of https://github.com/metaplex-foundation/metaplex (for example, https://github.com/my-name/my-metaplex)
	- set ASSET_PREFIX to repo name (for example, ASSET_PREFIX=/my-metaplex/)
- `cd js/packages/web`
- `yarn deploy`

### Metaplex Storefront vercel deployment
- Please follow instructions in official [page](https://docs.metaplex.com/storefront/deploy#vercel).

## Upload manually in Arweave
```
npm install -g arweave-deploy
arweave key-create new-arweave-key.json
arweave key-save new-arweave-key.json
```