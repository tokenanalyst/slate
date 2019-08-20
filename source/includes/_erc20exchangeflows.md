# ERC20 Exchange Flows

ERC20 tokens we currently support are:

| Name                  | Symbol |
| --------------------- | ------ |
| Maker                 | `mkr`  |
| Basic Attention Token | `bat`  |
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
| Fetch.ai.             | `fet`  |




## ERC20 Full Historical Inflow to Exchanges (with 1 hour granularity)

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_window_historical/last?token=omg&direction=inflow&window=1h&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2017-07-19",
    "hour": "11:00:00",
    "token_name": "OMG",
    "exchange": "Bitfinex",
    "inflow": 1021328.4514801201,
    "price_usd": 0.68,
    "inflow_usd": 695260.83,
    "number_of_txns": 46,
    "avg_txn_value": 22202.79242348087,
    "avg_txn_value_usd": 15114.37
  },
  {
    "date": "2017-07-19",
    "hour": "12:00:00",
    "token_name": "OMG",
    "exchange": "Bittrex",
    "inflow": 2440563.297567261,
    "price_usd": 0.68,
    "inflow_usd": 1661393.13,
    "number_of_txns": 198,
    "avg_txn_value": 12326.077260440712,
    "avg_txn_value_usd": 8390.87
  }
]
```

This endpoint returns the inflow of ERC20 into exchange wallets. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `omg`                                               |
| direction | _string_ | `inflow`                                            |
| window    | _string_ | `1h` or `1d`                                        |

### Data Overview

| Field | Type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| date     | _string_ | The date in _YYYY-MM-DD_                                                  |
| hour     | _string_ | The hour of the day in _HH:MM:SS_  (UTC time zone). This is an optional field based on the params used.                                               |
| token_name  | _string_ | The name of the token in question         |
| exchange  | _string_ | The name of the exchange in question         |
| inflow  | _decimal_ | The total amount of the token that flowed into the exchange on this date. Denominated in the token in question.         |
| price_usd | _decimal_ | The daily average price of the token in USD (the daily mean of minute-level price data) |
| inflow_usd  | _decimal_ | The USD value of the total amount of the token that flowed into the exchange on this date         |
| number_of_txns       | _integer_ | The number of transactions sending the token into this exchange on this date.                                 |
| avg_txn_value       | _decimal_ | The average amount of tokens transferred per transaction into the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of tokens transferred per transaction into the given exchange on this date.    |


## ERC20 Full Historical Outflow from Exchanges (with 1 hour granularity)

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_window_historical/last?token=omg&direction=outflow&window=1h&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2017-07-19",
    "hour": "11:00:00",
    "token_name": "OMG",
    "exchange": "Bitfinex",
    "outflow": 1021328.4514801201,
    "price_usd": 0.68,
    "outflow_usd": 695260.83,
    "number_of_txns": 46,
    "avg_txn_value": 22202.79242348087,
    "avg_txn_value_usd": 15114.37
  },
  {
    "date": "2017-07-19",
    "hour": "12:00:00",
    "token_name": "OMG",
    "exchange": "Bittrex",
    "outflow": 2440563.297567261,
    "price_usd": 0.68,
    "outflow_usd": 1661393.13,
    "number_of_txns": 198,
    "avg_txn_value": 12326.077260440712,
    "avg_txn_value_usd": 8390.87
  }
]
```

This endpoint returns the outflow of ERC20 from exchange wallets. The `avg_txn_value`, `outflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `omg`                                               |
| direction | _string_ | `outflow`                                           |
| window    | _string_ | `1h` or `1d`                                        |

### Data Overview

| Field | Type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| date     | _string_ | The date in _YYYY-MM-DD_                                                  |
| hour     | _string_ | The hour of the day in _HH:MM:SS_  (UTC time zone). This is an optional field based on the params used.                                               |
| token_name  | _string_ | The name of the token in question         |
| exchange  | _string_ | The name of the exchange in question         |
| outflow  | _decimal_ | The total amount of the token that flowed out of the exchange on this date. Denominated in the token in question.         |
| price_usd | _decimal_ | The daily average price of the token in USD (the daily mean of minute-level price data) |
| outflow_usd  | _decimal_ | The USD value of the total amount of the token that flowed out of the exchange on this date         |
| number_of_txns       | _integer_ | The number of transactions sending the token out of this exchange on this date.                                 |
| avg_txn_value       | _decimal_ | The average amount of tokens transferred per transaction out of the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of tokens transferred per transaction out of the given exchange on this date.    |