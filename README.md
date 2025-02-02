# VNS.js V2

## Overview of the API

### Setup

```
import { getEnsAddress, VNS } from '@vnsdomains/vnsjs'
import { ethers } from 'ethers'


const provider = new ethers.providers.JsonRpcProvider(
    "https://evmexplorer.velas.com/rpc",
    {
        chainId: 106,
        name: "Velas"
    }
)

const vns = new VNS({ 
    provider,
    vnsAddress: getEnsAddress('106') 
})

console.log(await vns.name('test.vlx').getAddress())
console.log(await vns.getName('0x8483fb78af59fbd15fd431d001f13844740ce6bc'))
```

### exports

```
default - VNS
getEnsAddress
getResolverContract
getVNSContract
namehash
labelhash
```

### VNS Interface

```
name(name: String) => Name
```

Returns a Name Object, that allows you to make record queries.

```
resolver(address: EthereumAddress) => Resolver
```

Returns a Resolver Object, allowing you to query names from this specific resolver. Most useful when querying a different resolver that is different than is currently recorded on the registry. E.g. migrating to a new resolver

```
async getName(address: EthereumAddress) => Promise<Name>
```

Returns the reverse record for a particular Ethereum address.

```
async setReverseRecord(name: Name) => Promise<EthersTxObject>
```

Sets the reverse record for the current Ethereum address

### Name Interface

```ts
async getOwner() => Promise<EthereumAddress>
```

Returns the owner/controller for the current VNS name.

```ts
async setOwner(address: EthereumAddress) => Promise<Ethers>
```

Sets the owner/controller for the current VNS name.

```ts
async getResolver() => Promise<EthereumAddress>
```

Returns the resolver for the current VNS name.

```ts
async setResolver(address: EthereumAddress) => Promise<EthereumAddress>
```

Sets the resolver for the current VNS name.

```ts
async getTTL() => Promise<Number>
```

Returns the TTL for the current VNS name.

```ts
async getAddress(coinId: String) => Promise<EthereumAddress>
```

Returns the address for the current VNS name for the coinId provided.

```ts
async setAddress(coinId: String, address: EthereumAddress) => Promise<EthersTxObject>
```

Sets the address for the current VNS name for the coinId provided.

```ts
async getContent() => Promise<ContentHash>
```

Returns the contentHash for the current VNS name.

```ts
async setContenthash(content: ContentHash) => Promise<EthersTxObject>
```

Sets the contentHash for the current VNS name.

```ts
async getText(key: String) => Promise<String>
```

Returns the text record for a given key for the current VNS name.

```ts
async setText(key: String, recordValue: String) => Promise<EthersTxObject>
```

Sets the text record for a given key for the current VNS name.

```ts
async setSubnodeOwner(label: String, newOwner: EthereumAddress) => Promise<EthersTxObject>
```

Sets the subnode owner for a subdomain of the current VNS name.

```ts
async setSubnodeRecord(label: String, newOwner: EthereumAddress, resolver: EthereumAddress, ttl: ?Number) => Promise<EthersTxObject>
```

Sets the subnode owner, resolver, ttl for a subdomain of the current VNS name in one transaction.

```ts
 async createSubdomain(label: String) => Promise<EthersTxObject>
```

Creates a subdomain for the current VNS name. Automatically sets the owner to the signing account.

```ts
async deleteSubdomain(label: String) => Promise<EthersTxObject>
```

Deletes a subdomain for the current VNS name. Automatically sets the owner to "0x0..."

## Resolver Interface

```ts
address
```

Static property that returns current resolver address

```ts
name(name) => Name
```

Returns a Name Object that hardcodes the resolver
