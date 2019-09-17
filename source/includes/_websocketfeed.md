# Websocket Feed [BETA]

The TokenAnalyst websocket feed provides real-time (with 3 blocks confirmation) bitcoin inflows and outflows to/from exchanges that we have labelled.

<img src="https://img.shields.io/badge/Tier-BETA-blueviolet.svg"/>

```shell
ws://ws.tokenanalyst.io:8000
```

> Subscribing to the above URL returns JSON structured like this:

```json
[
  {
    "blockNumber": 595307,
    "blockHash": "000000000000000000165c78ea45068c6ed0308dd7c5295608cd2ec5bf1a7c34",
    "transactionId": "eb98ab622365d63daf6baf5c9f02eaf52eefcbab78d25932b1d8bbd1725db647",
    "timestamp": 1568735726,
    "from": ["1JBRJFRBDEgNEiXkgRR7cGyi7c1W3r1NPd"],
    "to": ["Bitmex"],
    "value": 0.00026469,
    "flowType": "Inflow"
  },
  {
    "blockNumber": 595307,
    "blockHash": "000000000000000000165c78ea45068c6ed0308dd7c5295608cd2ec5bf1a7c34",
    "transactionId": "5bbe6732e5d191e12b9d005968fff9a40c74ebf16dd6295b7c84128112cf2096",
    "timestamp": 1568735726,
    "from": [
      "13UfH12GBuvmACQUy54fTKx8ScsoSySK6b",
      "1HUJCVmBGFNw5229uyg8GjRztzX1krocyj"
    ],
    "to": ["Binance"],
    "value": 0.04793434,
    "flowType": "Inflow"
  }
]
```

### URL

`ws://ws.tokenanalyst.io:8000`

### WS Data Overview

| Field       | Type      | Description                                                                                                                                 |
| ----------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| blockNumber       | _integer_  | The block number where this transaction occurred                                                                                                                    |
| blockHash | _string_  | The hash of the block where this transaction occurred |
| transactionId    | _string_  | The id of the transaction in question                      |
| timestamp   | _integer_ | Unix timestamp of the transaction in question                                                  |
| from   | [_string_] | A list of sending public key hashes (if infow) or exchange names (if outfow)                                                  |
| to      | [_string_] | A list of receiving public key hashes (if outflow) or exchange names (if inflow)                                                 |
| value      | _decimal_ | The total amount of BTC sent in the transaction                                                   |
| flowType      | _string_ | One of either `Inflow`, `Outflow`, or `IntraFlow` (if funds flow within exchange wallets)                                                   |


