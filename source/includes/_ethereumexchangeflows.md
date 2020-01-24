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
| hour *   | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                                                                                        |
| datetime *  | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`                                                                               |
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
| hour *   | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                                                                                        |
| datetime * | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`                                                                               |
| outflow  | _decimal_ | The total amount of ETH that flowed out of the exchange on this date. Denominated in ETH.         |
| outflow_usd  | _decimal_ | The USD value of the total amount of ETH that flowed out of the exchange on this date         |
| number_of_txns       | _integer_ | The number of transactions sending ETH out of this exchange on this date.                                 |
| avg_txn_value       | _decimal_ | The average amount ETH transferred per transaction out of the given exchange on this date.                                 |
| avg_txn_value_usd    | _decimal_ | The USD value of the average amount of ETH transferred per transaction out of the given exchange on this date.    |

## ETH Exchange to Exchange Flows

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the full historical inter-flows from an exchange *to* another exchange that we have labelled.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?`

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?format=json&token=eth&window=1h&from_date=2019-12-04&to_date=2019-12-04&limit=2&from_entity=binance&to_entity=kucoin&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2019-12-04",
    "hour": "07:00:00", // not available when window 1d
    "datetime": "2019-12-04 07:00:00", // not available when window 1d
    "value": 0.1317,
    "value_usd": 19.06,
    "number_of_txns": 1,
    "avg_txn_value": 0.1317,
    "avg_txn_value_usd": 19.06
  },
  {
    "date": "2019-12-04",
    "hour": "08:00:00", // not available when window 1d
    "datetime": "2019-12-04 08:00:00", // not available when window 1d
    "value": 0.2382,
    "value_usd": 34.58,
    "number_of_txns": 1,
    "avg_txn_value": 0.2382,
    "avg_txn_value_usd": 34.58
  }
]
```

### URL Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `eth`                                                                                     |                                                                             |
| window       | _string_  | `1h` or `1d`                                                                           |
| from_entity  | _string_  | An exchange from the table that we support
| to_entity    | _string_  | An exchange from the table that we support. Cannot be the same as ```from_entity```       |                                                 |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field             | Type      | Description                                                                                                  |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------ |
| avg_txn_value     | _decimal_ | The average amount ETH transferred per transaction out of the given exchange to another exchange on this date.                    |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of ETH transferred per transaction out of the given exchange to another exchange on this date.|
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                     |
| datetime *        | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`        |
| hour *            | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                 |
| number_of_txns    | _integer_ | The number of transactions sending ETH into from an exchange to another exchange on this date.                                       |
| value             | _decimal_ | The amount of ETH transferred in this transaction.                                                            |
| value_usd         | _decimal_ | The value in USD of the amount of ETH transferred in this transaction.                                         |

## ETH Full Historical Static Flows to Exchanges

<img src="https://img.shields.io/badge/Tier-Enterprise-blueviolet.svg"/>

This endpoint returns _static_ flows of ETH into exchange wallets for as far back as we track. What do we mean by static? while our standard API endpoint as seen <a href="https://docs.tokenanalyst.io/#eth-full-historical-flows-into-exchanges" target="_blank">above</a> dynamically updates the data (up to 7 days prior to the current day) when we find new information on exchange wallets, the historical data from this data _never_ changes from the time it is posted. The rationale for this is to serve a snapshot look of what was known at the specific point in time - to aid in effective backtesting and inputs for ML models. This is suited for users who want to use our websocket. 

<aside class="notice">
The static endpoint lags behind the tip of the chain by 2 hours in order to leave time to for our internal algorithms classify wallets definitively. This is important because the data in this endpoint does not change after it is posted (unlike the other endpoints).
</aside>

For this reason, as an extra reinforcement, this endpoint includes the `last_updated` field to show the time in UTC when the data point was last modified. Additionally, there is a `lag` parameter that needs to be explicitly included with the option of `hour` - which signifies the default 2 hour lag.

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
| lag          | _string_  | `hour` (default two hour lag)              |
| window       | _string_  | `1h`                                                                          |
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
| datetime *                             | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`                                                                               |
| hour *                                 | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                                                                                        |
| inflow                                | _decimal_ | The total amount of ETH that flowed into the exchange on this date. Denominated in ETH.                                                                                                                                     |
| inflow_usd                            | _decimal_ | The USD value of the total amount of ETH that flowed into the exchange on this date                                                                                                                                       |
| number_of_txns                        | _integer_ | The number of transactions sending ETH into this exchange on this date.                                                                                                                                                   |
| last_updated                          | _string_  | The date when the endpoint was last updated in `UTC` datetime format
