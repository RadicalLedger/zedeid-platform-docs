# zedeid-did-siop-lib

## Overview ##
This implements _Self Issued OpenId Connect Provider (SIOP)_ for _Decentralized Identities (DIDs)_. The library contains two components, **RP (Relying Party)** and **Provider**. Provider is intended to be used inside any piece of software which will provide DID SIOP authentication and RP can be used by relying parties (client apps) to utilize DID SIOP authentication. This library can be used in both client-side (browser) and server-side (Node.js) enviornments.

Following are the primary specifications followed by this implementation.
* [OpenID Connect Core 1.0 incorporating errata set 1](https://openid.net/specs/openid-connect-core-1_0.html#SelfIssued)
* [Self-Issued OpenID Connect Provider DID Profile](https://identity.foundation/did-siop/)

Additionally this library can be used in authentication code flow 

## Usage (Implicit flow) ##
### RP ###

````js
import {RP} from "zedeid-did-siop-lib"

//create a RP instance
const relyingParty = new RP(redirect_uri,did,kid,privateKey);

//before calling any other methods initialise the object (async method)
await relyingParty.init();

//generate the request
const request = await relyingParty.generateRequest();

//send the request to a provider and receive the response
//response - {response_type:'id_token', id_token: 'value':}

//validate a response token from the provider
const decodedResponse = await relyingParty.validateResponse(response.id_token);
console.log(decodedResponse) //{success: boolean, data: decodedResponse}

````
### Provider ###
```js
import {SIOProvider} from "zedeid-did-siop-lib";


//create a Provider instance
const provider = new SIOProvider(did, kid, privateKey);

//before calling any other methods initialise the object (async method)
await provider.init();

//validate the request from RP
const decodedRequest = await provider.validateRequest(request);

//generate response to the previously sent request by the RP
const res = await provider.generateResponse(decodedRequest, request, [expiresIn]);
console.log(res) //{response_type:'id_token', id_token: 'id_token_value'}             
```

## Usage (Authorization code flow) ##

### RP ###

````js
import {RP} from "zedeid-did-siop-lib"

//create a RP instance
const relyingParty = new RP(redirect_uri,did,kid,privateKey);

//before calling any other methods initialise the object (async method)
await relyingParty.init();

//generate the first request
const request = await relyingParty.generateRequest({response_type:'code'}, {response_type:'code'});

//send the request to a provider and receive the response
//response - {response_type:'code', code:code_value}

//generate the second request using the first response
const secondRequest = await relyingParty.generateRequest({response_type:'id_token', grant_type:'authorization_code', code: 'code_received_above'}, {response_type:'code'});
//send the request to a provider and receive the response            
//response - {response_type:'id_token', id_token:idToken, refresh_token: refreshToken}

//generate a token refresh request
const tokenRefreshReq = relyingParty.generateTokenRefreshRequest(id_token, refresh_token);

//validate a response token from the provider
const decodedResponse = await relyingParty.validateResponse(response.id_token);
console.log(decodedResponse) //{success: boolean, data: decodedResponse}

````

### Provider ###

```js
import {SIOProvider} from "zedeid-did-siop-lib"

//create a Provider instance
const provider = new SIOProvider(did, kid, privateKey);

//before calling any other methods initialise the object (async method)
await provider.init();
```


 if the environment is not a browser; set a storage with the interface of [Window.localstorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)  for getting and setting items.
 (ex: react-native : react-native-async-storage)
````js
provider.setStorage(new StorageAdapter());
````


```js
// firstRequest received from a RP
const decodedRequest = await provider.validateRequest(firstRequest);
const firstResponse = await provider.generateResponse(decodedRequest, firstRequest);
//response - {response_type:'code', code:code_value}

//send the response to redirect_uri and receive second request

const decodedRequestSecond = await provider.validateRequest(secondRequest);           
const secondResponse = await provider.generateResponse(decodedRequestSecond, secondRequest);            
//response - {response_type:'id_token', id_token:idToken, refresh_token: refreshToken}

//refresh a token
const decodedTokenRefreshReq = await provider.validateRequest(tokenRefreshReq);           
const response = await provider.generateResponse(decodedTokenRefreshReq, tokenRefreshReq);            
//response - {response_type:'id_token', id_token:idToken, refresh_token: refreshToken}

            
```

