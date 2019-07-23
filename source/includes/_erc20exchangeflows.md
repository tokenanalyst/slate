# ERC20 Exchange Flows

ERC20 tokens we currently support are:

| Name                  | Symbol |
| --------------------- | ------ |
| Binance Coin          | `bnb`  |
| Maker                 | `mkr`  |
| Basic Attention Token | `bat`  |
| Venchain              | `ven`  |
| OmiseGo               | `omg`  |
| Augur                 | `rep`  |
| Golem                 | `gnt`  |
| ZRX                   | `zrx`  |
| Zilliqa               | `zil`  |
| Decentraland          | `mana` |
| Numerai               | `nmr`  |
| Tokencard             | `tkn`  |
| Bancor                | `bnt`  |
| Loom Network          | `loom` |
| Status                | `snt`  |
| Civic                 | `cvc`  |
| Kyber Network         | `knc`  |
| iExec RLC             | `rlc`  |
| ChainLink             | `link` |
| Ocean Protocol        | `ocean`|
| Fetch.ai.             | `fet`  |

## ERC20 Full Historical Inflow to Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_historical/last?token=omg&direction=inflow&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2017-07-19",
    "token_name": "OMG",
    "exchange": "Bitfinex",
    "inflow": 1021328.4514801201,
    "price": 0.68,
    "inflow_usd": 695260.83,
    "number_of_txns": 46,
    "avg_txn_value": 22202.79242348087,
    "avg_txn_value_usd": 15114.37
  },
  {
    "date": "2017-07-19",
    "token_name": "OMG",
    "exchange": "Bittrex",
    "inflow": 2440563.297567261,
    "price": 0.68,
    "inflow_usd": 1661393.13,
    "number_of_txns": 198,
    "avg_txn_value": 12326.077260440712,
    "avg_txn_value_usd": 8390.87
  }
]
```

This endpoint returns the inflow of ERC20 tokens into exchange wallets. The `avg_txn_value` is the average transaction value for transactions flowing into exchange wallets on a given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `omg`                                               |
| direction | _string_ | `inflow`                                            |

## ERC20 Full Historical Outflow from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_historical/last?token=omg&direction=outflow&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2017-07-30",
    "token_name": "OMG",
    "exchange": "Bittrex",
    "outflow": 83173.64737858999,
    "price": 1.23,
    "outflow_usd": 102476.86,
    "number_of_txns": 115,
    "avg_txn_value": 723.249107639913,
    "avg_txn_value_usd": 891.1
  },
  {
    "date": "2017-07-31",
    "token_name": "OMG",
    "exchange": "Bitfinex",
    "outflow": 317922.74454691994,
    "price": 1.2,
    "outflow_usd": 382302.1,
    "number_of_txns": 95,
    "avg_txn_value": 3346.555205757052,
    "avg_txn_value_usd": 4024.23
  }
]
```

This endpoint returns the outflow of ERC20 tokens from exchange wallets. The `avg_txn_value` is the average transaction value for transactions flowing out of exchange wallets on a given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `omg`                                               |
| direction | _string_ | `outflow`                                           |
