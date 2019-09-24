# Miner Flows

## Miner Full Historical Inflow

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/miner_flow_window_historical/last?token=btc&direction=inflow&window=1h&from_date=2019-02-07&to_date=2019-02-08&format=json&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "avg_txn_value": 12.64279457,
    "avg_txn_value_usd": 46273.01,
    "date": "2019-02-08",
    "datetime": "2019-02-08 23:00:00", // not available when window 1d
    "hour": "23:00:00", // not available when window 1d
    "inflow": 12.64279457,
    "inflow_usd": 46273.01,
    "miner_name": "BTC.TOP",
    "number_of_txns": 1
  },
  {
    "avg_txn_value": 0.01407396,
    "avg_txn_value_usd": 51.51,
    "date": "2019-02-08",
    "datetime": "2019-02-08 23:00:00",
    "hour": "23:00:00",
    "inflow": 0.02814792, // not available when window 1d
    "inflow_usd": 103.02, // not available when window 1d
    "miner_name": "Unknown",
    "number_of_txns": 2
  }
]
```

This endpoint returns the inflow of a given token into miner controlled wallets during the time period specified. Miner wallets are all bitcoin addresses that have _ever_ been the recipient of block rewards. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). Inflow to miner addresses that are unlabelled are returned have a `miner_name` of `"Unknown"`. The `hour` is in UTC

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/miner_flow_window_historical/last?`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc` (only `btc` supported for now)                                                      |
| direction    | _string_  | `inflow`                                                                                  |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

### Data Overview

| Field             | Type      | Description                                                                                                                                 |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value     | _decimal_ | The average amount of tokens transferred per transaction into the given miner on this date/hour.                                            |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of tokens transferred per transaction into the given miner on this date/hour.                           |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                                    |
| datetime \*       | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h` |
| hour \*           | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field field and appears when window is `1h`                          |
| inflow            | _decimal_ | The total amount of the token that flowed into the miner on this date/hour. Denominated in the token in question.                           |
| inflow_usd        | _decimal_ | The USD value of the total amount of the token that flowed into the miner on this date/hour                                                 |
| miner_name        | _string_  | The name of the miner or mining pool in question                                                                                            |
| number_of_txns    | _integer_ | The number of transactions sending the token into this miner on this date/hour.                                                             |

## Miner Full Historical Outflow

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/miner_flow_window_historical/last?token=btc&direction=outflow&window=1h&from_date=2019-02-07&to_date=2019-02-08&format=json&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-02-08",
    "datetime": "2019-02-08 20:00:00", // not available when window 1d
    "hour": "20:00:00", // not available when window 1d
    "miner_name": "SlushPool",
    "outflow": 12.51808781,
    "number_of_txns": 1,
    "avg_txn_value": 12.51808781,
    "outflow_usd": 45818.33,
    "avg_txn_value_usd": 45818.33
  },
  {
    "avg_txn_value": 1.15274538,
    "avg_txn_value_usd": 4186.79,
    "date": "2019-02-08",
    "datetime": "2019-02-08 21:00:00",
    "hour": "21:00:00",
    "miner_name": "Unknown",
    "number_of_txns": 7,
    "outflow": 8.06921768,
    "outflow_usd": 29307.56
  }
]
```

This endpoint returns the outflow of a given token out of miner controlled wallets during the time period specified. Miner wallets are all bitcoin addresses that have _ever_ been the recipient of block rewards. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). Inflow to miner addresses that are unlabelled are returned have a `miner_name` of `"Unknown"`. The `hour` is in UTC.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/miner_flow_window_historical/last?`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc` (only `btc` supported for now)                                                      |
| direction    | _string_  | `inflow`                                                                                  |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

### Data Overview

| Field             | Type      | Description                                                                                                                                 |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value     | _decimal_ | The average amount of tokens transferred per transaction out of the given miner on this date/hour.                                            |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of tokens transferred per transaction out of the given miner on this date/hour.                           |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                                    |
| datetime \*       | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h` |
| hour \*           | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field field and appears when window is `1h`                          |
| outflow            | _decimal_ | The total amount of the token that flowed out of the miner on this date/hour. Denominated in the token in question.                           |
| outflow_usd        | _decimal_ | The USD value of the total amount of the token that flowed out of the miner on this date/hour                                                 |
| miner_name        | _string_  | The name of the miner or mining pool in question                                                                                            |
| number_of_txns    | _integer_ | The number of transactions sending the token out of this miner on this date/hour.                                                             |
