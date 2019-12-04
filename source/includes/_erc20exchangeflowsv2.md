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
| Decentraland          | `mana` | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Numerai               | `nmr`  | `bittrex` |
| Loom Network          | `loom` | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Status                | `snt`  | `kucoin`, `poloniex` |
| Civic                 | `cvc`  | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Kyber Network         | `knc`  | `binance`, `kucoin`, `poloniex` |
| iExec RLC             | `rlc`  | `bittrex` |
| ChainLink             | `link` | `binance` |

## ERC20 Full Historical Flows Into Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=bat&exchange=binance&direction=inflow&window=1h&format=json&from_date=2019-10-04&to_date=2019-10-06&limit=2&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2019-10-06",
    "hour": "22:00:00", // not available when window 1d
    "datetime": "2019-10-06 22:00:00", // not available when window 1d
    "inflow": 2564.4029,
    "inflow_usd": 487.24,
    "number_of_txns": 4,
    "avg_txn_value": 641.1007,
    "avg_txn_value_usd": 121.81
  },
  {
    "date": "2019-10-06",
    "hour": "23:00:00", // not available when window 1d
    "datetime": "2010-10-06 23:00:00", // not available when window 1d
    "inflow": 219.5791,
    "inflow_usd": 41.72,
    "number_of_txns": 2,
    "avg_txn_value": 109.7895,
    "avg_txn_value_usd": 20.86
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
| exchange  | _string_ | An exchange from the table that we support        |
| window    | _string_ | `1h` or `1d`       |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field | Type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| date     | _string_ | The date in _YYYY-MM-DD_                                                  |
| hour *   | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                                                                                        |
| datetime *  | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`                                                                               |
| inflow  | _decimal_ | The total amount of ERC20 token that flowed into the exchange on this date. Denominated in ERC20 token.         |
| inflow_usd  | _decimal_ | The USD value of the total amount of ERC20 token that flowed into the exchange on this date         |
| number_of_txns       | _integer_ | The number of transactions sending ERC20 token into this exchange on this date.                                 |
| avg_txn_value       | _decimal_ | The average amount ERC20 token transferred per transaction into the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of ERC20 token transferred per transaction into the given exchange on this date.    |


## ERC20 Full Historical Flows Out Of Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=bat&exchange=binance&direction=outflow&window=1h&format=json&from_date=2019-10-01&to_date=2019-10-10&limit=2&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2019-10-10",
    "hour": "22:00:00", // not available when window 1d
    "datetime": "2019-10-10 22:00:00", // not available when window 1d
    "outflow": 108214.6507,
    "outflow_usd": 21642.93,
    "number_of_txns": 8,
    "avg_txn_value": 13526.8313,
    "avg_txn_value_usd": 2705.37
  },
  {
    "date": "2019-10-10",
    "hour": "23:00:00", // not available when window 1d
    "datetime": "2019-10-10 23:00:00", // not available when window 1d
    "outflow": 51502.1242,
    "outflow_usd": 10300.42,
    "number_of_txns": 4,
    "avg_txn_value": 12875.5311,
    "avg_txn_value_usd": 2575.11
  }
]
```

This endpoint returns the outflow of ERC20 token from exchange wallets. The `avg_txn_value`, `outflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC
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
| hour *   | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                                                                                        |
| datetime * | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`                                                                               |
| outflow  | _decimal_ | The total amount of ERC20 token that flowed out of the exchange on this date. Denominated in ERC20 token.         |
| outflow_usd  | _decimal_ | The USD value of the total amount of ERC20 token that flowed out of the exchange on this date         |
| number_of_txns       | _integer_ | The number of transactions sending ERC20 token out of this exchange on this date.                                 |
| avg_txn_value       | _decimal_ | The average amount ERC20 token transferred per transaction out of the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of ERC20 token transferred per transaction out of the given exchange on this date.    |



## ERC20 Full Historical Static Flows to Exchanges

<img src="https://img.shields.io/badge/Tier-Enterprise-blueviolet.svg"/>

This endpoint returns _static_ flows of ERC20 into exchange wallets for as far back as we track. What do we mean by static? while our standard API endpoint as seen <a href="https://docs.tokenanalyst.io/#erc20-full-historical-flows-into-exchanges-beta" target="_blank">above</a> dynamically updates the data (up to 7 days prior to the current day) when we find new information on exchange wallets, the historical data from this endpoint _never_ changes from the time it is posted. The rationale for this is to serve a snapshot look of what was known at the specific point in time - to aid in effective backtesting and inputs for ML models. This is suited for users who want to use our websocket. 

For this reason, as an extra reinforcement, this endpoint includes the `last_updated` field to show the time in UTC when the data point was last modified. 

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_static/last?format=json&exchange=binance&token=bat&direction=inflow&window=1h&lag=hour&limit=2&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2019-11-16",
    "hour": "15:00:00", // not available when window 1d
    "datetime": "2019-11-16 15:00:00", // not available when window 1d
    "inflow": 532.8873, // not available when direction outflow
    "inflow_usd": 97338.28, // not available when direction outflow
    "number_of_txns": 202,
    "avg_txn_value": 2.6381,
    "avg_txn_value_usd": 481.87,
    "last_updated": "2019-11-17 16:00:18"
  },
  {
    "date": "2019-11-16",
    "hour": "16:00:00", // not available when window 1d
    "datetime": "2019-11-16 16:00:00", // not available when window 1d
    "inflow": 921.5056, // not available when direction outflow
    "inflow_usd": 168488.38, // not available when direction outflow
    "number_of_txns": 232,
    "avg_txn_value": 3.972,
    "avg_txn_value_usd": 726.24,
    "last_updated": "2019-11-17 17:01:24",
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_static/last?`

### URL Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `bat`                                                                                     |
| direction    | _string_  | `inflow` or `outflow`                                                                     |
| exchange     | _string_  | An exchange from the table that we support                                                |
| lag          | _string_  | `hour`,`day`, or `week`. Lags the returned data by the specified parameter               |
| window       | _string_  | `1h`                                                                             |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                                 | Type      | Description                                                                                                                                                                                                               |
| ------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value                         | _decimal_ | The average amount ERC20 token transferred per transaction into the given exchange on this date.                                                                                                                                  |
| avg_txn_value_usd                     | _decimal_ | The USD value of the average amount of ERC20 token transferred per transaction into the given exchange on this date.                                                                                                              |
| date                                  | _string_  | The date in _YYYY-MM-DD_                                                                                                                                                                                                  |
| datetime *                             | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`                                                                               |
| hour *                                 | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                                                                                        |
| inflow                                | _decimal_ | The total amount of ERC20 token that flowed into the exchange on this date. Denominated in ERC20 token.                                                                                                                                     |
| inflow_usd                            | _decimal_ | The USD value of the total amount of ERC20 token that flowed into the exchange on this date                                                                                                                                       |
| number_of_txns                        | _integer_ | The number of transactions sending ERC20 token into this exchange on this date.                                                                                                                                                   |
| last_updated                          | _string_  | The date when the endpoint was last updated in `UTC` datetime format
