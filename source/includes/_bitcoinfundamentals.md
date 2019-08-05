# Bitcoin Fundamentals

## BTC On-chain Volume

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&key=API_KEY&token=btc"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2009-04-13",
    "volume_gross": 50.0,
    "volume_change": 40.0,
    "volume_real": 10.0,
    "price_usd": "",
    "volume_real_usd": "",
    "volume_change_usd": ""
  },
  {
    "date": "2009-04-18",
    "volume_gross": 182.51,
    "volume_change": 17.49,
    "volume_real": 165.01999999999998,
    "price_usd": "",
    "volume_real_usd": "",
    "volume_change_usd": ""
  }
]
```

This endpoint returns the full historical on-chain volume of Bitcoin since it's genesis in 2009. The volume is separated into 'real' volume and 'change' volume.

Our current heuristic for 'change' related volume is for whenever BTC in a transaction is sent back to the same address that sent the BTC. The 'real' volume is simply the remainder left over after subtracting the change.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `btc`) |


### Data Overview

| Field | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| date       | _string_ | The date                                    |
| volume_gross    | _decimal_ | What this means, how it was calculated, what were the assumptions   |
| volume_change     | _decimal_ | |
| volume_gross    | _decimal_ |    |
| price_usd     | _decimal_ | what is the period |
| volume_real_usd    | _decimal_ |    |
| volume_change_usd     | _decimal_ |  |

## BTC On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&key=API_KEY&token=btc"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2009-03-12",
    "number_of_txns": 119
  },
  {
    "date": "2009-03-13",
    "number_of_txns": 114
  },
  {
    "date": "2009-03-14",
    "number_of_txns": 110
  }
]
```

This endpoint returns the number of transactions on the full historical Bitcoin blockchain for every day since it's genesis in 2009.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `btc`) |

## BTC Active addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last?&token=btc&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2009-01-12",
    "active_senders": 3,
    "active_recipients": 1
  },
  {
    "date": "2009-01-14",
    "active_senders": 3,
    "active_recipients": 0
  }
]
```

This endpoint returns the active addresses on the Bitcoin blockchain for every day of its existence. An address is defined as 'active' if it has transacted during the given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |

## BTC Supply

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_supply_historical/last?&token=btc&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2009-01-12",
    "supply": 50
  },
  {
    "date": "2009-01-13",
    "supply": 750
  }
]
```

This endpoint returns the historical supply of BTC on the Bitcoin blockchain for every day of its existence.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_supply_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |

## BTC NVT

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_nvt_historical/last?&token=btc&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2014-09-24",
    "marketcap_usd": 5708841339.86,
    "nvt": 33.195
  },
  {
    "date": "2014-09-25",
    "marketcap_usd": 5516694629.19,
    "nvt": 35.833
  }
]
```

This endpoint returns the NVT Ratio (Network Value to Transactions Ratio) for BTC. This is the ratio of the Market Cap divided by the volume transmitted by the blockchain. Special thanks to Willy Woo and Chris Burniske for coming up with it!

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_nvt_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |

## BTC Fees

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_fees_historical/last?&token=btc&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2012-08-10",
    "total_fee": 44.53058517,
    "avg_size_bytes": 403,
    "price": 9.1,
    "total_fee_usd": 405.23,
    "avg_satoshis_per_byte": 389,
    "avg_fee": 156935.983,
    "avg_fee_usd": 0.01
  },
  {
    "date": "2012-08-11",
    "total_fee": 19.13775992,
    "avg_size_bytes": 393,
    "price": 9.1,
    "total_fee_usd": 174.15,
    "avg_satoshis_per_byte": 147,
    "avg_fee": 57749.962,
    "avg_fee_usd": 0.01
  }
]
```

This endpoint returns the total and average fees spent on the Bitcoin network for every day of it's existence. The `total_fee` is denominated in Bitcoin, the `price` is the price of Bitcoin on that day, and the `avg_fee` is denominated in Bitcoin.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_fees_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |


## BTC UTXO Age

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_utxo_age_historical/last?format=json&token=btc&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "1-3m": 0.0872,
    "12-18m": 0.1227,
    "18-24m": 0.1173,
    "1d-1w": 0.032,
    "1w-1m": 0.0806,
    "2-3y": 0.0576,
    "3-5y": 0.0586,
    "3-6m": 0.0674,
    "5-10y": 0.1408,
    "6-12m": 0.1448,
    "<1d": 0.0123,
    ">10y": 0.0786,
    "date": "2019-06-10"
  },
  {
    "1-3m": 0.0883,
    "12-18m": 0.1219,
    "18-24m": 0.1179,
    "1d-1w": 0.021,
    "1w-1m": 0.0856,
    "2-3y": 0.0576,
    "3-5y": 0.0586,
    "3-6m": 0.0684,
    "5-10y": 0.1407,
    "6-12m": 0.145,
    "<1d": 0.0162,
    ">10y": 0.0787,
    "date": "2019-06-11"
  }
]
```

This endpoint returns the proportion of the current bitcoin supply held in unspent transaction outputs stratified by their age. For instance outputs in the category `12-18m` are unspent outputs (UTXOs) from transactions that occurred `12-18m` ago. Time is measured relative to blocktime assuming 6 blocks are generated per hour. This means that the proportion of UTXOs in the `<1d` category were generated less than or equal to `144 blocks ago (6 blocks * 24 hours)`.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_utxo_age_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |


## BTC Miner Hashrate

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_hashrate_historical/last?format=json&token=btc&key=API_KEY"
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

This endpoint returns the daily and miner specifc hashrates. The `total_daily_hashrate` and the `miner_daily_hashrate` are denominated in TH/s. The `total_daily_block_count` is the total number of blocks mined on a given day, and the `miner_daily_block_count` are the number of blocks mined by a specific miner. We do not know the identify of all miners and a lot of them are labelled as unkown and grouped together 

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_miner_hashrate_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |


## BTC Miner Rewards

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_rewards_historical/last?format=json&token=btc&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-07-23",
    "miner_name": "SlushPool",
    "miner_daily_block_reward": 51.29584509,
    "price_usd": 10123.41,
    "miner_daily_block_reward_usd": 519288.77897033526
  },
  {
    "date": "2019-07-23",
    "miner_name": "AntPool",
    "miner_daily_block_reward": 37.74736379,
    "price_usd": 10123.41,
    "miner_daily_block_reward_usd": 382131.9722380296
  }
]
```

This endpoint returns the daily coinbase rewards by miner (incl. txn fees). The `miner_daily_block_reward` is denomiated BTC. 

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_miner_rewards_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |
