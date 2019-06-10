# Stablecoin Exchange Flows

The stablecoins we currently support are:

| Name                 | Symbol |
| -------------------- | ------ |
| Tether               | `usdt` |
| USDC                 | `usdc` |
| Paxos Standard Token | `pax`  |
| TrueUSD              | `tusd` |
| Gemini Dollar        | `gusd` |
| Dai                  | `dai`  |


## Stablecoin Full Historical Inflow to Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_historical/last?token=usdc&direction=inflow&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-09-25",
    "token_name": "USDC",
    "exchange": "Kucoin",
    "inflow": 2.0,
    "price": 0.0,
    "inflow_usd": 0.0,
    "number_of_txns": 1,
    "avg_txn_value": 2.0,
    "avg_txn_value_usd": 0.0
  },
  {
    "date": "2018-09-28",
    "token_name": "USDC",
    "exchange": "Kucoin",
    "inflow": 261.08372099999997,
    "price": 0.0,
    "inflow_usd": 0.0,
    "number_of_txns": 2,
    "avg_txn_value": 130.54186049999998,
    "avg_txn_value_usd": 0.0
  }
]
```

This endpoint returns the inflow of Stablecoins into exchange wallets. The `avg_txn_value` is the average transaction value for transactions flowing into exchange wallets on a given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdc`                                              |
| direction | _string_ | `inflow`                                            |


## Stablecoin Full Historical Outflow from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_historical/last?token=usdc&direction=outflow&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-11-06",
    "token_name": "USDC",
    "exchange": "Kucoin",
    "outflow": 509.689581,
    "price": 1.0,
    "outflow_usd": 511.09,
    "number_of_txns": 3,
    "avg_txn_value": 169.896527,
    "avg_txn_value_usd": 170.36
  },
  {
    "date": "2018-11-07",
    "token_name": "USDC",
    "exchange": "Kucoin",
    "outflow": 3585.887836,
    "price": 1.01,
    "outflow_usd": 3609.0,
    "number_of_txns": 3,
    "avg_txn_value": 1195.2959453333333,
    "avg_txn_value_usd": 1203.0
  }
]
```

This endpoint returns the outflow of Stablecoins from exchange wallets. The `avg_txn_value` is the average transaction value for transactions flowing out of exchange wallets on a given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/erc20_exchanges_flow_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdc`                                              |
| direction | _string_ | `outflow`                                           |