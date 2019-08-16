# Ethereum Exchange Flows

For Ethereum currently supported exchanges are: `binance`, `kraken`, `bitfinex`, `poloniex`, `bittrex`, `kucoin`

## ETH Full Historical Flows Into Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=eth&exchange=binance&direction=inflow&window=1h&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2016-03-17",
    "hour": "11:00:00",
    "inflow": 1.8164,
    "price_usd": 11.64,
    "inflow_usd": 21.14,
    "number_of_txns": 8,
    "avg_txn_value": 0.22705,
    "avg_txn_value_usd": 2.64
  },
  {
    "date": "2016-03-18",
    "hour": "12:00:00",
    "inflow": 3.7594499999999997,
    "price_usd": 10.21,
    "inflow_usd": 38.38,
    "number_of_txns": 5,
    "avg_txn_value": 0.75189,
    "avg_txn_value_usd": 7.68
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
| exchange  | _string_ | An exchange from the list of ones we support        |
| window    | _string_ | `1h` or `1d`       |

### Data Overview

| Field | Type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| date     | _string_ | The date in _YYYY-MM-DD_                                                  |
| hour     | _string_ | The hour of the day in _HH:MM:SS_  (UTC time zone). This is an optional field based on the params used.                                               |
| inflow  | _decimal_ | The total amount of ETH that flowed into the exchange on this date. Denominated in ETH.         |
| price_usd | _decimal_ | The daily average price of ETH in USD (the daily mean of minute-level price data) |
| inflow_usd  | _decimal_ | The USD value of the total amount of ETH that flowed into the exchange on this date         |
| number_of_txns       | _integer_ | The number of transactions sending ETH into this exchange on this date.                                 |
| avg_txn_value       | _decimal_ | The average amount ETH transferred per transaction into the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of ETH transferred per transaction into the given exchange on this date.    |


## ETH Full Historical Flows Out Of Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=eth&exchange=binance&direction=outflow&window=1h&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2016-03-17",
    "hour": "11:00:00",
    "outflow": 1.8164,
    "price_usd": 11.64,
    "outflow_usd": 21.14,
    "number_of_txns": 8,
    "avg_txn_value": 0.22705,
    "avg_txn_value_usd": 2.64
  },
  {
    "date": "2016-03-18",
    "hour": "12:00:00",
    "outflow": 3.7594499999999997,
    "price_usd": 10.21,
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
| token     | _string_ | `eth`                                               |
| direction | _string_ | `outflow`                                            |
| exchange  | _string_ | An exchange from the list of ones we support        |
| window    | _string_ | `1h` or `1d`       |

### Data Overview

| Field | Type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| date     | _string_ | The date in _YYYY-MM-DD_                                                  |
| hour     | _string_ | The hour of the day in _HH:MM:SS_  (UTC time zone). This is an optional field based on the params used.                                               |
| outflow  | _decimal_ | The total amount of ETH that flowed out of the exchange on this date. Denominated in ETH.         |
| price_usd | _decimal_ | The daily average price of ETH in USD (the daily mean of minute-level price data) |
| outflow_usd  | _decimal_ | The USD value of the total amount of ETH that flowed out of the exchange on this date         |
| number_of_txns       | _integer_ | The number of transactions sending ETH out of this exchange on this date.                                 |
| avg_txn_value       | _decimal_ | The average amount ETH transferred per transaction out of the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of ETH transferred per transaction out of the given exchange on this date.    |

## ETH Full Historical Top 10 Inflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?token=eth&exchange=binance&direction=inflow&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "transactionhash": "0x8f4e1350eaa1c13360ea4a5269a1a350f3c5b3880147d0aa32ec34a12fc30923",
    "value": 3424.6575,
    "date": "2019-04-29",
    "rank": 2,
    "value_usd": 537210.85
  },
  {
    "transactionhash": "0x5512d27b371bfbef2fc6dae353fb243866fe3dfb24ad546d6b6eebb4159fb7c2",
    "value": 3000.0,
    "date": "2019-04-29",
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

### Data Overview

| Field | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| transactionhash | _string_ | The transaction hash of the transaction in question.                                            |
| value  | _decimal_ | The amount of ETH transferred in this transaction.        |
| date       | _string_ | The date in _YYYY-MM-DD_                                 |
| rank     | _integer_ | Ranking out of 10 for the 10 largest ETH transactions flowing into the exchange in question on this date.                                             |
| value_usd  | _decimal_ | The value in USD of the amount of ETH tranferred in this transaction.        |

## ETH Full Historical Top 10 Outflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?token=eth&exchange=binance&direction=outflow&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "transactionhash": "0x97b8063962d549b053cf7366e70877f09ede29f5e2d5bd9837e5a9ea8089bb46",
    "value": 7300.00024,
    "date": "2019-04-26",
    "rank": 3,
    "value_usd": 1129368.16
  },
  {
    "transactionhash": "0x0e3d275eeae64b27ccbb12b65861039a7c3662c0c99212f88b9927c41b37bbae",
    "value": 5982.0288,
    "date": "2019-04-26",
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

### Data Overview

| Field | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| transactionhash | _string_ | The transaction hash of the transaction in question.                                            |
| value  | _decimal_ | The amount of ETH transferred in this transaction.        |
| date       | _string_ | The date in _YYYY-MM-DD_                                 |
| rank     | _integer_ | Ranking out of 10 for the 10 largest ETH transactions flowing out of the exchange in question on this date.                                             |
| value_usd  | _decimal_ | The value in USD of the amount of ETH tranferred in this transaction.        |