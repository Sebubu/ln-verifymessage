# ln-verifymessage-js

A simple library to derive Lightning Network node public keys from signed messages.

### Install

```bash
npm i ln-verifymessage-js
```

### Usage

#### Derive nodeId from signature and message.


```ts
import { deriveNodeId } from "ln-verifymessage-js";

const messageThatHasBeenSigned = "ln-verifymessage-js";
const zbaseSignature = "rynmoqhhadjsttaracxgo9nhkoioi6peib8k18dekrih4hxpp36zcbgc6ntyrggc11uhjcb9prcx5py6qo16bk89i458r4n51ghggnxc";

const derivedNodeId = deriveNodeId(zbaseSignature, messageThatHasBeenSigned);
console.log("Message has been signed by", derivedNodeId);
```

Be aware: `deriveNodeId` does not check if the message has been signed by this specific signature.


#### Check if the signature and message has been signed by a specific node

```ts
const expectedNodeId = "02ac77f9f7397a64861b573c9e8b8652ce2e67a05150fd166831e9fc167670dfd8";
if (derivedNodeId !== expectedNodeId) {
    throw new Error("Signature does not match expected nodeId");
}

```


### Sign message

Node operators can sign message with (Ride the Lightning)[https://github.com/Ride-The-Lightning/RTL] and (Thunderhub)[https://thunderhub.io/].

If a user has access to a terminal messages can be signed directly with the cli's.

```bash
# LND
lncli signmessage --msg MyMessageToSign

# cLightning
lightning-cli signmessage MyMessageToSign
```