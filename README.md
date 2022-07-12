# What's this?

Do you want to run an archive node + block explorer in your machine using only 1 command and (_almost_) no devops knowledge?

This repo provides a series of pre-configured docker compose files that spin-up a Prysm (consensus layer client) + Erigon (execution layer archive node; alpha series) + Otterscan (block explorer).

Just follow the instructions, fill in the gaps and run it. Or customize it for your needs. Or improve it and contribute it back, it's all opensource.

> The twitter 🧵 that originated this project: https://twitter.com/wmitsuda/status/1535148383555530757

# How much disk space does it take?

As of Jul/2022.

## Sepolia testnet

- 2.1GB for Erigon sepolia archive
- 320MB for Prysm sepolia beacon chain

## Goerli testnet

- 162GB for Erigon goerli archive
- ?GB for Prysm prater beacon chain

## Ropsten testnet (deprecated)

- 266GB for Erigon ropsten archive
- 4.3GB for Prysm ropsten beacon chain

# Run it

## Requirements

- Docker compose V2 (see: https://stackoverflow.com/a/66516826/49530)

## Sepolia testnet

1. Clone this repo
2. Create empty dirs for erigon (`<erigon-data-dir>`) and prysm (`<prysm-data-dir>`) databases
3. On `/sepolia` directory, run: `PRYSM_DATA="<prysm-data-dir>" ERIGON_DATA="<erigon-data-dir>" docker compose up`
4. Wait a few hours until the archive node finishes syncing sepolia
5. You should be able to access Otterscan block explorer to browse your archive by accessing: http://localhost:3000/

## Goerli testnet

1. Clone this repo
2. Create empty dirs for erigon (`<erigon-data-dir>`) and prysm (`<prysm-data-dir>`) databases
3. Run: `PRYSM_DATA="<prysm-data-dir>" ERIGON_DATA="<erigon-data-dir>" docker compose -f goerli.yml up`
4. Wait 2 days until the archive node finishes syncing goerli
5. You should be able to access Otterscan block explorer to browse your archive by accessing: http://localhost:3000/

## Ropsten testnet (deprecated)

1. Clone this repo
2. Create empty dirs for erigon (`<erigon-data-dir>`) and prysm (`<prysm-data-dir>`) databases
3. On `/ropsten` diretory, run: `PRYSM_DATA="<prysm-data-dir>" ERIGON_DATA="<erigon-data-dir>" docker compose up`
4. Wait 1-2 days until the archive node finishes syncing ropsten
5. You should be able to access Otterscan block explorer to browse your archive by accessing: http://localhost:3000/

> Remember that ropsten is deprecated and will have no more upgrades after the merge
