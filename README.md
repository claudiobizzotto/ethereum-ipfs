(not so) Simple storage
-----------------------

A bare-bones example on how to use IPFS and Ethereum from the same application. 
Check [this wiki](https://github.com/ledgerlabs/ethereum-getting-started/wiki/Anatomy-of-a-Contract) 
for the original, Ethereum-only idea.

## Description

This application deploys a contract to an Ethereum blockchain (the public Ethereum 
testnet or a local Ethereum testnet) and uses it to keep track of an image stored 
in an IPFS blockchain (the public IPFS "testnet" or a local IPFS testnet). The image 
itself is stored in the IPFS *file system* - the only data stored in the Ethereum 
contract is the IPFS hash that corresponds to the image. [Images are used in the 
examples below, but any other file types could be used as well]

## Requirements

1. An Ethereum node with one or more accounts unlocked (e.g, `--unlock 0`), RPC 
enabled (`--rpc`) and the proper RPC CORS set up (e.g, `--rpccorsdomain = "*"`)
2. An IPFS node that doesn't block API calls from external origins (more on this 
below)
3. A modern web browser (preferably Opera) //! opinion detected :)

### Local Ethereum node

Check out [this guide](https://github.com/ledgerlabs/ethereum-getting-started/wiki/local-node) 
if you want to run a local Ethereum node.

### Local IPFS node

First, [install IPFS](https://ipfs.io/docs/install/) on your machine.
<br /><br />
I suggest you don't override the IPFS directory associated to your localhost's user 
(normally at `~/.ipfs`), so the first thing you want to do is set up an IPFS directory 
specific for development. You can define one under the current project's root, after 
you check out this repo:

```SHELL
$ export IPFS_PATH=.ipfs
$ ipfs init
```

After that, you need to loosen your IPFS node's CORS restrictions:

```SHELL
$ ipfs config --json API.HTTPHeaders.Access-Control-Allow-Origin '["*"]'
$ ipfs config --json Gateway.HTTPHeaders.Access-Control-Allow-Origin '["*"]'
```

You can now start the IPFS daemon:

`$ ipfs daemon`

## Project structure

* `ipfs.js`
  The IPFS interface in JavaScript (repository [here](https://github.com/ipfs/js-ipfs-api)).
  You can find the source (*broweserified*) code [here](https://npmcdn.com/ipfs-api@4.0.0/dist/index.js)

* `web3.min.js`
  The Ethereum interface in JavaScript (repository [here](https://github.com/ethereum/web3.js))

* `NotSoSimpleStorage.sol`
  Ethereum contract written in Solidity

* `NotSoSimpleStorage.html`
  The web application itself. It contains the core logic behind the interactions 
  to IPFS and Ethereum

## Usage

Open `NotSoSimpleStorage.html` in a text editor and replace the values under the 
`config` section according to your setup:

```JAVASCRIPT
// Config
var ipfsHost    = 'localhost',
    ipfsAPIPort = '5001',
    ipfsWebPort = '8080',
    web3Host    = 'localhost',
    web3Port    = '8545';
```

Now open `NotSoSimpleStorage.html` from your web browser (no web server needed). 
You'll need a JavaScript console to use the application - most web browsers come 
with one installed out of the box. From there, just follow the instructions on the 
web page.

