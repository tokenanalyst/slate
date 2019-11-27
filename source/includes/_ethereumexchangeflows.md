# Ethereum Exchange Flows

For Ethereum currently supported exchanges are:

| Name           | Symbol           |
|----------------|------------------|
| Binance        | `binance`        | 
| Bittrex        | `bittrex`        | 
| Bitfinex       | `bitfinex`       |
| Kraken         | `kraken`         |
| Kucoin         | `kucoin`         |
| Poloniex       | `poloniex`       |

## ETH Full Historical Flows Into Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=eth&exchange=binance&direction=inflow&window=1h&format=json&from_date=2018-01-01&to_date=2018-01-05&limit=2&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2018-01-05",
    "hour": "22:00:00", // not available when window 1d
    "datetime": "2018-01-05 22:00:00", // not available when window 1d
    "inflow": 11758.0723,
    "inflow_usd": 11131601.58,
    "number_of_txns": 8461,
    "avg_txn_value": 1.3897,
    "avg_txn_value_usd": 1315.64
  },
  {
    "date": "2018-01-05",
    "hour": "23:00:00", // not available when window 1d
    "datetime": "2018-01-05 23:00:00", // not available when window 1d
    "inflow": 11330.9083,
    "inflow_usd": 10958461.64,
    "number_of_txns": 8439,
    "avg_txn_value": 1.3427,
    "avg_txn_value_usd": 1298.55
  }
]
```

This endpoint returns the inflow of ETH into exchange wallets. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC 

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_window_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |
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
| hour *   | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field field and appears when window is `1h`                                                                                                        |
| datetime *  | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h`                                                                               |
| inflow  | _decimal_ | The total amount of ETH that flowed into the exchange on this date. Denominated in ETH.         |
| inflow_usd  | _decimal_ | The USD value of the total amount of ETH that flowed into the exchange on this date         |
| number_of_txns       | _integer_ | The number of transactions sending ETH into this exchange on this date.                                 |
| avg_txn_value       | _decimal_ | The average amount ETH transferred per transaction into the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of ETH transferred per transaction into the given exchange on this date.    |

## ETH Full Historical Flows Out Of Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=eth&exchange=binance&direction=outflow&window=1h&format=json&from_date=2019-01-01&to_date=2019-01-05&limit=2&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2019-01-05",
    "hour": "22:00:00", // not available when window 1d
    "datetime": "2019-01-05 22:00:00", // not available when window 1d
    "outflow": 4019.589,
    "outflow_usd": 631879.37,
    "number_of_txns": 133,
    "avg_txn_value": 30.2225,
    "avg_txn_value_usd": 4750.97
  },
  {
    "date": "2019-01-05",
    "hour": "23:00:00", // not available when window 1d
    "datetime": "2019-01-05 23:00:00", // not available when window 1d
    "outflow": 591.5552,
    "outflow_usd": 92418.66,
    "number_of_txns": 92,
    "avg_txn_value": 6.4299,
    "avg_txn_value_usd": 1004.55
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
| token     | _string_ | `eth`                                               |
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

## ETH Full Historical Static Flows to Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns _static_ flows of ETH into exchange wallets for as far back as we track. What do we mean by static? while our standard API endpoint as seen <a href="https://docs.tokenanalyst.io/#eth-full-historical-flows-into-exchanges" target="_blank">above</a> dynamically updates the data (up to 7 days prior to the current day) when we find new information on exchange wallets, the historical data from this data _never_ changes from the time it is posted. The rationale for this is to serve a snapshot look of what was known at the specific point in time - to aid in effective backtesting and inputs for ML models. This is suited for users who want to use our websocket. 

For this reason, as an extra reinforcement, this endpoint includes the `last_updated` field to show the time in UTC when the data point was last modified. 

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_static/last?format=json&exchange=binance&token=eth&direction=inflow&window=1h&lag=hour&limit=2&key=API_KEY"
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
| token        | _string_  | `eth`                                                                                     |
| direction    | _string_  | `inflow` or `outflow`                                                                     |
| exchange     | _string_  | An exchange from the table that we support                                                |
| lag          | _string_  | `hour`,`day`, or `week`. Lags the returned data by the specified parameter               |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                                 | Type      | Description                                                                                                                                                                                                               |
| ------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value                         | _decimal_ | The average amount ETH transferred per transaction into the given exchange on this date.                                                                                                                                  |
| avg_txn_value_usd                     | _decimal_ | The USD value of the average amount of ETH transferred per transaction into the given exchange on this date.                                                                                                              |
| date                                  | _string_  | The date in _YYYY-MM-DD_                                                                                                                                                                                                  |
| datetime *                             | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h`                                                                               |
| hour *                                 | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field field and appears when window is `1h`                                                                                                        |
| inflow                                | _decimal_ | The total amount of ETH that flowed into the exchange on this date. Denominated in ETH.                                                                                                                                     |
| inflow_usd                            | _decimal_ | The USD value of the total amount of ETH that flowed into the exchange on this date                                                                                                                                       |
| number_of_txns                        | _integer_ | The number of transactions sending ETH into this exchange on this date.                                                                                                                                                   |
| last_updated                          | _string_  | The date when the endpoint was last updated in `UTC` datetime format

## ETH Full Historical Top 10 Inflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?token=eth&exchange=binance&direction=inflow&format=json&limit=2&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "transactionhash": "0x8f4e1350eaa1c13360ea4a5269a1a350f3c5b3880147d0aa32ec34a12fc30923",
    "value": 3424.6575,
    "date": "2019-04-29",
    "transaction_datetime": "2019-04-29 09:13:57",
    "rank": 2,
    "value_usd": 537210.85
  },
  {
    "transactionhash": "0x5512d27b371bfbef2fc6dae353fb243866fe3dfb24ad546d6b6eebb4159fb7c2",
    "value": 3000.0,
    "date": "2019-04-29",
    "transaction_datetime": "2019-04-29 04:50:08",
    "rank": 3,
    "value_usd": 470596.71
  }
]
```

This endpoint returns the top 10 transactions (in terms of total ETH sent) flowing into exchange wallets for every day that the exchange wallets we track have been live on the blockchain.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |
| direction | _string_ | `inflow`                                            |
| exchange  | _string_ | An exchange from the list of ones we support        |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| transactionhash | _string_ | The transaction hash of the transaction in question.                                            |
| value  | _decimal_ | The amount of ETH transferred in this transaction.        |
| date       | _string_ | The date in _YYYY-MM-DD_                                 |
| transaction_datetime | _string_  | The timestamp in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone) when the transaction was mined            |
| rank     | _integer_ | Ranking out of 10 for the 10 largest ETH transactions flowing into the exchange in question on this date.                                             |
| value_usd  | _decimal_ | The value in USD of the amount of ETH tranferred in this transaction.        |

## ETH Full Historical Top 10 Outflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?token=eth&exchange=binance&direction=outflow&format=json&limit=2&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "transactionhash": "0x97b8063962d549b053cf7366e70877f09ede29f5e2d5bd9837e5a9ea8089bb46",
    "value": 7300.00024,
    "date": "2019-04-26",
    "transaction_datetime": "2019-04-26 09:03:53",
    "rank": 3,
    "value_usd": 1129368.16
  },
  {
    "transactionhash": "0x0e3d275eeae64b27ccbb12b65861039a7c3662c0c99212f88b9927c41b37bbae",
    "value": 5982.0288,
    "date": "2019-04-26",
    "transaction_datetime": "2019-04-26 04:02:49",
    "rank": 4,
    "value_usd": 925467.48
  }
]
```

This endpoint returns the top 10 transactions (in terms of total ETH sent) flowing out of exchange wallets for every day that the exchange wallets we track have been live on the blockchain.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |
| direction | _string_ | `outflow`                                           |
| exchange  | _string_ | An exchange from the list of ones we support        |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| transactionhash | _string_ | The transaction hash of the transaction in question.                                            |
| value  | _decimal_ | The amount of ETH transferred in this transaction.        |
| date       | _string_ | The date in _YYYY-MM-DD_                                 |
| transaction_datetime | _string_  | The timestamp in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone) when the transaction was mined            |
| rank     | _integer_ | Ranking out of 10 for the 10 largest ETH transactions flowing out of the exchange in question on this date.                                             |
| value_usd  | _decimal_ | The value in USD of the amount of ETH tranferred in this transaction.        |
