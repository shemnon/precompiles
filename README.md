# EVM Precompiled Contract Catalog

The source data is in _data/precompiles.

## File Structure

Each precompiled function has its own file with the filename starting with the
the [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md)
representation of the chain that originated the smart contract, and then the
short hex representation of that contract, and `.json` an extension.

The origin chain is the production chain that promulgated the specification,
even if a testnet chain or non-origin chain was the first to place that
precompiled function in production.

Example: [eip155-1-0x1.json](_data/precompiles/eip155-1-0x1.json)

```json
{
  "name": "ecrecover",
  "description": "ECDSA public key recovery function on the elliptic curve secp256k1",
  "address": {
    "full": "0000000000000000000000000000000000000000000000000000000000000001",
    "hex": "1",
    "decimal": "1"
  },
  "origin": {
    "chain": "eip155:1",
    "specification": "https://ethereum.github.io/yellowpaper/paper.pdf"
  },
  "networks": [
    "*"
  ],
  "languages": {
    "solidity": {
      "type": "function",
      "name": "ecrecover"
    }
  }
}
```

Each chain has a `<CAIP-2 represntation>-schedule.json` file that describes when
the precompile function activated on that chain. This format does not support
the sunsetting of a precompile function as no chain specified has removed a
precompiled function.

The field name is the decimal representation of the block number that the
precompile was activated. The value is an array of the CAIP-2/short hex filename
without the file extension.

Example:
Example: [eip155-1-schedule.json](_data/precompiles/eip155-1-schedule.json)

```json
{
  "0": [
    "eip155-1-0x1",
    "eip155-1-0x2",
    "eip155-1-0x3",
    "eip155-1-0x4"
  ],
  "4370000": [
    "eip155-1-0x5",
    "eip155-1-0x6",
    "eip155-1-0x7",
    "eip155-1-0x8"
  ],
  "9069000": [
    "eip155-1-0x9"
  ]
}
```

## Aggregation

There is no aggregation or fancy website currently. That will come in the
future.

## Collision Management

By using the CAIP-2 representation in the file name there should be no naming
collisions. It is possible that colliding chains may define separate addresses
or that a chain may provide two definitions of the same address. In the event
that chains and functions that were defined chronologically later should add an
extra classifier to their designations.
