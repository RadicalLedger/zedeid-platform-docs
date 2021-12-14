# zedeid-vcsd-lib

Package for issue, present and verify selectively disclossable verifiable credentials.

## Availability
- For Node.js via [npm](https://www.npmjs.com/package/@zedeid-sdk/sd-vc-lib)
- For Browser via [jsdelivr](https://cdn.jsdelivr.net/npm/@zedeid-sdk/sd-vc-lib/dist/browser/zedeid-vcsd.js)

## Installation

1. Clone repository
2. run *npm run build* 
3. npm install < local repository directory >

## Usage
---
### issue
Issue selectively disclosable credentials for given claims.

```import { issue } from 'sd-vc-lib';```

#### Parameters
- claims : Claims - list of key value pairs.
- signerPrivateKey : string - hex encoded private key(Ethereum)
- holderPublicKey : string - hex encoded public key(Ethereum)

#### Returns
- verifiableCredential: VC - signed selectively disclosable verifiable credential.

---
### present
Present given list of verifiable credentials.

```import { present } from 'sd-vc-lib';```

#### Parameters
- credentials : VC[] - list of verifiable credentials.
- masks : Mask[] - list of masks.
- holderPrivateKey : string - hex encoded private key(Ethereum)

#### Returns
- verifiablePresentation: VP - presentation of set of selectively disclosed verifiable credentials.

---
### verify
Verify authenticity and validity of a verifiable presentaion.
```import { verify } from 'sd-vc-lib';```

#### Parameters

- vp : VP - valid mnemonic phrase.
- signerPublicKeys : string[] - set of hex encoded public keys(Ethereum)
- holderPublicKey : string - hex encoded public key(Ethereum)

#### Returns
- verified: Promise< boolean > - resolve to true if valid.

---
### verifyVC
Verify authenticity and validity of a verifiable credential.
```import { verifyVC } from 'sd-vc-lib';```

#### Parameters
- vc : VC - verifiable credential.
- signerPublicKey : string - hex encoded public key(Ethereum).
- holderPublicKey : string - hex encoded public key(Ethereum).

#### Returns
- verified: Promise< boolean > - resolve to true if verifiable credential is valid.