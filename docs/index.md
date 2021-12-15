
# ZeDeId Platform Documentation

## What is ZeDeId?
ZeDeId is a collection of tools to provide better privacy for online users. ZeDeId provide necessary tools for users to create identities truly own by them. For this purpose, Identities are created anchoring to Decentralsied Ledgers (Blockchains) and follow the specifications of Decentrlised Identities (DIDs) by [Identity Foundation](http://identity.foundation/).

## Main Modules
 - Identity Management
 - SIOP Authentication
 - Verifiable Credentials

## Libraries
- **[zedeid-did-siop-lib](zedeid-did-siop-lib)**

Self Issued OpenIDConnect Provider with Decentralised Identities. This library implements all necessary function to authenticate users with DID SIOP. Could be used in both Node and Browser environments 
- **[zedeid-vcsd-lib](zedeid-vcsd-lib)**

Verifiable Credentials with Selective Disclosure. Utility library to generate, present and verify Verifiable Credentials. Furhter implements functions to selectively disclose attributes of VCs. 
- **[zedeid-hdk-wallet](zedeid-hdk-wallet)**

Identitiy Wallet with Hierarchichally Deterministic Keys (HD Keys). Wrapper around functionalities to generate and manage HD Keys
