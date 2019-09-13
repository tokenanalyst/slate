# Bitcoin Exchange Flows

For Bitcoin currently supported exchanges are: `binance`, `bittrex`, `bitstamp`, `poloniex`, `bitmex`, `bitfinex`

<aside class="warning">
Please switch to the Bitcoin Exchange Flows <code>V2</code> endpoint. Bitcoin Exchange Flows <code>V1</code> is no longer updated.
</aside>

## BTC Full Historical Inflow to Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the inflow of BTC into exchange wallets for as far back as we track. The average inflow is the average transaction value for transactions flowing into exchange wallets on a given day.

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?format=json&token=btc&exchange=binance&direction=inflow&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "avg_txn_value": 0.79,
    "avg_txn_value_usd": 3306.01,
    "date": "2017-08-16",
    "entity": "Binance",
    "inflow": 1053.89,
    "inflow_usd": 4410336.79,
    "number_of_entity_receiving_addresses": 1349,
    "number_of_nonentity_sending_addresses": 19413,
    "number_of_txns": 1338
  },
  {
    "avg_txn_value": 1.15,
    "avg_txn_value_usd": 5009.32,
    "date": "2017-08-17",
    "entity": "Binance",
    "inflow": 2236.29,
    "inflow_usd": 9741124.94,
    "number_of_entity_receiving_addresses": 2121,
    "number_of_nonentity_sending_addresses": 24915,
    "number_of_txns": 1950
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
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field | Type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| avg_txn_value       | _decimal_ | The average amount BTC transferred per transaction into the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of BTC transferred per transaction into the given exchange on this date.    |
| date     | _string_ | The date in _YYYY-MM-DD_                                                  |
| entity | _string_ | The name of the exchange in question |
| inflow  | _decimal_ | The total amount of BTC that flowed into the entity on this date. Denominated in BTC.         |
| inflow_usd  | _decimal_ | The USD value of the total amount of BTC that flowed into the exchange on this date         |
| number_of_entity_receiving_addresses  | _integer_ | The distinct number of wallets identified as belonging to the exchange in question that were on the receiving side of a transaction (where no wallets identified as belonging to the exchange were senders) on this date.          |
| number_of_nonentity_sending_addresses  | _integer_ | The distinct number of wallets (that don't belong to the exchange in question) that sent Bitcoin to wallets identified as belonging to this exchange on this date.         |
| number_of_txns       | _integer_ | The number of transactions sending BTC into this exchange on this date.                                 |




## BTC Full Historical Outflows from Exchanges

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
    "avg_txn_value": 26.73,
    "avg_txn_value_usd": 69375.93,
    "date": "2017-07-05",
    "entity": "Binance",
    "number_of_entity_sending_addresses": 23,
    "number_of_nonentity_receiving_addresses": 1,
    "number_of_txns": 3,
    "outflow": 26.73,
    "outflow_usd": 69375.93
  },
  {
    "avg_txn_value": 102.48,
    "avg_txn_value_usd": 241881.49,
    "date": "2017-07-12",
    "entity": "Binance",
    "number_of_entity_sending_addresses": 77,
    "number_of_nonentity_receiving_addresses": 1,
    "number_of_txns": 2,
    "outflow": 102.48,
    "outflow_usd": 241881.49
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
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field | Type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| avg_txn_value       | _decimal_ | The average amount BTC transferred per transaction out of the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of BTC transferred per transaction out of the given exchange on this date.    |
| date     | _string_ | The date in _YYYY-MM-DD_                                                  |
| entity | _string_ | The name of the exchange in question |
| number_of_entity_sending_addresses  | _integer_ | The distinct number of wallets identified as belonging to the exchange in question that were on the sending side of a transaction (where no wallets identified as belonging to the exchange were receivers) on this date.          |
| number_of_nonentity_receiving_addresses  | _integer_ | The distinct number of wallets (that don't to the exchange in question) that received Bitcoin from wallets identified as belonging to this exchange on this date.         |
| number_of_txns  | _decimal_ | The number of transactions sending BTC out of this exchange on this date.         |
| outflow  | _decimal_ | The total amount of BTC that flowed out of the entity on this date. Denominated in BTC.         |
| outflow_usd  | _decimal_ | The USD value of the total amount of BTC that flowed out of the exchange on this date         |



## BTC Full Historical Top 10 Inflow Large Value Transactions

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
    "rank": 1,
    "transactionhash": "0546f2545393d706b3b77ec251be93af12038dc28eefd5dc0d27acea9f0613a0",
    "transactionid": "0546f2545393d706b3b77ec251be93af12038dc28eefd5dc0d27acea9f0613a0",
    "value": 0.01,
    "value_usd": 52.51
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
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |



### Data Overview

| Field | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| date       | _string_ | The date in _YYYY-MM-DD_                                 |
| entity    | _string_ | The name of the exchange in question |
| rank     | _integer_ | Ranking out of 10 for the 10 largest transactions of BTC flowing into the exchange in question on this date.                                             |
| transactionhash | _string_ | The transaction hash of the transaction in question.                                            |
| transactionid  | _string_ | The transaction id of the transaction in question.       |
| value  | _decimal_ | The amount of BTC transferred in this transaction.        |
| value_usd  | _decimal_ | The value in USD of the amount of BTC tranferred in this transaction.        |


## BTC Full Historical Top 10 Outflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?token=btc&exchange=binance&direction=outflow&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2017-08-15",
    "entity": "Binance",
    "rank": 1,
    "transactionhash": "c1053514fbc010322e9fec4d9931e9f4271a1453e1f2b6941c367bf75fd47ca2",
    "transactionid": "c1053514fbc010322e9fec4d9931e9f4271a1453e1f2b6941c367bf75fd47ca2",
    "value": 20,
    "value_usd": 83539.6
  },
  {
    "date": "2017-08-15",
    "entity": "Binance",
    "rank": 2,
    "transactionhash": "d73a0d5c4100cbe3a680fc541d53a27133172f18da99768e89ec245cef93afa1",
    "transactionid": "d73a0d5c4100cbe3a680fc541d53a27133172f18da99768e89ec245cef93afa1",
    "value": 12.2471,
    "value_usd": 51155.89
  }
]
```

This endpoint returns the top 10 transactions (in terms of total BTC sent) flowing out of exchange wallets for every day that the exchange wallets we track have been live on the blockchain.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |
| direction | _string_ | `outflow`                                           |
| exchange  | _string_ | An exchange from the list of ones we support        |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| date       | _string_ | The date in _YYYY-MM-DD_                                 |
| entity    | _string_ | The name of the exchange in question |
| rank     | _integer_ | Ranking out of 10 for the 10 largest transactions of BTC flowing out of the exchange in question on this date.                                             |
| transactionhash | _string_ | The transaction hash of the transaction in question.                                            |
| transactionid  | _string_ | The transaction id of the transaction in question.       |
| value  | _decimal_ | The amount of BTC transferred in this transaction.        |
| value_usd  | _decimal_ | The value in USD of the amount of BTC tranferred in this transaction.        |
