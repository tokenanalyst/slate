# Bitcoin Miner Stats

For Bitcoin _Miner Hashrate_, _Miner Rewards_, _Miner Historical Inflow_ and _Miner Historical Outflow_ endpoints, the supported miners/mining pools in the field `miner_name` are:

| `miner_name`     |
|------------------|
| `Antpool`        |
| `BTC.TOP`        |
| `BitClubNetwork` |
| `F2Pool `        |
| `SlushPool`      |
| `viaBTC`         |
| `Unknown  `      |

## Miner Hashrate

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_hashrate_window_historical/last?format=json&window=1d&token=btc&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-07-22",
    "miner_name": "F2 Pool",
    "miner_daily_block_count": 19,
    "total_daily_block_count": 322,
    "miner_daily_hashrate": 8561054.749877952,
    "total_daily_hashrate": 71191928.97266929,
    "miner_daily_hashrate_pct": 12.025316455696203
  },
  {
    "date": "2019-07-22",
    "miner_name": "AntPool",
    "miner_daily_block_count": 18,
    "total_daily_block_count": 322,
    "miner_daily_hashrate": 8110472.920937006,
    "total_daily_hashrate": 71191928.97266929,
    "miner_daily_hashrate_pct": 11.392405063291138
  }
]
```

This endpoint returns the daily miner specific hashrates for all the miners we cover. The `total_daily_hashrate` and the `miner_daily_hashrate` are denominated in TH/s. The `total_daily_block_count` is the total number of blocks mined on a given day, and the `miner_daily_block_count` are the number of blocks mined by a specific miner. We do not know the identify of all miners and a lot of them are labelled as unknown and grouped together.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_miner_hashrate_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                                                                     |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                    | Type      | Description                                                                                                         |
| ------------------------ | --------- | ------------------------------------------------------------------------------------------------------------------- |
| date                     | _string_  | The date in _YYYY-MM-DD_                                                                                            |
| miner_name               | _string_  | Human readable name of the miner in our database, if known.                                                         |
| miner_daily_block_count  | _integer_ | The total number of blocks mined by the miner on this date                                                          |
| total_daily_block_count  | _integer_ | The total number of blocks mined on the blockchain on this date.                                                    |
| miner_daily_hashrate     | _decimal_ | The hashrate contribution of the given miner for the day. Denominated in Th/s.                                      |
| total_daily_hashrate     | _decimal_ | The hashrate of the blockchain for the day. Denominated in Th/s.                                                    |
| miner_daily_hashrate_pct | _decimal_ | The percentage of the daily hashrate contributed by the miner. (_miner_daily_hashrate_/_total_daily_hashrate_)\*100 |

## Miner Rewards

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_rewards_window_historical/last?format=json&token=btc&window=1d&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-10-16",
    "miner_name": "unknown",
    "miner_daily_block_reward": 571.6431,
    "miner_daily_block_reward_usd": 4620304.75
  },
  {
    "date": "2019-10-16",
    "miner_name": "viaBTC",
    "miner_daily_block_reward": 164.9395,
    "miner_daily_block_reward_usd": 1333123.7
  }
]
```

This endpoint returns the daily coinbase rewards earned by all the miners we cover (incl. txn fees). The `miner_daily_block_reward` is denominated BTC.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_miner_rewards_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                                                                     |
| window       | _string_  | `1d` only. `1h` not supported currently.                                                  |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                        | Type      | Description                                                                              |
| ---------------------------- | --------- | ---------------------------------------------------------------------------------------- |
| date                         | _string_  | The date in _YYYY-MM-DD_                                                                 |
| miner_name                   | _string_  | Human readable name of the miner in our database, if known.                              |
| miner_daily_block_reward     | _decimal_ | The total amount of block rewards earned by this miner on this date. Denominated in BTC. |  |
| miner_daily_block_reward_usd | _decimal_ | _miner_daily_block_reward_ \* _price_usd_                                                |


Miner addresses that are unlabelled have a `miner_name` of `"Unknown"`.

## Miner Full Historical Inflow

This endpoint returns the inflow of a given token into miner controlled wallets during the time period specified. Miner wallets are all bitcoin addresses that have _ever_ been the recipient of block rewards. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). The `hour` is in UTC.


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
    "datetime": "2019-02-08 23:00:00", // not available when window 1d
    "hour": "23:00:00", // not available when window 1d
    "inflow": 0.02814792,
    "inflow_usd": 103.02,
    "miner_name": "Unknown",
    "number_of_txns": 2
  }
]
```

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
| datetime \*       | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h` |
| hour \*           | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                          |
| inflow            | _decimal_ | The total amount of the token that flowed into the miner on this date/hour. Denominated in the token in question.                           |
| inflow_usd        | _decimal_ | The USD value of the total amount of the token that flowed into the miner on this date/hour                                                 |
| miner_name        | _string_  | The name of the miner or mining pool from the table above.                                                                                            |
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
    "datetime": "2019-02-08 21:00:00", // not available when window 1d
    "hour": "21:00:00", // not available when window 1d
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
| datetime \*       | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h` |
| hour \*           | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                          |
| outflow            | _decimal_ | The total amount of the token that flowed out of the miner on this date/hour. Denominated in the token in question.                           |
| outflow_usd        | _decimal_ | The USD value of the total amount of the token that flowed out of the miner on this date/hour                                                 |
| miner_name        | _string_  | The name of the miner or mining pool from the table above                                                                                            |
| number_of_txns    | _integer_ | The number of transactions sending the token out of this miner on this date/hour.                                                             |

## Miners to Exchanges Full Historical Flows

This endpoint returns the full historical flows of BTC from miners *to* exchanges that we have labelled.


For Bitcoin, the currently supported Miners/Exchanges are:

| Name           | `from_entity`    | `to_entity`                                                                           |
|----------------|------------------|---------------------------------------------------------------------------------------|
| AntPool        | `antpool`        | `bitstamp`, `bittrex`                                                                 |
| BTC.TOP        | `btc.top`        | `binance`, `bitfinex`, `bitmex`, `bitstamp`, `bittrex`, `huobi`, `kraken`, `okex`, `poloniex` |    
| BitClubNetwork | `bitclubnetwork` | `bitfinex`, `bitstamp`                                                                |
| F2Pool         | `f2pool`         | `binance`, `bitfinex`, `bitstamp`, `bittrex`, `huobi`, `kraken`, `okex`, `poloniex`           |
| SlushPool      | `slushpool`      | `binance`, `bitfinex`, `bitmex`, `bitstamp`, `bittrex`, `huobi`, `kraken`, `poloniex` |
| viaBTC         | `viabtc`         | `bitmex`, `bitstamp`, `bittrex`, `huobi`, `poloniex`                                  |

The above table defines supported pairs of the query parameters `from_entity` and `to_entity`. 

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>


```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?window=1d&limit=2&from_entity=slushpool&to_entity=binance&format=json&token=btc&key=APIKEY"
```

> The above command returns JSON structured like this:

```json
[
    {
        "date": "2019-10-05",
        "value": 2.80564686,
        "value_usd": 22805.88,
        "number_of_txns": 9,
        "avg_txn_value": 0.31173854,
        "avg_txn_value_usd": 2533.99
    },
    {
        "date": "2019-10-06",
        "value": 1.90917571,
        "value_usd": 15287.62,
        "number_of_txns": 8,
        "avg_txn_value": 0.23864696,
        "avg_txn_value_usd": 1910.95
    }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                                                                     |                                       |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_entity  | _string_  | A miner from the table that we support
| to_entity    | _string_  | An exchange from the table that we support
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                                   | Type      | Description                                                                                                                                                                                                               |
| --------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value                           | _decimal_ | The average amount of BTC transferred per transaction into the given exchange on this date.                                                                                                                                  |
| avg_txn_value_usd                       | _decimal_ | The USD value of the average amount of BTC transferred per transaction into the given exchange on this date.                                                                                                          |
| date                                    | _string_  | The date in _YYYY-MM-DD_                                                                                                                                                                                                  |
| datetime *                              | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`                                                                               |
| hour *                                  | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                                                                                        |
| number_of_txns                          | _integer_ | The number of transactions sending BTC into an exchange on this date/hour
| value                                   | _decimal_ | The total value of transactions sending BTC into an exchange
| value_usd                               | _decimal_ | The USD value of transactions sending BTC into an exchange