# How To Manage The Whole Lifecycle Of A Metaplex Candy Machine
This repository is a demonstration of the tools neccessary to manage the whole lifecycle of 
a Metaplex Candy Machine using the Solana CLI and the Sugar CLI, as well as 
the project structure for doing so. This example is using devnet. This example and 
the steps for this example assumes you can have created a project structure similar to this one.

## Install
- [Solana CLI](https://docs.solanalabs.com/cli/install)
- [Sugar CLI](https://developers.metaplex.com/candy-machine/sugar/installation)

## Steps

### Create A Solana Account

Use Solana's command-line tool `solana-keygen` to generate a keypair file. This keypair file
will be used to fund the creation of the Metaplex Candy Machine.

```bash
$ solana-keygen new --no-passphrase -o metaplex-candy-machine.json
```

The file `metaplex-candy-machine.json` contains your unencrypted keypair.
To display its public key, run:

```bash
$ solana-keygen pubkey metaplex-candy-machine.json
```

[Reference](https://docs.solanalabs.com/cli/wallets/file-system)

### Fund The Newly Created Solana Account

We will fund the newly created Solana account using the [Sol Faucet](https://solfaucet.com/) for devnet.
Copy the public key that is outputted by running:

```bash
$ solana-keygen pubkey metaplex-candy-machine.json
```

Paste the public key into the Sol Faucet and airdrop some SOL on the devnet. You can check that the airdrop was
successful by running:

```bash
$ solana balance metaplex-candy-machine.json --url https://api.devnet.solana.com
```

The output should be the amount of SOL you requested to airdrop.

[Reference](https://solana.com/developers/guides/getstarted/solana-token-airdrop-and-faucets)

### Running Sugar

Inside your project's directory run:

```bash
$ sugar launch -k ~/metaplex-candy-machine.json -r https://api.devnet.solana.com
```

This command will start an interactive process of creating 
your config file and deploying a Candy Machine to Solana devnet using the Solana account 
we created in the previous steps.

At the end of the execution of the launch command, a Candy Machine will be deployed on-chain. 
You can use the mint command to mint an NFT:

```bash
$ sugar mint
```

When all NFTs have been minted, you can close your Candy Machine and reclaim the account rent:


```bash
$ sugar withdraw
```

[Reference](https://developers.metaplex.com/candy-machine/sugar/getting-started)

## References
- [Solana File System Wallets Using The CLI](https://docs.solanalabs.com/cli/wallets/file-system)
- [Solana Airdrop](https://solana.com/developers/guides/getstarted/solana-token-airdrop-and-faucets)
- [Sugar CLI](https://developers.metaplex.com/candy-machine/sugar/getting-started)
- [Candy Machine Configuration File](https://developers.metaplex.com/candy-machine/sugar/configuration)
- [Candy Machine Token Standards (Assets)](https://developers.metaplex.com/token-metadata/token-standard)