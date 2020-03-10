# Websocket Feed

The TokenAnalyst websocket feed provides real-time bitcoin inflows and outflows to/from exchanges that we have labelled. We have three channels you can subscribe to:

- `btc_confirmed_exchange_flows`: This is the primary channel that we support in production and it shows transactions as soon as they are included in a block on the blockchain by a miner.
- `btc_unconfirmed_exchange_flows`: This is a much more experimental channel that shows a stream of unconfirmed transactions that are in the Bitcoin memory pool of our nodes. This particular stream is highly experimental and is in a _beta_ stage right now.
- `btc_confirmed_value_flows`: This is a channel that contains all of the value flows within every transaction (without any filtering) as soon as they are included in a block on the blockchain by a miner.

You can find a sample python script to subscribe to these feeds here - <a href="https://github.com/tokenanalyst/samplecode" target="_blank">https://github.com/tokenanalyst/samplecode</a>

Here are the exchanges we support in the Bitcoin WebSocket: `Binance`, `BitMEX`, `Bitfinex`, `Bittrex`, `Deribit`, `Huobi`, `Kraken`, `OKex`, and `Poloniex`.

<img src="https://img.shields.io/badge/Tier-Enterprise-blueviolet.svg"/>

## Connection Details
### URL

`wss://ws.tokenanalyst.io`

### Request process

Websocket connections go through the following lifecycle:

- Establish a websocket connection with: 

`wss://ws.tokenanalyst.io:8000`

- Receive heartbeat (every 30 seconds): 

 `{"id":null,"event":"heartbeat","data":{"serverTime":1570014312199}}`
 
- Authenticate and subscribe to a channel with: 

`{"event":"subscribe","channel":"btc_confirmed_exchange_flows","id":"test-id","key":"<insert_api_key_here>"}`

- Receive subscription response: 

`{"id":"test-id","event":"subscribed","data":{"success":true,"errorCode":null,"message":"Subscribed to channel btc_confirmed_exchange_flows"}}`

- Receive data: 

`{"id":"test-id","event":"data","data":{"blockNumber":597542,"blockHash":"0000000000000000000581292750484f48e85bc2de54c2658a4a774da2095880","transactionId":"67bd2bc0652ae1a999cd5c60a879c5c15f5cb7178aa00b97875bb6fe8debff2d","timestamp":1570019590,"from":["1Bf5e5iUDbKL1c4wqom1Us6zszSokXY4Bd","1Bf5e5iUDbKL1c4wqom1Us6zszSokXY4Bd","1Bf5e5iUDbKL1c4wqom1Us6zszSokXY4Bd","1Bf5e5iUDbKL1c4wqom1Us6zszSokXY4Bd"],"to":["Huobi"],"value":0.2018245,"flowType":"Inflow"}}`

- Unsubscribe: 

`{"event":"unsubscribe","channel":"btc_confirmed_exchange_flows","id":"test-id"}`

- Receive unsubscription response: 

`{"id":"test-id","event":"unsubscribed","data":{"success":true,"errorCode":null,"message":"Unsubscribed from channel btc_confirmed_exchange_flows"}}`

### Request Parameters

| Field   | Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| event   | _string_ | `subscribe` or `unsubscribe`                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| channel | _string_ | The channel you want to subscribe to. Currently we only support 1) `btc_confirmed_exchange_flows`, which has all BTC transactions going into, out of, and in-between exchanges on-chain 2) `btc_unconfirmed_exchange_flows` which has all BTC transactions going into, out of, and in-between exchanges on-chain straight from the Bitcoin memory pool (unconfirmed transactions) and 3) `btc_confirmed_value_flows` which has all value flows on-chain (with no filtering) |
| id      | _string_ | An arbitrary id that you can specify to identify the data from the specific subscription                                                                                                                                                                                                                                                                                                                                                                                    |
| key     | _string_ | Your unique TokenAnalyst API key                                                                                                                                                                                                                                                                                                                                                                                                                                            |

## Channels

| Name                           | Description                                                                                                                                                                                    |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| btc_confirmed_exchange_flows   | This channel has all BTC transactions going into, out of, and in-between exchanges on-chain, if the transaction is mined in one block.                                                         |
| btc_unconfirmed_exchange_flows | This channel has unconfirmed BTC transactions going into, out of, and in-between exchanges on-chain straight from the Bitcoin memory pool (_beta_)                                             |
| btc_confirmed_value_flows      | This channel has all BTC value flows within every transaction for any transaction that is mined in a block. For every every output in a transaction, there is a value flow that is recorded. |

<aside class="notice">
We currently support and return 4 types of events - <code>subscribe</code>, <code>unsubscribe</code>, <code>error</code>, and <code>data</code>. Below are overviews of the types of responses you will get from each event type.
</aside>

## Error Responses

### Subscribe/Unsubscribe/Error Event Response Overview

| Field     | Type     | Description                                                                              |
| --------- | -------- | ---------------------------------------------------------------------------------------- |
| success   | _string_ | `true` or `false`                                                                        |
| errorCode | _string_ | The error code if an error occurred. Error codes detailed below.                         |
| message   | _string_ | Human readable message confirming what event has occurred (successful subscription etc.) |

### Error Codes

| Code | Human Readable Response                            | Description                                              |
| ---- | -------------------------------------------------- | -------------------------------------------------------- |
| 1    | "An unknown error occured."                        | General error code if something went wrong               |
| 2    | "Could not read request, please send proper JSON." | When your request is malformed JSON                      |
| 3    | "You need to provide a valid API key."             | When your API key is not valid                           |
| 4    | "Channel \$name does not exist."                   | When the channel you've subscribed to doesn't exist      |
| 5    | "Not subscribed to channel \$name."                | When you are not subscribed to the channel you specified |
| 6    | "The field \$field is missing in the request"      | When one of the required request parameters are missing. |


## BTC Confirmed Exchange Flows Data Response Overview

> Subscribing to the `btc_confirmed_exchange_flows` channel returns JSON structured like this:

```json
{
  "id": "test-id",
  "event": "data",
  "data": {
    "blockNumber": 595307,
    "blockHash": "000000000000000000165c78...c5295608cd2ec5bf1a7c34",
    "transactionId": "eb98ab622365d63daf6...25932b1d8bbd1725db647",
    "timestamp": 1568735726,
    "from": ["1JBRJFRBDEgNEiXkgRR7cGyi7c1W3r1NPd"],
    "to": ["Bitmex"],
    "value": 0.00026469,
    "flowType": "Inflow"
  }
}
```


| Field         | Type       | Description                                                                                                                                                  |
| ------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| blockNumber   | _integer_  | The block number where this transaction occurred                                                                                                             |
| blockHash     | _string_   | The hash of the block where this transaction occurred                                                                                                        |
| transactionId | _string_   | The id of the transaction in question                                                                                                                        |
| timestamp     | _integer_  | Unix timestamp of the transaction in question                                                                                                                |
| from          | [_string_] | A list of sending public key hashes (if inflow) or exchange names (if outflow)                                                                                 |
| to            | [_string_] | A list of receiving public key hashes (if outflow) or exchange names (if inflow)                                                                             |
| value         | _decimal_  | The total amount of BTC sent in the transaction                                                                                                              |
| flowType      | _string_   | One of either `Inflow`, `Outflow`, or `InterFlow` (if funds flow between different exchanges) `IntraFlow` (if funds flow within the same exchange's wallets) |

## BTC Unconfirmed Exchange Flows (Mempool) Data Response Overview

> Subscribing to the `btc_unconfirmed_exchange_flows` (Mempool) channel returns JSON structured like this:

```json
{
  "id": "test-id",
  "event": "data",
  "data": {
    "blockNumber": 600372,
    "probability": 1.0,
    "transactionHash": "c3960dda32e862001c963a...0724bc72502b3e14bfc",
    "seen": 1571665338,
    "feerate": 4.0153846153846547e-7,
    "from": ["1KnBtxSH4sNdMXz2gQ3vYuH9iAaPafxwTT"],
    "to": ["Binance"],
    "value": 0.01737219,
    "flowType": "Inflow"
  }
}
```

| Field         | Type       | Description                                                                                                                                                  |
| ------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| blockNumber   | _integer_  | The predicted block number in which this transaction will be mined                                                                                           |
| transactionId | _string_   | The id of the transaction in question                                                                                                                        |
| probability   | _string_   | Placeholder field, will be removed soon                                                                                                                      |
| seen          | _integer_  | Unix timestamp when this transaction was seen in the Memory Pool                                                                                             |
| from          | [_string_] | A list of sending public key hashes (if infow) or exchange names (if outfow)                                                                                 |
| to            | [_string_] | A list of receiving public key hashes (if outflow) or exchange names (if inflow)                                                                             |
| value         | _decimal_  | The total amount of BTC sent in the transaction                                                                                                              |
| flowType      | _string_   | One of either `Inflow`, `Outflow`, or `InterFlow` (if funds flow between different exchanges) `IntraFlow` (if funds flow within the same exchange's wallets) |

## BTC Confirmed Value Flows Data Response Overview

> Subscribing to the `btc_confirmed_value_flows` (all flows) channel returns JSON structured like this:

```json
{
  "id": "test-id",
  "event": "data",
  "data": {
    "blockNumber": 605732,
    "blockHash": "0000000000000000000ab29452f880860cc56008cafd4bb48bc1372b62e05497",
    "transactionId": "283a02a55ab9a7f16ec9862bbb799f3e1e940d3238afdde9c287a4029017aef7",
    "timestamp": 1574935742,
    "from": [
      "1KUPay2RCy9GHiVcie1x535SVHHSgcY1bc",
      "1KUPay2RCy9GHiVcie1x535SVHHSgcY1bc",
      "1TuoU8zq3EuLxAuyCNKWQ5vJGgr7E3i3U"
    ],
    "to": ["1TuoU8zq3EuLxAuyCNKWQ5vJGgr7E3i3U"],
    "value": 0.03123805,
    "flowType": "Unclassified"
  }
}
```

| Field         | Type       | Description                                                                                                                                                  |
| ------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| blockNumber   | _integer_  | The block number where this transaction occurred                                                                                                             |
| blockHash     | _string_   | The hash of the block where this transaction occurred                                                                                                        |
| transactionId | _string_   | The id of the transaction in question                                                                                                                        |
| timestamp     | _integer_  | Unix timestamp of the transaction in question                                                                                                                |
| from          | [_string_] | A list of sending public key hashes                                                                                 |
| to            | [_string_] | A list of receiving public key hashes                                                                            |
| value         | _decimal_  | The total amount of BTC sent in the transaction                                                                                                              |
| flowType      | _string_   | Always `Unclassified` for now |
