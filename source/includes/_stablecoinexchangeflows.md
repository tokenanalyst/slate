# Stablecoin Exchange Flows

The stablecoins we currently support are:

| Name                 | Symbol |
| -------------------- | ------ |
| Tether               | `usdt_erc20` |
| USDC                 | `usdc` |
| Paxos Standard Token | `pax`  |
| TrueUSD              | `tusd` |
| Gemini Dollar        | `gusd` |
| Dai                  | `dai`  |


## Stablecoin Full Historical Inflow from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_window_historical/last?token=omg&direction=inflow&window=1h&format=json&key=API_KEY"
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

This endpoint returns the inflow of stablecoins into exchange wallets. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). `hour` is in UTC

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt`                                               |
| direction | _string_ | `inflow`                                           |
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


## Stablecoin Full Historical Outflow from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_window_historical/last?token=omg&direction=outflow&window=1h&format=json&key=API_KEY"
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
| token     | _string_ | `usdt`                                               |
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