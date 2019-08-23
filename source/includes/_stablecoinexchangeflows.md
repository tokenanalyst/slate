# Stablecoin Exchange Flows

The stablecoins we currently support are:

| Name                 | Symbol       |
| -------------------- | ------------ |
| Tether (Omni)        | `usdt_omni`  |
| Tether (ERC20)       | `usdt_erc20` |
| USDC                 | `usdc`       |
| Paxos Standard Token | `pax`        |
| TrueUSD              | `tusd`       |
| Gemini Dollar        | `gusd`       |
| Dai                  | `dai`        |

For Tether (Omni), currently supported exchanges are: `kraken`, `bitfinex`, `poloniex`, `bittrex`, `okex`

For ERC20 Stablecoins, currently supported exchanges are: `binance`, `kraken`, `bitfinex`, `poloniex`, `bittrex`, `kucoin`

## Tether (Omni) Full Historical Inflow from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?format=json&window=1d&token=usdt_omni&exchange=kraken&direction=inflow&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-08-16",
    "inflow": 2760452.458,
    "inflow_usd": 2760452.46,
    "number_of_txns": 26,
    "price_usd": 1,
    "avg_txn_value": 106171.2484,
    "avg_txn_value_usd": 106171.25
  },
  {
    "date": "2019-08-17",
    "inflow": 97184.7667,
    "inflow_usd": 97184.76,
    "number_of_txns": 10,
    "price_usd": 1,
    "avg_txn_value": 9718.4767,
    "avg_txn_value_usd": 9718.48
  }
]
```

This endpoint returns the inflow of USDT (Tether) on the Omni blockchain into exchange wallets. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| exchange  | _string_ | Which supported exchange you require flow data for  |
| direction | _string_ | `inflow`                                            |
| window    | _string_ | `1h` or `1d`                                        |

### Data Overview

| Field             | Type      | Description                                                                                                                |
| ----------------- | --------- | -------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                   |
| hour              | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field that only appears if the `window=1h` is used. |
| inflow            | _decimal_ | The total amount of the token that flowed into the exchange on this date. Denominated in the token in question.            |
| inflow_usd        | _decimal_ | The USD value of the total amount of the token that flowed into the exchange on this date                                  |
| number_of_txns    | _integer_ | The number of transactions sending the token into this exchange on this date.                                              |
| price_usd         | _decimal_ | The daily average price of the token in USD (the daily mean of minute-level price data)                                    |
| avg_txn_value     | _decimal_ | The average amount of tokens transferred per transaction into the given exchange on this date.                             |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of tokens transferred per transaction into the given exchange on this date.            |

## Tether (Omni) Full Historical Outflow from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?format=json&window=1d&token=usdt_omni&exchange=huobi&direction=outflow&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-09-26",
    "outflow": 11148431.05,
    "outflow_usd": 11137036.46,
    "number_of_txns": 465,
    "price_usd": 1,
    "avg_txn_value": 23975.1205,
    "avg_txn_value_usd": 23950.62
  },
  {
    "date": "2018-09-27",
    "outflow": 15456621.51,
    "outflow_usd": 15426543.13,
    "number_of_txns": 436,
    "price_usd": 1,
    "avg_txn_value": 35450.9668,
    "avg_txn_value_usd": 35381.98
  }
]
```

This endpoint returns the inflow of USDT (Tether) on the Omni blockchain into exchange wallets. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| exchange  | _string_ | Which supported exchange you require flow data for  |
| direction | _string_ | `inflow`                                            |
| window    | _string_ | `1h` or `1d`                                        |

### Data Overview

| Field             | Type      | Description                                                                                                                |
| ----------------- | --------- | -------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                   |
| hour              | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field that only appears if the `window=1h` is used. |
| inflow            | _decimal_ | The total amount of the token that flowed into the exchange on this date. Denominated in the token in question.            |
| inflow_usd        | _decimal_ | The USD value of the total amount of the token that flowed into the exchange on this date                                  |
| number_of_txns    | _integer_ | The number of transactions sending the token into this exchange on this date.                                              |
| price_usd         | _decimal_ | The daily average price of the token in USD (the daily mean of minute-level price data)                                    |
| avg_txn_value     | _decimal_ | The average amount of tokens transferred per transaction into the given exchange on this date.                             |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of tokens transferred per transaction into the given exchange on this date.            |

## Tether (Omni) Full Historical Top 10 Inflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?token=usdt_omni&exchange=binance&direction=inflow&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2019-08-18",
    "transactionid": "5e5c74b0aab078c929952f9de0155d32152c0dc7c65c8cfdc53c2c0ed1a4d720",
    "value": 34000,
    "rank": 9,
    "value_usd": 34001.93
  },
  {
    "date": "2019-08-18",
    "transactionid": "84801e2b0fa58093fa74b997a3bfd936b598c91ff1d9f16cf55b8d294ff2c672",
    "value": 33283,
    "rank": 10,
    "value_usd": 33284.88
  }
]
```

This endpoint returns the top 10 transactions (in terms of total USDT sent) flowing into exchange wallets for every day that the exchange wallets we track have been live on the blockchain.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| direction | _string_ | `inflow`                                            |
| exchange  | _string_ | An exchange from the list of ones we support        |

### Data Overview

| Field         | Type      | Description                                                                                                       |
| ------------- | --------- | ----------------------------------------------------------------------------------------------------------------- |
| date          | _string_  | The date in _YYYY-MM-DD_                                                                                          |
| transactionid | _string_  | The transaction id of the transaction in question.                                                                |
| value         | _decimal_ | The amount of USDT transferred in this transaction.                                                               |
| rank          | _integer_ | Ranking out of 10 for the 10 largest USDT (Omni) transactions flowing into the exchange in question on this date. |
| value_usd     | _decimal_ | The value in USD of the amount of USDT tranferred in this transaction.                                            |

## Tether (Omni) Full Historical Top 10 Outflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?token=usdt_omni&exchange=binance&direction=outflow&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2019-08-14",
    "transactionid": "5354b702a372027cc23bb9c47749bdfab77c9d7739f8afafcf49178bc6659a2b",
    "value": 129985,
    "rank": 3,
    "value_usd": 129985
  },
  {
    "date": "2019-08-14",
    "transactionid": "7a91a7b4eabe7b0d0e77139ea1ed7eaecd6d45d82f7b789aae41617cfcdcf026",
    "value": 100090,
    "rank": 4,
    "value_usd": 100090
  }
]
```

This endpoint returns the top 10 transactions (in terms of total USDT sent) flowing out of exchange wallets for every day that the exchange wallets we track have been live on the blockchain.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| direction | _string_ | `outflow`                                           |
| exchange  | _string_ | An exchange from the list of ones we support        |

### Data Overview

| Field         | Type      | Description                                                                                                       |
| ------------- | --------- | ----------------------------------------------------------------------------------------------------------------- |
| date          | _string_  | The date in _YYYY-MM-DD_                                                                                          |
| transactionid | _string_  | The transaction id of the transaction in question.                                                                |
| value         | _decimal_ | The amount of USDT transferred in this transaction.                                                               |
| rank          | _integer_ | Ranking out of 10 for the 10 largest USDT (Omni) transactions flowing into the exchange in question on this date. |
| value_usd     | _decimal_ | The value in USD of the amount of USDT tranferred in this transaction.                                            |

## ERC20 Stablecoin Full Historical Inflow from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_window_historical/last?token=usdc&direction=inflow&window=1h&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-11-06",
    "hour": "11:00:00",
    "token_name": "USDC",
    "exchange": "Binance",
    "inflow": 509.689581,
    "price_usd": 1.0,
    "inflow_usd": 511.09,
    "number_of_txns": 3,
    "avg_txn_value": 169.896527,
    "avg_txn_value_usd": 170.36
  },
  {
    "date": "2018-11-07",
    "hour": "12:00:00",
    "token_name": "USDC",
    "exchange": "Kucoin",
    "inflow": 3585.887836,
    "price_usd": 1.01,
    "inflow_usd": 3609.0,
    "number_of_txns": 3,
    "avg_txn_value": 1195.2959453333333,
    "avg_txn_value_usd": 1203.0
  }
]
```

This endpoint returns the inflow of stablecoins into exchange wallets. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC. As a reminder, the exchanges we support for this endpoint are: `binance`, `kraken`, `bitfinex`, `poloniex`, `bittrex`, `kucoin`.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdc`                                              |
| direction | _string_ | `inflow`                                            |
| window    | _string_ | `1h` or `1d`                                        |

### Data Overview

| Field             | Type      | Description                                                                                                     |
| ----------------- | --------- | --------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                        |
| hour              | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field based on the params used.          |
| token_name        | _string_  | The name of the token in question                                                                               |
| exchange          | _string_  | The name of the exchange in question                                                                            |
| inflow            | _decimal_ | The total amount of the token that flowed into the exchange on this date. Denominated in the token in question. |
| price_usd         | _decimal_ | The daily average price of the token in USD (the daily mean of minute-level price data)                         |
| inflow_usd        | _decimal_ | The USD value of the total amount of the token that flowed into the exchange on this date                       |
| number_of_txns    | _integer_ | The number of transactions sending the token into this exchange on this date.                                   |
| avg_txn_value     | _decimal_ | The average amount of tokens transferred per transaction into the given exchange on this date.                  |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of tokens transferred per transaction into the given exchange on this date. |

## ERC20 Stablecoin Full Historical Outflow from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_window_historical/last?token=usdc&direction=outflow&window=1h&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-11-06",
    "hour": "11:00:00",
    "token_name": "USDC",
    "exchange": "Kucoin",
    "outflow": 509.689581,
    "price_usd": 1.0,
    "outflow_usd": 511.09,
    "number_of_txns": 3,
    "avg_txn_value": 169.896527,
    "avg_txn_value_usd": 170.36
  },
  {
    "date": "2018-11-07",
    "hour": "12:00:00",
    "token_name": "USDC",
    "exchange": "Kucoin",
    "outflow": 3585.887836,
    "price_usd": 1.01,
    "outflow_usd": 3609.0,
    "number_of_txns": 3,
    "avg_txn_value": 1195.2959453333333,
    "avg_txn_value_usd": 1203.0
  }
]
```

This endpoint returns the outflow of stablecoins from exchange wallets. The `avg_txn_value`, `outflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdc`                                              |
| direction | _string_ | `outflow`                                           |
| window    | _string_ | `1h` or `1d`                                        |

### Data Overview

| Field             | Type      | Description                                                                                                       |
| ----------------- | --------- | ----------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                          |
| hour              | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field based on the params used.            |
| token_name        | _string_  | The name of the token in question                                                                                 |
| exchange          | _string_  | The name of the exchange in question                                                                              |
| outflow           | _decimal_ | The total amount of the token that flowed out of the exchange on this date. Denominated in the token in question. |
| price_usd         | _decimal_ | The daily average price of the token in USD (the daily mean of minute-level price data)                           |
| outflow_usd       | _decimal_ | The USD value of the total amount of the token that flowed out of the exchange on this date                       |
| number_of_txns    | _integer_ | The number of transactions sending the token out of this exchange on this date.                                   |
| avg_txn_value     | _decimal_ | The average amount of tokens transferred per transaction out of the given exchange on this date.                  |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of tokens transferred per transaction out of the given exchange on this date. |
