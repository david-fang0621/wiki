### Tech stack

DeFi, AirDrop, Anchor, Rust, Mocha, NFT drop, Metaplex Candy Machine V1, V2, GIF portal in the metaverse
! Solana program is "stateless"

https://wecap.io/stake/ (PHANT token staking)
https://webuyyournft.net/ (Solana NFTselling project)
https://solana.starbet666.com/stake (WOS token staking)

### Airdrop Project

```
mkdir airdrop-project
cd airdrop-project
npm init -y
npm install --save @solana/web3.js
```

### Setting up Solana

https://github.com/david-fang0621/solana-env-setup.git

Install SPL crate
cargo install spl-token-cli

Create wallet
solana-keygen new --force
5WtWcqGT7ecKYPQX4vGGX4xzu4CGpLCJrEP6xbEzUzRi

solana-keygen pubkey // get pubkey
solana balance --url devnet // see balance

Confirm the wallet on Solana
[https://explorer.solana.com](https://explorer.solana.com/)

Token airdrop
solana airdrop 2 [pubkey] --url devnet

Create token (SPL)
spl-token create-token --url devnet
CABkxsZJNW2u4W1E4vrvBEQYvL2WDoc6hJXQdKJiQuRg

Mint token
spl-token create-account [token address] --url devnet
ThUbZ9ka8AwJEnFjdq56gHgkBpQvkkZEEFAxeQSSxfo

spl-token balance [token address] --url devnet
spl-token mint [token address] 1000 --url devnet

Limit total supply & burn
spl-token supply [token address] --url devnet
spl-token authorize [token address] mint --disable --url devnet

spl-token burn [account address] 500 --url devnet

Phantom wallet
BdyQMv7X5s4euP7uwWuUwcb4MoVojq6ifTiWE9bcn3dp
spl-token transfer [token address] 150 [friend's wallet address] --url devnet --allow-unfunded-recipient --fund-recipient

### Anchor project

anchor init [project name]
anchor build
anchor test

### Sonala NFT

Metaplex Candy Machine V1, V2
Metaplex Candy machine -> returns a _random_ NFT from a collection
git clone https://github.com/metaplex-foundation/metaplex.git ~/metaplex-foundation/metaplex
yarn install --cwd ~/metaplex-foundation/metaplex/js/
npm install -g ts-node
ts-node ~/metaplex-foundation/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts --version

Deploy the NFTs to the devnet
solana-keygen new --outfile ~/.config/solana/devnet.json

ts-node ~/metaplex-foundation/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts upload -e devnet -k ~/.config/solana/devnet.json -cp config.json ./assets
