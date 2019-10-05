# Websocket Feed

The TokenAnalyst websocket feed provides real-time (with 0 blocks confirmation) bitcoin inflows and outflows to/from exchanges that we have labelled.

You can find a sample python script to subscribe to this feed here - <a href="https://github.com/tokenanalyst/samplecode" target="_blank">https://github.com/tokenanalyst/samplecode</a>

<img src="https://img.shields.io/badge/Tier-ALPHA-blueviolet.svg"/>

```shell
ws://ws.tokenanalyst.io:8000
```

> Subscribing to the exchange_flows channel returns JSON structured like this:

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

`wss://ws.tokenanalyst.io:8000`

### Request process
Websocket connections go through the following lifecycle:

* Establish a websocket connection with `ws://ws.tokenanalyst.io:8000`
* Receive heartbeat (every 30 seconds) - `{"id":null,"event":"heartbeat","data":{"serverTime":1570014312199}}`
* Authenticate and subscribe to a channel with `{"event":"subscribe","channel":"exchange_flows","id":"test-id","key":"<insert_api_key_here>"}`
* Receive subscription response `{"id":"test-id","event":"subscribed","data":{"success":true,"errorCode":null,"message":"Subscribed to channel exchange_flows"}}`
* Receive data `{"id":"test-id","event":"data","data":{"blockNumber":597542,"blockHash":"0000000000000000000581292750484f48e85bc2de54c2658a4a774da2095880","transactionId":"67bd2bc0652ae1a999cd5c60a879c5c15f5cb7178aa00b97875bb6fe8debff2d","timestamp":1570019590,"from":["1Bf5e5iUDbKL1c4wqom1Us6zszSokXY4Bd","1Bf5e5iUDbKL1c4wqom1Us6zszSokXY4Bd","1Bf5e5iUDbKL1c4wqom1Us6zszSokXY4Bd","1Bf5e5iUDbKL1c4wqom1Us6zszSokXY4Bd"],"to":["Huobi"],"value":0.2018245,"flowType":"Inflow"}}`
* Unsubscribe `{"event":"unsubscribe","channel":"exchange_flows","id":"test-id"}`
* Receive unsubscription response `{"id":"test-id","event":"unsubscribed","data":{"success":true,"errorCode":null,"message":"Unsubscribed from channel exchange_flows"}}`

### Request Parameters

| Field       | Type      | Description                                                                                                                                 |
| ----------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| event       | _string_  | `subscribe` or `unsubscribe`                                                                                                                    |
| channel | _string_  | The channel you want to subscribe to. Currently we only support `exchange_flows`, which has all BTC transactions going into, out of, and in-between exchanges on-chain. |
| id    | _string_  | An arbitrary id that you can specify to identify the data from the specific subscription                     |
| key   | _string_ | Your unique TokenAnalyst API key                                                  |

<aside class="notice">
We currently support and return 4 types of events - <code>subscribe</code>, <code>unsubscribe</code>, <code>error</code>, and <code>data</code>. Below are overviews of the types of responses you will get from each event type.
</aside>

### Data Response Overview

| Field       | Type      | Description                                                                                                                                 |
| ----------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| blockNumber       | _integer_  | The block number where this transaction occurred                                                                                                                    |
| blockHash | _string_  | The hash of the block where this transaction occurred |
| transactionId    | _string_  | The id of the transaction in question                      |
| timestamp   | _integer_ | Unix timestamp of the transaction in question                                                  |
| from   | [_string_] | A list of sending public key hashes (if infow) or exchange names (if outfow)                                                  |
| to      | [_string_] | A list of receiving public key hashes (if outflow) or exchange names (if inflow)                                                 |
| value      | _decimal_ | The total amount of BTC sent in the transaction                                                   |
| flowType      | _string_ | One of either `Inflow`, `Outflow`, or `InterFlow` (if funds flow between different exchanges) `IntraFlow` (if funds flow within the same exchange's wallets)                                                   |


### Subscribe/Unsubscribe/Error Event Response Overview

| Field       | Type      | Description                                                                                                                                 |
| ----------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| success       | _string_  | `true` or `false`                                                                                                                    |
| errorCode | _string_  | The error code if an error occurred. Error codes detailed below. |
| message    | _string_  | Human readable message confirming what event has occurred (successful subscription etc.)                      |


### Error Codes

| Code       | Human Readable Response      | Description                                                                                                                                 |
| ----------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | "An unknown error occured." | General error code if something went wrong                                                                                                                    |
| 2 | "Could not read request, please send proper JSON." | When your request is malformed JSON |
| 3    | "You need to provide a valid API key."  | When your API key is not valid                      |
| 4   | "Channel $name does not exist." | When the channel you've subscribed to doesn't exist                                                  |
| 5   | "Not subscribed to channel $name." | When you are not subscribed to the channel you specified                                                  |
| 6   | "The field $field is missing in the request" | When one of the required request parameters are missing.                                                  |