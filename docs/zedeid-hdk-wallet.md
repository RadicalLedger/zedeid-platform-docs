# zedeid-hdk-wallet
A wrapper package of bip32 and bip39 to generate ethr decentralized IDs

## Availability
- Source Code on [GitHub](https://github.com/RadicalLedger/zedeid-hdk-wallet)
- For Node.js via [npm](https://www.npmjs.com/package/@zedeid-sdk/zedeid-hdk-wallet)
- For Browser via [jsdelivr](https://cdn.jsdelivr.net/npm/@zedeid-sdk/zedeid-hdk-wallet/dist/browser/zedeid-hdk-wallet.js)
- Sample Implementation on [GitHub](https://github.com/RadicalLedger/hdk-wallet-lib-sample)


## Installation

1. Clone repository
2. run *npm run build* 
3. npm install < local repository directory >

## Usage
---
### generateMnemonic

Generate a random mnemonic with a given strength to represent a private key. This is a root key for a set of hierachically deterministic keys (HD Keys).

```import { generateMnemonic } from 'did-hd-wallet';```


#### Parameters

- strength : number - Integer between 128 - 256.

#### Returns

- mnemonic: string - mnemonic words.  Either 12 to 24 depending on the strength specified (for 128 or 256 respectively).


---
### validateMnemonic

Validates a given mnemonic string.

```import { validateMnemonic } from 'did-hd-wallet';```

#### Parameters

- mnemonic : string - Mnemonic string.

#### Returns

- validity: boolean - whether mnemonic string is valid or not.

---
### getSeedFromMnemonic
Gets the seed from mnemonic words.

```import { getSeedFromMnemonic } from 'did-hd-wallet';```

#### Parameters

- mnemonic : string - valid mnemonic phrase.

#### Returns

- seed: string - hex encoded seed.

---
### publicKeyToETH

Gets the ethereum address of a public key.

```import { publicKeyToETH } from 'did-hd-wallet';```

#### Parameters

- publicKey : string - public key.

#### Returns

- ethereumAddress: string - Ethereum address corresponding to the public key.

---
### getDID
Gets the ethereum decentralized ID (DID) of an Ethereum address.

```import { getDID } from 'did-hd-wallet';```

#### Parameters

- address : string - Ethereum adress of which the DID is needed.

#### Returns

- DID: string - Ethereum DID.

---
### createRandomETHDID

Generates a random Ethereum address.

```import { createRandomETHDID } from 'did-hd-wallet';```

#### Parameters

- none

#### Returns

- ethereumAddress: string - random Ethereum address.

---
### createETHDIDFromPrivateKey
Derives an ethereum address from a private key.

```import { createETHDIDFromPrivateKey } from 'did-hd-wallet';```

#### Parameters

- privateKey : string - valid private key.

#### Returns

- ethereumAddress: string - Ethereum address corresponding to the private key.

## Wallet Class
Functions related to wallet management

```import Wallet from 'did-hd-wallet';```

---
### getMasterPrivateKey

#### Parameters

- none

#### Returns

- masterPrivateKey: string - hex encoded master private key.

---
### getMasterPublicKey
Retreives the master public key related to the master key of the wallet.
#### Parameters
- none

##### Returns
- masterPublicKey: string - hex encoded master public key.

---
### getMasterChainCode
Retreives the chaincode related to the master key of the wallet.
#### Parameters
- none

#### Returns
- masterChainCode: string - hex encoded master chain code.

---
### getMasterMnemonic
Retreives the mnemonic related to the master key of the wallet.
#### Parameters
- none

#### Returns
- masterMnemonic: string - master mnemonic phrase.

---
### getChildKeys
Retreives the child key details for a given derivation path.
#### Parameters
- path: string - valid derivation path.

#### Returns
- childKeys: object - JS object containing child private key, child public key, child chain code, base58 representation of child node, WIF representation of child node, Ethereum address and ETH DID .

---
### getMasterKeys
Retreives the master key details of the wallet.
#### Parameters
- none

#### Returns
- childKeys: object - JS object containing master private key, master public key, master chain code, base58 representation of master node, WIF representation of master node, Ethereum master Ethereum address and master ETH DID..