# Truffle React boilerplate

Truffle + React + Babel + Webpack

[中文 README](README.zh-TW.md)

## Getting Started

install npm and [truffle](https://github.com/trufflesuite/truffle) `npm install -g truffle`

install yarn (not required)

```
git clone https://github.com/wayne5540/truffle-react-boilerplate.git my-project
cd my-project
yarn install
```

Running client:

install [testrpc](https://github.com/ethereumjs/testrpc) `npm install -g ethereumjs-testrpc`

Install [metamask](https://metamask.io/)(Chrome) or [mist](https://github.com/ethereum/mist/releases)

```
testrpc
truffle compile
truffle migrate
yarn start
```

Switch your wallet using local node 8545 port

Go to `localhost:8080` and play around

### Interact your deployed contract with truffle console

Example

**Get owner address**

```
SimpleStorage.deployed().then(function(instance) { instance.owner().then((address) => console.log(address)) } )
```

**Set value**

```
SimpleStorage.deployed().then(function(instance) { instance.setValue(10) } )
```

### Test

```
truffle test
```

## Trouble Shooting

### I don't have eth in my wallet

**under testrpc (local node)**

run those commands, it will send 2 ether to your test wallet

```
truffle console

web3.eth.sendTransaction({from: web3.eth.accounts[2], to: 'YOUR_ETH_ADDRESS', value: web3.toWei(2, "ether")})
```

**under ropsten testnet**

Go to http://faucet.ropsten.be:3001/ and get some eth to your address


## Deployment

Since this project use Ethereum as "database", you can deploy contract to testnet or main chain at your local, and serve client code into any web server.

### Deploy to testnet (or Main chain)

You need to sync testnet node first before you deploy, the easiest way to do this is by using [geth](https://github.com/ethereum/go-ethereum/wiki/geth) or [parity](https://github.com/paritytech/parity) to sync node, example here are using `geth`

**create account under testnet**

https://github.com/ethereum/go-ethereum/wiki/Managing-your-accounts

**deploy**

In first console
```
geth --testnet --rpc --datadir /usr/local/var/ethereum-testnet-data console 2>> /usr/local/var/log/geth.testnet.log

personal.unlockAccount(eth.accounts[0], "YOUR_ACCOUNT_PASSWORD", 36000)
```

In another console
```
truffle migrate --network ropsten
```

All done.

## Bugs

- [] Can't find web3 after page refreshed
  - `Uncaught (in promise) TypeError: Cannot read property 'apply' of undefined`