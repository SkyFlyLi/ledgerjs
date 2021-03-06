<img src="https://user-images.githubusercontent.com/211411/34776833-6f1ef4da-f618-11e7-8b13-f0697901d6a8.png" height="100" />

[Github](https://github.com/LedgerHQ/ledgerjs/),
[Ledger Devs Slack](https://ledger-dev.slack.com/)

## @ledgerhq/hw-app-eth

Ledger Hardware Wallet ETH JavaScript bindings.

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

-   [byContractAddress](#bycontractaddress)
    -   [Parameters](#parameters)
-   [list](#list)
-   [Eth](#eth)
    -   [Parameters](#parameters-1)
    -   [Examples](#examples)
    -   [getAddress](#getaddress)
        -   [Parameters](#parameters-2)
        -   [Examples](#examples-1)
    -   [provideERC20TokenInformation](#provideerc20tokeninformation)
        -   [Parameters](#parameters-3)
        -   [Examples](#examples-2)
    -   [signTransaction](#signtransaction)
        -   [Parameters](#parameters-4)
        -   [Examples](#examples-3)
    -   [getAppConfiguration](#getappconfiguration)
    -   [signPersonalMessage](#signpersonalmessage)
        -   [Parameters](#parameters-5)
        -   [Examples](#examples-4)
    -   [starkGetPublicKey](#starkgetpublickey)
        -   [Parameters](#parameters-6)
    -   [starkSignOrder](#starksignorder)
        -   [Parameters](#parameters-7)
    -   [starkSignTransfer](#starksigntransfer)
        -   [Parameters](#parameters-8)
    -   [starkProvideQuantum](#starkprovidequantum)
        -   [Parameters](#parameters-9)

### byContractAddress

Retrieve the token information by a given contract address if any

#### Parameters

-   `contract` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 

Returns **TokenInfo?** 

### list

list all the ERC20 tokens informations

Returns **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;TokenInfo>** 

### Eth

Ethereum API

#### Parameters

-   `transport` **Transport&lt;any>** 
-   `scrambleKey` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**  (optional, default `"w0w"`)

#### Examples

```javascript
import Eth from "@ledgerhq/hw-app-eth";
const eth = new Eth(transport)
```

#### getAddress

get Ethereum address for a given BIP 32 path.

##### Parameters

-   `path` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a path in BIP 32 format
-   `boolDisplay` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** 
-   `boolChaincode` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** 

##### Examples

```javascript
eth.getAddress("44'/60'/0'/0/0").then(o => o.address)
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;{publicKey: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String), address: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String), chainCode: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?}>** an object with a publicKey, address and (optionally) chainCode

#### provideERC20TokenInformation

This commands provides a trusted description of an ERC 20 token
to associate a contract address with a ticker and number of decimals.

It shall be run immediately before performing a transaction involving a contract
calling this contract address to display the proper token information to the user if necessary.

##### Parameters

-   `info` **any** : a blob from "erc20.js" utilities that contains all token information.
    -   `info.data`  

##### Examples

```javascript
import { byContractAddress } from "@ledgerhq/hw-app-eth/erc20"
const zrxInfo = byContractAddress("0xe41d2489571d322189246dafa5ebde1f4699f498")
if (zrxInfo) await appEth.provideERC20TokenInformation(zrxInfo)
const signed = await appEth.signTransaction(path, rawTxHex)
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)>** 

#### signTransaction

You can sign a transaction and retrieve v, r, s given the raw transaction and the BIP 32 path of the account to sign

##### Parameters

-   `path` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 
-   `rawTxHex` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 

##### Examples

```javascript
eth.signTransaction("44'/60'/0'/0/0", "e8018504e3b292008252089428ee52a8f3d6e5d15f8b131996950d7f296c7952872bd72a2487400080").then(result => ...)
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;{s: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String), v: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String), r: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)}>** 

#### getAppConfiguration

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;{arbitraryDataEnabled: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number), erc20ProvisioningNecessary: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number), starkEnabled: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number), version: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)}>** 

#### signPersonalMessage

You can sign a message according to eth_sign RPC call and retrieve v, r, s given the message and the BIP 32 path of the account to sign.

##### Parameters

-   `path` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 
-   `messageHex` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 

##### Examples

```javascript
eth.signPersonalMessage("44'/60'/0'/0/0", Buffer.from("test").toString("hex")).then(result => {
var v = result['v'] - 27;
v = v.toString(16);
if (v.length < 2) {
v = "0" + v;
}
console.log("Signature 0x" + result['r'] + result['s'] + v);
})
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;{v: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number), s: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String), r: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)}>** 

#### starkGetPublicKey

get Stark public key for a given BIP 32 path.

##### Parameters

-   `path` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a path in BIP 32 format
-   `boolDisplay` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** 

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[Buffer](https://nodejs.org/api/buffer.html)>** the Stark public key

#### starkSignOrder

sign a Stark order

##### Parameters

-   `path` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a path in BIP 32 format
-   `sourceTokenAddress` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** 
-   `sourceQuantization` **BigNumber** quantization used for the source token
-   `destinationTokenAddress` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** 
-   `destinationQuantization` **BigNumber** quantization used for the destination token
-   `sourceVault` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** ID of the source vault
-   `destinationVault` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** ID of the destination vault
-   `amountSell` **BigNumber** amount to sell
-   `amountBuy` **BigNumber** amount to buy
-   `nonce` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** transaction nonce
-   `timestamp` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** transaction validity timestamp

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[Buffer](https://nodejs.org/api/buffer.html)>** the signature

#### starkSignTransfer

sign a Stark transfer

##### Parameters

-   `path` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a path in BIP 32 format
-   `transferTokenAddress` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** 
-   `transferQuantization` **BigNumber** quantization used for the token to be transferred
-   `targetPublicKey` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** target Stark public key
-   `sourceVault` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** ID of the source vault
-   `destinationVault` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** ID of the destination vault
-   `amountTransfer` **BigNumber** amount to transfer
-   `nonce` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** transaction nonce
-   `timestamp` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** transaction validity timestamp

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[Buffer](https://nodejs.org/api/buffer.html)>** the signature

#### starkProvideQuantum

provide quantization information before singing a deposit or withdrawal Stark powered contract call

It shall be run following a provideERC20TokenInformation call for the given contract

##### Parameters

-   `operationContract` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** contract address of the token to be transferred (not present for ETH)
-   `operationQuantization` **BigNumber** quantization used for the token to be transferred

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)>** 
