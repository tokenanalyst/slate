# Stablecoin Exchange Flows

The stablecoins we currently support are:

| Name                 | Symbol       | Supported Exchanges     |
| -------------------- | ------------ | ------------ |
| Tether (Omni)        | `usdt_omni`  | `bitfinex`, `kraken`, `huobi`, `okex`, `poloniex` |
| Tether (ERC20)       | `usdt_erc20` | `binance`, `bitfinex`, `bittrex`, `kucoin`, `poloniex` |
| USDC                 | `usdc`       | `binance`, `bitfinex`|
| Paxos Standard Token | `pax`        | `binance`, `bitfinex`, `bittrex` |
| TrueUSD              | `tusd`       | `binance`, `bittrex` |
| Dai                  | `dai`        | `bittrex` |

## Stablecoins Full Historical Inflow from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?format=json&window=1h&token=usdt_omni&exchange=kraken&direction=inflow&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-10-24",
    "hour": "15:00:00", // not available when window 1d
    "datetime": "2019-10-24 15:00:00", // not available when window 1d
    "avg_txn_value": 0,
    "avg_txn_value_usd": 0,
    "inflow": 0,
    "inflow_usd": 0,
    "number_of_txns": 0
  },
  {
    "date": "2019-10-24",
    "hour": "16:00:00", // not available when window 1d
    "datetime": "2019-10-24 16:00:00", // not available when window 1d
    "avg_txn_value": 2701.218,
    "avg_txn_value_usd": 2702.59,
    "inflow": 8103.6541,
    "inflow_usd": 8107.77,
    "number_of_txns": 3
  }
]
```

This endpoint returns the inflow of stablecoins into exchange wallets. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| exchange  | _string_ | An exchange from the [table](#stablecoin-exchange-flows) that we support        |
| direction | _string_ | `inflow`                                            |
| window    | _string_ | `1h` or `1d`                                        |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field             | Type      | Description                                                                                                                |
| ----------------- | --------- | -------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                   |
| hour              | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field that only appears if the `window=1h` is used. |
| inflow            | _decimal_ | The total amount of the token that flowed into the exchange on this date. Denominated in the token in question.            |
| inflow_usd        | _decimal_ | The USD value of the total amount of the token that flowed into the exchange on this date                                  |
| number_of_txns    | _integer_ | The number of transactions sending the token into this exchange on this date.                                              |
| avg_txn_value     | _decimal_ | The average amount of tokens transferred per transaction into the given exchange on this date.                             |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of tokens transferred per transaction into the given exchange on this date.            |


## Stablecoins Full Historical Outflow from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?format=json&window=1h&token=usdt_omni&exchange=huobi&direction=outflow&limit=2&API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-10-24",
    "hour": "15:00:00", // not available when window 1d
    "datetime": "2019-10-24 15:00:00", // not available when window 1d
    "outflow": 786995.9981,
    "outflow_usd": 788730.02,
    "number_of_txns": 143,
    "avg_txn_value": 5503.4685,
    "avg_txn_value_usd": 5515.59
  },
  {
    "date": "2019-10-24",
    "hour": "16:00:00", // not available when window 1d
    "datetime": "2019-10-24 16:00:00", // not available when window 1d
    "outflow": 74282.2861,
    "outflow_usd": 74320.05,
    "number_of_txns": 15,
    "avg_txn_value": 4952.1524,
    "avg_txn_value_usd": 4954.67
  }
]
```

This endpoint returns the inflow of stablecoins into exchange wallets. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| exchange  | _string_ | An exchange from the [table](#stablecoin-exchange-flows) that we support       |
| direction | _string_ | `inflow`                                            |
| window    | _string_ | `1h` or `1d`                                        |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field             | Type      | Description                                                                                                                |
| ----------------- | --------- | -------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                   |
| hour              | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field that only appears if the `window=1h` is used. |
| inflow            | _decimal_ | The total amount of the token that flowed into the exchange on this date. Denominated in the token in question.            |
| inflow_usd        | _decimal_ | The USD value of the total amount of the token that flowed into the exchange on this date                                  |
| number_of_txns    | _integer_ | The number of transactions sending the token into this exchange on this date.                                              |
| avg_txn_value     | _decimal_ | The average amount of tokens transferred per transaction into the given exchange on this date.                             |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of tokens transferred per transaction into the given exchange on this date.            |



## Stablecoins Full Historical Static Flows to Exchanges

<img src="https://img.shields.io/badge/Tier-Enterprise-blueviolet.svg"/>

This endpoint returns _static_ flows of stablecoins into exchange wallets for as far back as we track. What do we mean by static? while our standard API endpoint as seen <a href="https://docs.tokenanalyst.io/#stablecoins-full-historical-inflow-from-exchanges" target="_blank">above</a> dynamically updates the data (up to 7 days prior to the current day) when we find new information on exchange wallets, the historical data from this endpoint _never_ changes from the time it is posted. The rationale for this is to serve a snapshot look of what was known at the specific point in time - to aid in effective backtesting and inputs for ML models. This is suited for users who want to use our websocket. 

<aside class="notice">
The static endpoint lags behind the tip of the chain by 2 hours in order to leave time to for our internal algorithms classify wallets definitively. This is important because the data in this endpoint does not change after it is posted (unlike the other endpoints).
</aside>

For this reason, as an extra reinforcement, this endpoint includes the `last_updated` field to show the time in UTC when the data point was last modified. Additionally, there is a `lag` parameter that needs to be explicitly included with the option of `hour` - which signifies the default 2 hour lag.

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_static/last?format=json&exchange=binance&token=usdc&direction=inflow&window=1h&lag=hour&limit=2&key=API_KEY"
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
| token        | _string_  | `usdc`                                                                                     |
| direction    | _string_  | `inflow` or `outflow`                                                                     |
| exchange     | _string_  | An exchange from the [table](#stablecoin-exchange-flows) that we support                                                |
| lag          | _string_  | `hour` (default 2 hour lag)              |
| window       | _string_  | `1h`                                                                            |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                                 | Type      | Description                                                                                                                                                                                                               |
| ------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value                         | _decimal_ | The average amount stablecoin transferred per transaction into the given exchange on this date.                                                                                                                                  |
| avg_txn_value_usd                     | _decimal_ | The USD value of the average amount of stablecoin transferred per transaction into the given exchange on this date.                                                                                                              |
| date                                  | _string_  | The date in _YYYY-MM-DD_                                                                                                                                                                                                  |
| datetime *                             | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`                                                                               |
| hour *                                 | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                                                                                        |
| inflow                                | _decimal_ | The total amount of stablecoin that flowed into the exchange on this date. Denominated in ERC20 token.                                                                                                                                     |
| inflow_usd                            | _decimal_ | The USD value of the total amount of stablecoin that flowed into the exchange on this date                                                                                                                                       |
| number_of_txns                        | _integer_ | The number of transactions sending stablecoin into this exchange on this date.                                                                                                                                                   |
| last_updated                          | _string_  | The date when the endpoint was last updated in `UTC` datetime format


## Tether (Omni) Full Historical Top 10 Inflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_window_historical/last?token=usdt_omni&exchange=binance&direction=inflow&format=json&window=1d&limit=2&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2019-08-18",
    "transactionid": "5e5c74b0aab078c929952f9de0155d32152c0dc7c65c8cfdc53c2c0ed1a4d720",
    "transaction_datetime": "2019-08-18 04:48:59",
    "value": 34000,
    "rank": 9,
    "value_usd": 34001.93
  },
  {
    "date": "2019-08-18",
    "transactionid": "84801e2b0fa58093fa74b997a3bfd936b598c91ff1d9f16cf55b8d294ff2c672",
    "transaction_datetime": "2019-08-18 18:50:19",
    "value": 33283,
    "rank": 10,
    "value_usd": 33284.88
  }
]
```

This endpoint returns the top 10 transactions (in terms of total USDT sent) flowing into exchange wallets for every day that the exchange wallets we track have been live on the blockchain.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_window_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| direction | _string_ | `inflow`                                            |
| exchange  | _string_ | An exchange from the [table](#stablecoin-exchange-flows) that we support     |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field         | Type      | Description                                                                                                       |
| ------------- | --------- | ----------------------------------------------------------------------------------------------------------------- |
| date          | _string_  | The date in _YYYY-MM-DD_                                                                                          |
| transactionid | _string_  | The transaction id of the transaction in question.                                                                |
| transaction_datetime | _string_  | The timestamp in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone) when the transaction was mined            |
| value         | _decimal_ | The amount of USDT transferred in this transaction.                                                               |
| rank          | _integer_ | Ranking out of 10 for the 10 largest USDT (Omni) transactions flowing into the exchange in question on this date. |
| value_usd     | _decimal_ | The value in USD of the amount of USDT tranferred in this transaction.                                            |

## Tether (Omni) Full Historical Top 10 Outflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_window_historical/last?token=usdt_omni&exchange=binance&direction=outflow&format=json&limit=2&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2019-08-14",
    "transactionid": "5354b702a372027cc23bb9c47749bdfab77c9d7739f8afafcf49178bc6659a2b",
    "transaction_datetime": "2019-08-14 17:23:03",
    "value": 129985,
    "rank": 3,
    "value_usd": 129985
  },
  {
    "date": "2019-08-14",
    "transactionid": "7a91a7b4eabe7b0d0e77139ea1ed7eaecd6d45d82f7b789aae41617cfcdcf026",
    "transaction_datetime": "2019-08-14 16:37:27",
    "value": 100090,
    "rank": 4,
    "value_usd": 100090
  }
]
```

This endpoint returns the top 10 transactions (in terms of total USDT sent) flowing out of exchange wallets for every day that the exchange wallets we track have been live on the blockchain.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_window_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| direction | _string_ | `outflow`                                           |
| exchange  | _string_ | An exchange from the [table](#stablecoin-exchange-flows) that we support        |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field         | Type      | Description                                                                                                       |
| ------------- | --------- | ----------------------------------------------------------------------------------------------------------------- |
| date          | _string_  | The date in _YYYY-MM-DD_                                                                                          |
| transactionid | _string_  | The transaction id of the transaction in question.                                                                |
| transaction_datetime | _string_  | The timestamp in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone) when the transaction was mined            |
| value         | _decimal_ | The amount of USDT transferred in this transaction.                                                               |
| rank          | _integer_ | Ranking out of 10 for the 10 largest USDT (Omni) transactions flowing into the exchange in question on this date. |
| value_usd     | _decimal_ | The value in USD of the amount of USDT tranferred in this transaction.                                            |
