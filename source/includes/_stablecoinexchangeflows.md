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
    "date": "2018-11-28",
    "token_name": "USDC",
    "exchange": "Binance",
    "inflow": 7170265.744998998,
    "price": 1.01,
    "inflow_usd": 7253918.77,
    "number_of_txns": 174,
    "avg_txn_value": 41208.42382183332,
    "avg_txn_value_usd": 41689.19
  },
  {
    "date": "2018-11-28",
    "token_name": "USDC",
    "exchange": "Kucoin",
    "inflow": 7724.377048,
    "price": 1.01,
    "inflow_usd": 7814.49,
    "number_of_txns": 6,
    "avg_txn_value": 1287.3961746666666,
    "avg_txn_value_usd": 1302.42
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
