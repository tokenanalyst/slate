# Ethereum Miner Stats

For Ethereum _Miner Hashrate_ and _Miner Rewards_ endpoints, the supported miners/mining pools in the query parameter `miner` are:

| Miner Name     | `miner`           | 
|----------------|-------------------|
| BitClubPool    | `bitclubpool`     |
| Coinotron3     | `coinotron3`      |
| DwarfPool1     | `dwarfpool1`      |
| Ethermine      | `ethermine`       |
| Ethpool2       | `ethpool2`        |
| F2Pool2        | `f2pool2`         |
| MiningPoolHub  | `miningpoolhub`   |
| NanoPool       | `nanopool`        |
| SparkPool      | `sparkpool`       |
| Zhizhu.top     | `zhizhu-top`      |
| Others         | `others`          |
| Unknown        | `unknown`         |

Miner addresses that we have identified but are not supported have a `miner` name of `others`. Similarly, miner addresses that are unlabelled have a `miner` name of `unknown`

## ETH Miner Hashrate

This endpoint returns the daily miner specific hashrates for all the miners we cover. 
The `hashrate` are denominated in TH/s. The `block_count` are the number of blocks mined by a specific miner.

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_hashrate_window_historical/last?format=json&miner=nanopool&token=eth&window=1d&from_date=2020-01-22&to_date=2020-01-23&limit=2&key=API_KEY"
```
```json
[
  {
    "date": "2020-01-22",
    "hashrate": ,
    "block_count": ,
    "hashrate_pct": 
  },
  {
    "date": "2020-01-23",
    "hashrate": ,
    "block_count": ,
    "hashrate_pct": 
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
| token        | _string_  | `eth`                                                                                     |
| miner        | _miner_   | A miner from the [table](#ethereum-miner-stats) that we support                                                              |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
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

## ETH Miner Rewards

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_rewards_window_historical/last?format=json&miner=nanopool&token=eth&window=1d&from_date=2020-01-22&to_date=2020-01-23&limit=2&key=API_KEY"

```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2020-01-22",
    "block_reward": ,
    "block_reward_usd": 
  },
  {
    "date": "2020-01-23",
    "block_reward": ,
    "block_reward_usd": 
  }
]
```

This endpoint returns the daily rewards earned by all the miners we cover (incl. uncle rewards). The `block_reward` is denominated ETH.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_miner_rewards_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `eth`                                                                                     |
| miner        | _string_  | A miner from the [table](#ethereum-miner-stats) that we support                                                    |
| window       | _string_  | `1d` only. `1h` not supported currently.                                                  |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                        | Type      | Description                                                                              |
| ---------------------------- | --------- | ---------------------------------------------------------------------------------------- |
| date                         | _string_  | The date in _YYYY-MM-DD_                                                                 |
| block_reward                 | _decimal_ | The total amount of block rewards earned by a given miner on this date. Denominated in ETH. |
| block_reward_usd             | _decimal_ | _block_reward_ \* _price_usd_                                                            |

## ETH Miners to Exchanges Full Historical Flows

This endpoint returns the full historical flows of ETH from miners _to_ exchanges that we have labelled.

For Ethereum, the currently supported Exchanges/Miners are:

| Name             | `to_entity`        | `from_entity`                                                    |
| ---------------- | ------------------ | ---------------------------------------------------------------- |
| 2 Miners PPLNS   | `2minerspplns`     | `binance`, `bitfinex`, `bittrex`, `kraken`, `kucoin`             |
| 2 Miners SOLO    | `2minerssolo`      | `binance`, `bittrex`                                             |
| AltPool.Pro      | `altpool-pro`      | `binance`                                                        |
| BTC.COM          | `btc-compool`      | `binance`, `bittrex`, `kraken`                                   |
| Baikalmine       | `baikalmine1`      | `bittrex`                                                        |
| Beeppool         | `beeppool`         | `binance`, `bittrex`                                             |
| Coinotron        | `coinotron3`       | `binance`, `bitfinex`, `bittrex`, `kraken`, `poloniex`           |
| Cruxpool         | `cruxpool`         | `binance`, `kraken`                                              |
| Dwarfpool        | `dwarfpool1`       | `binance`, `bitfinex`, `bittrex`, `kraken`, `kucoin`, `poloniex` |
| eth.solopool.org | `eth-solopool-org` | `binance`, `bittrex`                                             |
| Ethermine        | `ethermine`        | `binance`, `bitfinex`, `bittrex`, `kraken`, `kucoin`, `poloniex` |
| Ethpool          | `ethpool2`         | `binance`, `kraken`                                              |
| F2 Pool          | `f2pool2`          | `binance`, `bitfinex`, `bittrex`, `kraken`, `kucoin`             |
| Minerall         | `minerallpool`     | `binance`, `bittrex`, `kraken`, `poloniex`                       |
| Miningpoolhub    | `miningpoolhub`    | `binance`, `bitfinex`, `bittrex`, `kraken`, `kucoin`             |
| Nanopool         | `nanopool`         | `binance`, `bitfinex`, `bittrex`, `kraken`, `kucoin`, `poloniex` |
| Sparkpool        | `sparkpool`        | `bitfinex`                                                       |
| Uleypool         | `uleypool`         | `binance`                                                        |
| W pool           | `wpool`            | `binance`, `bitfinex`, `bittrex`, `kraken`, `kucoin`             |
| zhizhu.top       | `zhizhu-top`       | `binance`, `bittrex`                                             |

The above table defines supported pairs of the query parameters `to_entity` and `from_entity`.

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?ormat=json&to_entity=binance&from_entity=2miners:%20pplns&token=eth&window=1h&limit=2&key=APIKEY"
```

> The above command returns JSON structured like this:

```json

    {
        "date": "2019-11-27",
        "hour": "08:00:00", // not available when window 1d
        "datetime": "2019-11-17 08:00:00", // not available when window 1d
        "value": 0.05637151,
        "value_usd": 8.26,
        "number_of_txns": 1,
        "avg_txn_value": 0.05637151,
        "avg_txn_value_usd": 8.26
    },
    {
        "date": "2019-11-27",
        "hour": "09:00:00", // not available when window 1d
        "datetime": "2019-11-17 09:00:00", // not available when window 1d
        "value": 0.10035594,
        "value_usd": 14.35,
        "number_of_txns": 2,
        "avg_txn_value": 0.05017797,
        "avg_txn_value_usd": 7.18
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
| token        | _string_  | `eth`                                                                                     |  |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_entity  | _string_  | A miner from the <a href="https://docs.tokenanalyst.io/##eth-miners-to-exchanges-full-historical-flows" target="_self">table</a> that we support                                                    |
| to_entity    | _string_  | An exchange from the <a href="https://docs.tokenanalyst.io/##eth-miners-to-exchanges-full-historical-flows" target="_self">table</a> that we support                                                |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field             | Type      | Description                                                                                                                           |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value     | _decimal_ | The average amount of ETH transferred per transaction into the given exchange on this date.                                           |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of ETH transferred per transaction into the given exchange on this date.                          |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                              |
| datetime \*       | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h` |
| hour \*           | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                          |
| number_of_txns    | _integer_ | The number of transactions sending ETH into an exchange on this date/hour                                                             |
| value             | _decimal_ | The total value of transactions sending ETH into an exchange                                                                          |
| value_usd         | _decimal_ | The USD value of transactions sending ETH into an exchange                                                                            |
