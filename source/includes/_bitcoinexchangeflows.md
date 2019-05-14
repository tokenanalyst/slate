# Bitcoin Exchange Flows

For Bitcoin currently supported exchanges are: `binance`, `bittrex`, `bitstamp`, `poloniex`, `bitmex`, `bitfinex`

## Full Historical Inflow to Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the inflow of BTC into exchange wallets for as far back as we track. The average inflow is the average transaction value for transactions flowing into exchange wallets on a given day.

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?format=json&key=API_KEY&token=btc&exchange=binance&direction=inflow"
```

> The response looks like:

```json
[
  {
    "avg_txn_value": "0.79",
    "avg_txn_value_usd": "3306.01",
    "date": "2017-08-16",
    "entity": "Binance",
    "inflow": "1053.89",
    "inflow_usd": "4410336.79",
    "number_of_entity_receiving_addresses": "1349",
    "number_of_nonentity_sending_addresses": "19413",
    "number_of_txns": "1338"
  },
  {
    "avg_txn_value": "1.15",
    "avg_txn_value_usd": "5009.32",
    "date": "2017-08-17",
    "entity": "Binance",
    "inflow": "2236.29",
    "inflow_usd": "9741124.94",
    "number_of_entity_receiving_addresses": "2121",
    "number_of_nonentity_sending_addresses": "24915",
    "number_of_txns": "1950"
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| key       | _string_ | Your unique API key                                  |
| format    | _string_ | What format you want your data in (`json` or `csv`)  |
| token     | _string_ | `btc`                                                |
| direction | _string_ | Either `inflow` or `outflow` (in this case `inflow`) |
| exchange  | _string_ | An exchange from the list of ones we support         |

## Full Historical Outflows from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the outflow of BTC from exchange wallets for as far back as we track. The average outflow is the average transaction value for transactions flowing out of exchange wallets on a given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?`

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?token=btc&exchange=binance&direction=outflow&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "avg_txn_value": "26.73",
    "avg_txn_value_usd": "69375.93",
    "date": "2017-07-05",
    "entity": "Binance",
    "number_of_entity_sending_addresses": "23",
    "number_of_nonentity_receiving_addresses": "1",
    "number_of_txns": "3",
    "outflow": "26.73",
    "outflow_usd": "69375.93"
  },
  {
    "avg_txn_value": "102.48",
    "avg_txn_value_usd": "241881.49",
    "date": "2017-07-12",
    "entity": "Binance",
    "number_of_entity_sending_addresses": "77",
    "number_of_nonentity_receiving_addresses": "1",
    "number_of_txns": "2",
    "outflow": "102.48",
    "outflow_usd": "241881.49"
  }
]
```

### URL Parameters

| Parameter | Type     | Description                                           |
| --------- | -------- | ----------------------------------------------------- |
| key       | _string_ | Your unique API key                                   |
| format    | _string_ | What format you want your data in (`json` or `csv`)   |
| token     | _string_ | `btc`                                                 |
| direction | _string_ | Either `inflow` or `outflow` (in this case `outflow`) |
| exchange  | _string_ | An exchange from the list of ones we support          |

## Full Historical Top 10 Inflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the top 10 transactions (in terms of total BTC sent) flowing into exchange wallets for every day that the exchange wallets we track have been live on the blockchain.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?`

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?token=btc&exchange=binance&direction=inflow&format=json&key=API_KEY"
```

> This is what the response looks like

```json
[
  {
    "date": "2017-06-23",
    "entity": "Binance",
    "rank": "1",
    "transactionhash": "0546f2545393d706b3b77ec251be93af12038dc28eefd5dc0d27acea9f0613a0",
    "transactionid": "0546f2545393d706b3b77ec251be93af12038dc28eefd5dc0d27acea9f0613a0",
    "value": "0.01",
    "value_usd": "52.51"
  }
]
```

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |
| direction | _string_ | `inflow`                                            |
| exchange  | _string_ | An exchange from the list of ones we support        |
