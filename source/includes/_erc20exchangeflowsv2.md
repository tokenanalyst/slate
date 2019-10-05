# ERC20 Exchange Flows

ERC20 tokens we currently support are:

| Name                  | Symbol | Supported exchanges |
| --------------------- | ------ | ------------------- |
| Maker                 | `mkr`  | `bittrex`, `kucoin` |
| Basic Attention Token | `bat`  | `binance`, `bittrex`, `poloniex` |
| OmiseGo               | `omg`  | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Augur                 | `rep`  | `binance`, `bittrex`, `kraken`, `poloniex` |
| Golem                 | `gnt`  | `binance`, `bittrex`, `poloniex` |
| ZRX                   | `zrx`  | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Zilliqa               | `zil`  | `binance`, `bittrex`, `kucoin` |
| Decentraland          | `mana` | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Numerai               | `nmr`  | `bittrex` |
| Loom Network          | `loom` | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Status                | `snt`  | `kucoin`, `poloniex` |
| Civic                 | `cvc`  | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Kyber Network         | `knc`  | `binance`, `kucoin`, `poloniex` |
| iExec RLC             | `rlc`  | `bittrex` |
| ChainLink             | `link` | `binance` |

## ERC20 Full Historical Flows Into Exchanges [Beta]

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=bat&exchange=binance&direction=inflow&window=1h&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2016-03-17",
    "hour": "11:00:00", // not available when window 1d
    "datetime": "2016-03-17 11:00:00", // not available when window 1d
    "inflow": 1.8164,
    "inflow_usd": 21.14,
    "number_of_txns": 8,
    "avg_txn_value": 0.22705,
    "avg_txn_value_usd": 2.64
  },
  {
    "date": "2016-03-18",
    "hour": "12:00:00", // not available when window 1d
    "datetime": "2016-03-18 12:00:00", // not available when window 1d
    "inflow": 3.7594499999999997,
    "inflow_usd": 38.38,
    "number_of_txns": 5,
    "avg_txn_value": 0.75189,
    "avg_txn_value_usd": 7.68
  }
]
```

This endpoint returns the inflow of ERC20 tokens into exchange wallets. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC 

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_window_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `bat`                                               |
| direction | _string_ | `inflow`                                            |
| exchange  | _string_ | An exchange from the list of ones we support        |
| window    | _string_ | `1h` or `1d`       |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field | Type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| date     | _string_ | The date in _YYYY-MM-DD_                                                  |
| hour *   | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field field and appears when window is `1h`                                                                                                        |
| datetime *  | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h`                                                                               |
| inflow  | _decimal_ | The total amount of ETH that flowed into the exchange on this date. Denominated in ETH.         |
| inflow_usd  | _decimal_ | The USD value of the total amount of ETH that flowed into the exchange on this date         |
| number_of_txns       | _integer_ | The number of transactions sending ETH into this exchange on this date.                                 |
| avg_txn_value       | _decimal_ | The average amount ETH transferred per transaction into the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of ETH transferred per transaction into the given exchange on this date.    |


## ERC20 Full Historical Flows Out Of Exchanges [Beta]

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=bat&exchange=binance&direction=outflow&window=1h&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2016-03-17",
    "hour": "11:00:00", // not available when window 1d
    "datetime": "2016-03-17 11:00:00", // not available when window 1d
    "outflow": 1.8164,
    "outflow_usd": 21.14,
    "number_of_txns": 8,
    "avg_txn_value": 0.22705,
    "avg_txn_value_usd": 2.64
  },
  {
    "date": "2016-03-18",
    "hour": "12:00:00", // not available when window 1d
    "datetime": "2016-03-18 12:00:00", // not available when window 1d
    "outflow": 3.7594499999999997,
    "outflow_usd": 38.38,
    "number_of_txns": 5,
    "avg_txn_value": 0.75189,
    "avg_txn_value_usd": 7.68
  }
]
```

This endpoint returns the outflow of ETH from exchange wallets. The `avg_txn_value`, `outflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC
### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_window_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `bat`                                               |
| direction | _string_ | `outflow`                                            |
| exchange  | _string_ | An exchange from the list of ones we support        |
| window    | _string_ | `1h` or `1d`       |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field | Type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| date     | _string_ | The date in _YYYY-MM-DD_                                                  |
| hour *   | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field field and appears when window is `1h`                                                                                                        |
| datetime * | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h`                                                                               |
| outflow  | _decimal_ | The total amount of ETH that flowed out of the exchange on this date. Denominated in ETH.         |
| outflow_usd  | _decimal_ | The USD value of the total amount of ETH that flowed out of the exchange on this date         |
| number_of_txns       | _integer_ | The number of transactions sending ETH out of this exchange on this date.                                 |
| avg_txn_value       | _decimal_ | The average amount ETH transferred per transaction out of the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of ETH transferred per transaction out of the given exchange on this date.    |