# Bitcoin Exchange Flows
For Bitcoin currently supported exchanges are: `binance`, `bittrex`, `bitstamp`, `poloniex`, `bitmex`, `bitfinex`

## BTC Full Historical Inflow to Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the inflow of BTC into exchange wallets for as far back as we track. The average inflow is the average transaction value for transactions flowing into exchange wallets on a given day.

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?format=json&token=btc&exchange=binance&direction=inflow&window=1h&limit=2&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2019-09-03",
    "hour": "14:00:00", // not available when window 1d
    "datetime": "2019-09-03 14:00:00", // not available when window 1d
    "avg_txn_value": 1.81428269,
    "avg_txn_value_usd": 19438.16,
    "inflow": 344.71371202,
    "inflow_usd": 3693250.26,
    "number_of_entity_receiving_addresses": 185,
    "number_of_nonentity_sending_addresses": 547,
    "number_of_txns": 190
  },
  {
    "date": "2019-09-03",
    "hour": "15:00:00", // not available when window 1d
    "datetime": "2019-09-03 15:00:00", // not available when window 1d
    "avg_txn_value": 0.48022623,
    "avg_txn_value_usd": 5109.47,
    "inflow": 46.58194403,
    "inflow_usd": 495618.65,
    "number_of_entity_receiving_addresses": 109,
    "number_of_nonentity_sending_addresses": 224,
    "number_of_txns": 97
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?`

### URL Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                                                                     |
| direction    | _string_  | Either `inflow` or `outflow` (in this case `inflow`)                                      |
| exchange     | _string_  | An exchange from the list of ones we support                                              |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                                 | Type      | Description                                                                                                                                                                                                               |
| ------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value                         | _decimal_ | The average amount BTC transferred per transaction into the given exchange on this date.                                                                                                                                  |
| avg_txn_value_usd                     | _decimal_ | The USD value of the average amount of BTC transferred per transaction into the given exchange on this date.                                                                                                              |
| date                                  | _string_  | The date in _YYYY-MM-DD_                                                                                                                                                                                                  |
| datetime *                             | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h`                                                                               |
| hour *                                 | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field field and appears when window is `1h`                                                                                                        |
| inflow                                | _decimal_ | The total amount of BTC that flowed into the entity on this date. Denominated in BTC.                                                                                                                                     |
| inflow_usd                            | _decimal_ | The USD value of the total amount of BTC that flowed into the exchange on this date                                                                                                                                       |
| number_of_entity_receiving_addresses  | _integer_ | The distinct number of wallets identified as belonging to the exchange in question that were on the receiving side of a transaction (where no wallets identified as belonging to the exchange were senders) on this date. |
| number_of_nonentity_sending_addresses | _integer_ | The distinct number of wallets (that don't belong to the exchange in question) that sent Bitcoin to wallets identified as belonging to this exchange on this date.                                                        |
| number_of_txns                        | _integer_ | The number of transactions sending BTC into this exchange on this date.                                                                                                                                                   |

## BTC Full Historical Outflows from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the outflow of BTC from exchange wallets for as far back as we track. The average outflow is the average transaction value for transactions flowing out of exchange wallets on a given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?`

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=btc&exchange=binance&direction=outflow&window=1h&format=json&limit=2&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "avg_txn_value": 26.73,
    "avg_txn_value_usd": 69375.93,
    "date": "2019-09-03",
    "hour": "11:00:00", // not available when window 1d
    "datetime": "2019-09-03 11:00:00", // not available when window 1d
    "number_of_entity_sending_addresses": 23,
    "number_of_nonentity_receiving_addresses": 1,
    "number_of_txns": 3,
    "outflow": 26.73,
    "outflow_usd": 69375.93
  },
  {
    "avg_txn_value": 102.48,
    "avg_txn_value_usd": 241881.49,
    "date": "2019-09-04",
    "hour": "11:00:00", // not available when window 1d
    "datetime": "2019-09-04 11:00:00", // not available when window 1d
    "number_of_entity_sending_addresses": 77,
    "number_of_nonentity_receiving_addresses": 1,
    "number_of_txns": 2,
    "outflow": 102.48,
    "outflow_usd": 241881.49
  }
]
```

### URL Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                                                                     |
| direction    | _string_  | Either `inflow` or `outflow` (in this case `outflow`)                                     |
| exchange     | _string_  | An exchange from the list of ones we support                                              |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                                   | Type      | Description                                                                                                                                                                                                               |
| --------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value                           | _decimal_ | The average amount BTC transferred per transaction out of the given exchange on this date.                                                                                                                                |
| avg_txn_value_usd                       | _decimal_ | The USD value of the average amount of BTC transferred per transaction out of the given exchange on this date.                                                                                                            |
| date                                    | _string_  | The date in _YYYY-MM-DD_                                                                                                                                                                                                  |
| hour *                                   | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field field and appears when window is `1h`                                                                                                        |
| datetime *                               | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h`                                                                               |
| number_of_entity_sending_addresses      | _integer_ | The distinct number of wallets identified as belonging to the exchange in question that were on the sending side of a transaction (where no wallets identified as belonging to the exchange were receivers) on this date. |
| number_of_nonentity_receiving_addresses | _integer_ | The distinct number of wallets (that don't to the exchange in question) that received Bitcoin from wallets identified as belonging to this exchange on this date.                                                         |
| number_of_txns                          | _decimal_ | The number of transactions sending BTC out of this exchange on this date.                                                                                                                                                 |
| outflow                                 | _decimal_ | The total amount of BTC that flowed out of the entity on this date. Denominated in BTC.                                                                                                                                   |
| outflow_usd                             | _decimal_ | The USD value of the total amount of BTC that flowed out of the exchange on this date                                                                                                                                     |

## BTC Full Historical Top 10 Inflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the top 10 transactions (in terms of total BTC sent) flowing into exchange wallets for every day that the exchange wallets we track have been live on the blockchain.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_window_historical/last?`

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_window_historical/last?format=json&token=btc&exchange=bitmex&direction=inflow&window=1d&limit=2&from_date=2019-02-02&to_date=2019-02-08&key=API_KEY"
```

> This is what the response looks like

```json
[
  {
    "date": "2019-02-08",
    "transactionid": "ea6a036eb69f0b3c47ce27cc77a59270d2c0dc99342cdd5f4dcc41cfa1c98298",
    "transaction_datetime": "2019-02-08 16:50:54",
    "rank": 9,
    "value": 50,
    "value_usd": 174539.71
  },
  {
    "date": "2019-02-08",
    "transactionid": "310ff316a1f8d887be851dfaaa14cb829f4d4d225a416ce7cd74a0c032d03c98",
    "transaction_datetime": "2019-02-08 17:21:24",
    "rank": 10,
    "value": 50,
    "value_usd": 174539.71
  }
]
```

### URL Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                                                                     |
| direction    | _string_  | `inflow`                                                                                  |
| exchange     | _string_  | An exchange from the list of ones we support                                              |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field            | Type      | Description                                                                                                  |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------------ |
| date             | _string_  | The date in _YYYY-MM-DD_                                                                                     |
| entity           | _string_  | The name of the exchange in question                                                                         |
| rank             | _integer_ | Ranking out of 10 for the 10 largest transactions of BTC flowing into the exchange in question on this date. |
| transaction_time | _string_  | The timestamp in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone) when the transaction was mined          |
| transactionhash  | _string_  | The transaction hash of the transaction in question.                                                         |
| transactionid    | _string_  | The transaction id of the transaction in question.                                                           |
| value            | _decimal_ | The amount of BTC transferred in this transaction.                                                           |
| value_usd        | _decimal_ | The value in USD of the amount of BTC tranferred in this transaction.                                        |

## BTC Full Historical Top 10 Outflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_window_historical/last?format=json&token=btc&exchange=bitmex&direction=outflow&window=1d&limit=2&from_date=2019-02-02&to_date=2019-02-08&key=API_KEY"
```

> This is what the response looks like

```json
[
  {
    "date": "2019-02-08",
    "transactionid": "bdf372897349b7103ed48c56e6bf0cfd44df854b4e3fc6cb6ce6b106360d0c2f",
    "transaction_datetime": "2019-02-08 18:50:53",
    "rank": 9,
    "value": 8,
    "value_usd": 27926.35
  },
  {
    "date": "2019-02-08",
    "transactionid": "fcca2b0d59d640c5ba6bade0c32936d4ad512865b5e9e602ddce1da745d589e2",
    "transaction_datetime": "2019-02-08 18:50:53",
    "rank": 10,
    "value": 7.71,
    "value_usd": 26897.2
  }
]
```

This endpoint returns the top 10 transactions (in terms of total BTC sent) flowing out of exchange wallets for every day that the exchange wallets we track have been live on the blockchain. Note: Currently Bitstamp and Binance are not supported for this endpoint

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_window_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |
| direction | _string_ | `outflow`                                           |
| exchange  | _string_ | An exchange from the list of ones we support        |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field            | Type      | Description                                                                                                    |
| ---------------- | --------- | -------------------------------------------------------------------------------------------------------------- |
| date             | _string_  | The date in _YYYY-MM-DD_                                                                                       |
| entity           | _string_  | The name of the exchange in question                                                                           |
| rank             | _integer_ | Ranking out of 10 for the 10 largest transactions of BTC flowing out of the exchange in question on this date. |
| transaction_time | _string_  | The timestamp in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone) when the transaction was mined            |
| transactionhash  | _string_  | The transaction hash of the transaction in question.                                                           |
| transactionid    | _string_  | The transaction id of the transaction in question.                                                             |
| value            | _decimal_ | The amount of BTC transferred in this transaction.                                                             |
| value_usd        | _decimal_ | The value in USD of the amount of BTC tranferred in this transaction.                                          |
