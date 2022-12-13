# stacks miner docker

## update configs

For a miner, at a minimum you'll need to:

1. create a bitcoin wallet (or import an address)
2. add the btc privatkey to the stacks config ( replace `%%PRIVATEKEY%%` in sample configs below)

### Testnet

- [bitcoin testnet config](./config/bitcoin.testnet.conf)
- [stacks miner testnet config](./config/stacks.testnet.miner.toml)

### Mainnet

- [bitcoin mainnnet config](./config/bitcoin.mainnet.conf)
- [stacks miner mainnet config](./config/stacks.mainnet.miner.toml)

## Run the miner

### Install/Upgrade docker-compose

- [jq binary](https://stedolan.github.io/jq/download/)

```bash
#You will need to have jq installed, or this snippet won't run.
VERSION=$(curl --silent https://api.github.com/repos/docker/compose/releases/latest | jq .name -r)
DESTINATION=/usr/local/bin/docker-compose
sudo curl -L https://github.com/docker/compose/releases/download/${VERSION}/docker-compose-$(uname -s)-$(uname -m) -o $DESTINATION
sudo chmod 755 $DESTINATION
```

### start container

On first start, `docker-compose` will build the required images locally - this can take a while to compile the binaries and create the images.

```bash
$ docker-compose up -d
```

## TODO

1. use distroless image for build artifact - or the smallest viable image possible
2. remove shell? - maybe create a few variants of dockerfile for different scenarios (alpine, no shell, distroless, etc)
3. for v2, write script to generate the keys

- import address into btc
- adjust the stacks config to use the privatekey

4. k8s chart(s)?
5. script for checking on chain status during sync

- check against public node block height every 120s or so
- script to expand envvar into the stacks config (requires writable path for the config - not a fan of this)
