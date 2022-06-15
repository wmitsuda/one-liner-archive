# What's this?

Do you want to run an archive node + block explorer in your machine using only 1 command and (_almost_) no devops knowledge?

This repo provides a series of pre-configured docker-compose files that spin-up a Prysm (consensus layer client) + Erigon (execution layer archive node; alpha series) + Otterscan (block explorer).

Just follow the instructions, fill in the gaps and run it. Or customize it for your needs. Or improve it and contribute it back, it's all opensource.

> The twitter 🧵 that originated this project: https://twitter.com/wmitsuda/status/1535148383555530757

# How much disk space does it take?

As of Jun/2022.

## Sepolia testnet

- 1.5GB for Erigon sepolia archive

## Post-merge ropsten testnet

- 260GB for Erigon ropsten archive
- 1GB for Prysm ropsten beacon chain

# Run it

## Sepolia testnet

1. Clone this repo
2. Create an empty dir for erigon (`<erigon-data-dir>`) database
3. Run: `ERIGON_DATA="<erigon-data-dir>" docker-compose -f sepolia.yml up`
4. Wait a few hours until the archive node finishes syncing sepolia
5. You should be able to access Otterscan block explorer to browse your archive by accessing: http://localhost:3000/

> This script will be updated soon as clients gets updated to the upcoming sepolia merge

## Post-merge ropsten testnet

1. Clone this repo
2. Create empty dirs for erigon (`<erigon-data-dir>`) and prysm (`<prysm-data-dir>`) databases
3. Run: `PRYSM_DATA="<prysm-data-dir>" ERIGON_DATA="<erigon-data-dir>" docker-compose -f ropsten.yml up`
4. Wait 1-2 days until the archive node finishes syncing ropsten
5. You should be able to access Otterscan block explorer to browse your archive by accessing: http://localhost:3000/

> Remember that ropsten is deprecated and will have no more upgrades after the merge
