# truffle-source-verify

This truffle plugin allows you to automatically verify your smart contracts' source code on Etherscan/Blockscout, straight from the Truffle CLI.

It extends [truffle-plugin-verify](https://github.com/rkalis/truffle-plugin-verify) to also support Blockscout.

## Installation

1. Install the plugin with npm or yarn
   ```
   yarn add @zcorefinance/truffle-source-verify
   ```
   or
   ```
   npm i -D @zcorefinance/truffle-source-verify
   ```
2. Add the plugin to your `truffle-config.js` file

   ```js
   module.exports = {
     /* ... rest of truffle-config */

     plugins: ["truffle-source-verify"],
   };
   ```
   
3. Add ZCore Testnet network

   ```js
   zcrTestnet:{
     provider: function() {
       return new HDWalletProvider("PRIVATE_KEY", "https://rpc-testnet.zcore.cash")
     },
     network_id: "3331",
     gasPrice: 1000000000,
   },
   ```

## Usage

### On the command-line

Before running verification, make sure that you have actually deployed your contracts to a public network with Truffle.

To verify your contracts on ZCore, run:

```
npx truffle run blockscout SomeContractName AnotherContractName --network zcrTestnet --license UNLICENSED [--debug]
```


See [truffle-plugin-verify](https://github.com/rkalis/truffle-plugin-verify) for more information.

### In Javascript

```
// file: ./scripts/test_verify.js
// Usage: npx truffle exec ./scripts/test_verify.js --network rinkeby

const { verify } = require("truffle-source-verify/lib");

async function main() {
  const idx = process.argv.indexOf("--network");
  const network = process.argv[idx + 1];
  await verify(["BasicContract"], network, "UNLICENSED");
}

module.exports = (cb) => main().then(cb).catch(cb);
```
