# Bitcoin Miner Stats

For Bitcoin _Miner Hashrate_, _Miner Rewards_, _Miner Historical Inflow_, _Miner Historical Outflow_ and _Miner Balances_ endpoints, the supported miners/mining pools in the query parameter `miner` are:

| Miner Name     | `miner`           | 
|----------------|-------------------|
| Antpool        | `antpool`         |
| BTC.TOP        | `btc-top`         |
| BTC-com        | `btc-com`         |
| BitFury        | `bitfury`         |
| F2Pool         | `f2pool`          |
| Huobi Pool     | `huobi-pool`      |
| Poolin         | `poolin`          |
| SlushPool      | `slushpool`       |
| viaBTC         | `viabtc`          |
| 1THash&58coin  | `1thash%2658coin` |
| Others †       | `others`          |
| Unknown †      | `unknown`         |

Miner addresses that we have identified but are not supported have a `miner` name of `others`. Similarly, miner addresses that are unlabelled have a `miner` name of `unknown`

Note: All miners with a † are not supported for _Miner Balances_ endpoint.

## BTC Miner Hashrate

This endpoint returns the daily miner specific hashrates for all the miners we cover. The `hashrate` are denominated in TH/s. The `block_count` are the number of blocks mined by a specific miner.


<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_hashrate_window_historical/last?format=json&miner=antpool&token=btc&window=1d&from_date=2020-01-22&to_date=2020-01-23&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2020-01-22",
    "hashrate": 13956207.0726,
    "block_count": 19,
    "hashrate_pct": 12.1795
  },
  {
    "date": "2020-01-23",
    "hashrate": 12487132.6439,
    "block_count": 17,
    "hashrate_pct": 10.6918
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_miner_hashrate_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                                                                     |
| miner        | _string_  | A miner from the [table](#bitcoin-miner-stats) that we support     |
| window       | _string_  | `1d` only. `1h` not supported currently.                                                    |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                    | Type      | Description                                                                                                         |
| ------------------------ | --------- | ------------------------------------------------------------------------------------------------------------------- |
| date                     | _string_  | The date in _YYYY-MM-DD_                                                                                            |
| hashrate                 | _decimal_ | The hashrate contribution of a given miner for the day. Denominated in Th/s.                                      |
| block_count              | _integer_ | The total number of blocks mined by a given miner on this date                                                          |
| hashrate_pct             | _decimal_ | The percentage of the daily hashrate contributed by the miner. (_miner_daily_hashrate_/_total_daily_hashrate_)\*100 |

## BTC Miner Rewards

This endpoint returns the daily coinbase rewards earned by all the miners we cover (incl. txn fees). The `block_reward` is denominated BTC.

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/token_rewards_hashrate_window_historical/last?format=json&miner=antpool&token=btc&window=1d&from_date=2020-01-22&to_date=2020-01-23&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2020-01-22",
    "block_reward": 240.2266818,
    "block_reward_usd": 2086207.8
  },
  {
    "date": "2020-01-23",
    "block_reward": 215.34830001,
    "block_reward_usd": 1816345.79
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_miner_rewards_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                                                                     |
| miner        | _string_  | A miner from the [table](#bitcoin-miner-stats) that we support                                                    |
| window       | _string_  | `1d` only. `1h` not supported currently.                                                  |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                        | Type      | Description                                                                              |
| ---------------------------- | --------- | ---------------------------------------------------------------------------------------- |
| date                         | _string_  | The date in _YYYY-MM-DD_                                                                 |
| block_reward                 | _decimal_ | The total amount of block rewards earned by a given miner on this date. Denominated in BTC. |
| block_reward_usd             | _decimal_ | _block_reward_ \* _price_usd_                                                            |

## BTC Miner Full Historical Inflow

This endpoint returns the inflow of a given token into miner controlled wallets during the time period specified. Miner wallets are all bitcoin addresses that have _ever_ been the recipient of block rewards. The `avg_txn_value`, `inflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). The `hour` is in UTC.

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/miner_flow_window_historical/last?token=btc&direction=inflow&window=1h&miner=f2pool&from_date=2019-02-07&to_date=2019-02-08&format=json&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-02-08",
    "hour": "19:00:00", // not available when window 1d
    "datetime": "2019-02-08 19:00:00", // not available when window 1d
    "inflow": 12.79939595,
    "inflow_usd": 46978.65,
    "number_of_txns": 1,
    "avg_txn_value": 12.79939595,
    "avg_txn_value_usd": 46978.65,
  },
  {
    "date": "2019-02-08",
    "hour": "20:00:00", // not available when window 1d
    "datetime": "2019-02-08 20:00:00", // not available when window 1d
    "inflow": 12.56972757,
    "inflow_usd": 46007.34,
    "number_of_txns": 1,
    "avg_txn_value": 12.56972757,
    "avg_txn_value_usd": 46007.34,
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
| token        | _string_  | `btc`                                                                                     |
| direction    | _string_  | `inflow`                                                                                  |
| window       | _string_  | `1h` or `1d`                                                                              |
| miner        | _string_  | A miner from the [table](#bitcoin-miner-stats) that we support                                                    |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field             | Type      | Description                                                                                                                                 |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                                    |
| hour \*           | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                |
| datetime \*       | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`       |
| inflow            | _decimal_ | The total amount of BTC that flowed into the miner on this date/hour.                                                                       |
| inflow_usd        | _decimal_ | The USD value of the total amount of BTC that flowed into the miner on this date/hour                                                       |
| number_of_txns    | _integer_ | The number of transactions sending BTC into this miner on this date/hour.                                                                   |
| avg_txn_value     | _decimal_ | The average amount of BTC transferred per transaction into the given miner on this date/hour.                                               |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of BTC transferred per transaction into the given miner on this date/hour.                              |

## BTC Miner Full Historical Outflow

This endpoint returns the outflow of a given token out of miner controlled wallets during the time period specified. Miner wallets are all bitcoin addresses that have _ever_ been the recipient of block rewards. The `avg_txn_value`, `outflow`, and `number_of_txns` are calculated over the window (either 1 hour or 1 day). The `hour` is in UTC.

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/miner_flow_window_historical/last?token=btc&direction=outflow&window=1h&miner=slushpool&from_date=2019-01-01&to_date=2019-01-02&format=json&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-01-01",
    "hour": "11:00:00", // not available when window 1d
    "datetime": "2019-01-01 11:00:00", // not available when window 1d
    "outflow": 12.52530201,
    "outflow_usd": 46992.93,
    "number_of_txns": 1,
    "avg_txn_value": 12.52530201,
    "avg_txn_value_usd": 46992.93,
  },
  {
    "date": "2019-01-01",
    "hour": "12:00:00", // not available when window 1d
    "datetime": "2019-01-01 12:00:00", // not available when window 1d
    "outflow": 12.53417305,
    "outflow_usd": 47204.95,
    "number_of_txns": 1,
    "avg_txn_value": 12.53417305,
    "avg_txn_value_usd": 47204.95,
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
| token        | _string_  | `btc`                                                                                     |
| direction    | _string_  | `outflow`                                                                                 |
| window       | _string_  | `1h` or `1d`                                                                              |
| miner        | _string_  | A miner from the [table](#bitcoin-miner-stats) that we support                                                    |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

### Data Overview

| Field             | Type      | Description                                                                                                                                 |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                                    |
| hour \*           | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                |
| datetime \*       | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`       |
| outflow           | _decimal_ | The total amount of BTC that flowed out of the miner on this date/hour. Denominated in BTC.                                                 |
| outflow_usd       | _decimal_ | The USD value of the total amount of BTC that flowed out of the miner on this date/hour                                                     |
| number_of_txns    | _integer_ | The number of transactions sending BTC out of this miner on this date/hour.                                                                 |
| avg_txn_value     | _decimal_ | The average amount of BTC transferred per transaction out of the given miner on this date/hour.                                             |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of BTC transferred per transaction out of the given miner on this date/hour.                            |

## BTC Miners to Exchanges Full Historical Flows

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
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?window=1d&limit=2&from_entity=slushpool&to_entity=binance&format=json&token=btc&key=API_KEY"
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
| from_entity  | _string_  | A miner from the <a href="https://docs.tokenanalyst.io/#btc-miners-to-exchanges-full-historical-flows" target="_self">table</a> that we support
| to_entity    | _string_  | An exchange from the <a href="https://docs.tokenanalyst.io/#btc-miners-to-exchanges-full-historical-flows" target="_self">table</a> that we support
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

## BTC Miner Balances

This endpoint returns the balance of BTC held in the wallets of miners that we support for the full history of the miner in question.

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/miner_balance_window_historical/last?token=btc&window=1h&miner=slushpool&from_date=2019-01-01&to_date=2019-02-08&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-01-01",
    "hour": "00:00:00", // not available when window 1d
    "datetime": "2019-01-01 00:00:00", // not available when window 1d
    "balance": 1000.50560683,
    "balance_usd": 3752806.49
  },
  {
    "date": "2019-01-01",
    "hour": "01:00:00", // not available when window 1d
    "datetime": "2019-01-01 01:00:00", // not available when window 1d
    "balance": 997.17045289,
    "balance_usd": 3725528.53
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/miner_balance_window_historical/last?`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                                                                     |
| window       | _string_  | `1h` or `1d`                                                                              |
| miner        | _string_  | A miner from the <a href="https://docs.tokenanalyst.io/#bitcoin-miner-stats" target="_self">table</a> that we support                                                    |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field             | Type      | Description                                                                                                                                 |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                                    |
| hour \*           | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                |
| datetime \*       | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`       |
| balance           | _decimal_ | The amount of BTC for a given miner on this date.                                                                                           |
| balance_usd       | _decimal_ | The USD value of the amount of BTC for a given miner on this date.                                                                          |
