# Ethereum Fundamentals

## ETH On-chain Volume

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&token=eth&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2015-08-07",
    "volume_internal": 39.7,
    "volume_external": 2008602.511431967,
    "volume_gross": 2008642.2114319669,
    "volume_internal_usd": 49.63,
    "volume_external_usd": 2510753.14,
    "volume_gross_usd": 2510802.76
  },
  {
    "date": "2015-08-08",
    "volume_internal": 3568.4341612339426,
    "volume_external": 1681503.1468948552,
    "volume_gross": 1685071.5810560891,
    "volume_internal_usd": 6210.56,
    "volume_external_usd": 2926516.07,
    "volume_gross_usd": 2932726.63
  }
]
```

This endpoint returns the full historical on-chain volume of Ethereum since it went live in 2015. The volume is separated into 'internal' volume and 'external' volume.

'Internal' transactions are transfers of ETH that are initiated by smart contracts. While contracts can't initiate transactions on their own, when certain functions are called on from the outside, the smart contract can generate transfers of ETH towards multiple addresses (other contracts and non-contract addresses). At TokenAnalyst, we track every function call and event that happens on Ethereum and thus we are able to derive an accurate 'internal' ETH on-chain volume. The 'external' transaction volume is that which can be seen on the surface by looking at the blockchain using standard web3 calls - 'normal' ETH transactions included on each block.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `eth`) |

### Data Overview

| Field               | Type      | Description                                                                                                                                                                      |
| ------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| date                | _string_  | The date in _YYYY-MM-DD_                                                                                                                                                         |
| volume_internal     | _decimal_ | The total sum of ETH transferred on this date via value transfers initiated by smart contracts (see <a href="https://www.tokenanalyst.io/faq" target="_blank">here</a> for more) |
| volume_external     | _decimal_ | The total sum of eth transferred in transactions with a timestamp that occurs during this date.                                                                                  |
| volume_gross        | _decimal_ | _volume_internal_ + _volume_external_                                                                                                                                            |
| volume_internal_usd | _decimal_ | _volume_internal_ \* _price_usd_                                                                                                                                                 |
| volume_external_usd | _decimal_ | _volume_external_ \* _price_usd_                                                                                                                                                 |
| volume_gross_usd    | _decimal_ | _volume_gross_ \* _price_usd_                                                                                                                                                    |

## ETH On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&token=eth&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2015-08-07",
    "number_of_txns": 1975
  },
  {
    "date": "2015-08-08",
    "number_of_txns": 2036
  },
  {
    "date": "2015-08-09",
    "number_of_txns": 1249
  }
]
```

This endpoint returns the number of transactions on the full historical Ethereum blockchain for every day since its genesis in 2015.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `eth`) |

### Data Overview

| Field          | Type      | Description                                                                                 |
| -------------- | --------- | ------------------------------------------------------------------------------------------- |
| date           | _string_  | The date in _YYYY-MM-DD_                                                                    |
| number_of_txns | _integer_ | The number of transactions included in blocks with a timestamp that occurs during this date |

## ETH Active addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last?&token=eth&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2015-08-11",
    "active_senders": 2235,
    "active_recipients": 2155
  },
  {
    "date": "2015-08-12",
    "active_senders": 739,
    "active_recipients": 665
  }
]
```

This endpoint returns the active addresses on the Ethereum blockchain for every day of its existence. An address is defined as 'active' if it has transacted during the given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |

### Data Overview

| Field             | Type      | Description                                                                                            |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------ |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                               |
| active_senders    | _integer_ | The total number of distinct addresses that sent ETH in transactions with a timestamp on this date     |
| active_recipients | _integer_ | The total number of distinct addresses that received ETH in transactions with a timestamp on this date |

## ETH Supply

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_supply_historical/last?&token=eth&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2015-07-30",
    "supply": 39311.09375
  },
  {
    "date": "2015-07-31",
    "supply": 75502.8125
  }
]
```

This endpoint returns the historical supply of ETH on the Ethereum blockchain for every day of its existence.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_supply_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |

### Data Overview

| Field  | Type      | Description                                                                             |
| ------ | --------- | --------------------------------------------------------------------------------------- |
| date   | _string_  | The date in _YYYY-MM-DD_                                                                |
| supply | _decimal_ | The cumulative sum of ether (ETH) generated by mining and uncle rewards up to this date |

## ETH NVT

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_nvt_historical/last?&token=eth&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2015-09-02",
    "marketcap_usd": 98056055.37,
    "nvt": 262.7
  },
  {
    "date": "2015-09-03",
    "marketcap_usd": 91877253.74,
    "nvt": 130.9
  }
]
```

This endpoint returns the NVT Ratio (Network Value to Transactions Ratio) for ETH. This is the ratio of the Market Cap divided by the volume transmitted by the blockchain. Special thanks to Willy Woo and Chris Burniske for coming up with it!

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_nvt_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |

### Data Overview

| Field         | Type      | Description                                                                                                         |
| ------------- | --------- | ------------------------------------------------------------------------------------------------------------------- |
| date          | _string_  | The date in _YYYY-MM-DD_                                                                                            |
| marketcap_usd | _decimal_ | The total USD market capitalization of ETH on this date. (_price_usd_ \* _supply_)                                  |
| nvt           | _decimal_ | Ratio comprising the total ETH Market Cap divided by the on-chain volume. (_marketcap_usd_ / _volume_external_usd_) |

## ETH Fees

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_fees_historical/last?&token=eth&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2015-10-19",
    "avg_gas": 32831.1236,
    "avg_gas_price_wei": 52456819761.0774,
    "total_fee": 11.699219139604072,
    "total_fee_usd": 5.85,
    "avg_fee": 0.001771535302786807,
    "avg_fee_usd": 0
  },
  {
    "date": "2015-10-20",
    "avg_gas": 32483.8972,
    "avg_gas_price_wei": 53767556518.0802,
    "total_fee": 11.527019798770482,
    "total_fee_usd": 5.65,
    "avg_fee": 0.001954726097807441,
    "avg_fee_usd": 0
  }
]
```

This endpoint returns the total and average fees spent on the Ethereum network for every day of it's existence. The `total_fee` and the `avg_fee` are denominated in ETH.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_nvt_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |

### Data Overview

| Field             | Type     | Description                                                                                                                                                                                               |
| ----------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_ | The date in _YYYY-MM-DD_                                                                                                                                                                                  |
| avg_gas           | _string_ | The average amount of gas used by transactions that occurred on this date. See <a href="https://www.investopedia.com/terms/g/gas-ethereum.asp" target="_blank">here</a> for a detailed definition of gas. |
| avg_gas_price_wei | _string_ | The average price (in wei) paid per unit of gas for transactions that occurred on this date                                                                                                               |
| total_fee         | _string_ | The sum of fees paid in transactions that occurred on this date. Denominated in ETH. Fees for a transaction are calculated as such: (gas used * gas price)*10^-18                                         |
| total_fee_usd     | _string_ | _total_fee_ \* _price_                                                                                                                                                                                    |
| avg_fee           | _string_ | The average fee paid per transaction that occurred on this date. Denominated in ETH.                                                                                                                      |
| avg_fee_usd       | _string_ | _avg_fee_ \* _price_usd_                                                                                                                                                                                      |

## ETH Miner Hashrate

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_hashrate_historical/last?format=json&token=eth&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2016-04-07",
    "miner": "0x5bD7a5f263fD5B00Fc8047D581fDBa92E34783b8",
    "miner_name": "Unknown",
    "total_daily_hashrate": 1.6977,
    "miner_daily_hashrate": 0.0006,
    "miner_daily_hashrate_pct": 0.0333,
    "miner_daily_block_count": 2,
    "miner_daily_uncle_count": 0,
    "miner_daily_uncle_pct": 0,
    "total_daily_block_count": 5953,
    "total_daily_uncle_count": 403,
    "total_daily_uncle_pct": 6
  },
  {
    "date": "2016-04-07",
    "miner": "0x61C808D82A3Ac53231750daDc13c777b59310bD9",
    "miner_name": "F2Pool 1",
    "total_daily_hashrate": 1.6977,
    "miner_daily_hashrate": 0.1032,
    "miner_daily_hashrate_pct": 6.0811,
    "miner_daily_block_count": 362,
    "miner_daily_uncle_count": 22,
    "miner_daily_uncle_pct": 5,
    "total_daily_block_count": 5953,
    "total_daily_uncle_count": 403,
    "total_daily_uncle_pct": 6
  }
]
```

This endpoint returns the total and miner specifc hashrate and uncle rates. The `total_daily_hashrate` and the `miner_daily_hashrate` are denominated in TH/s. The `total_daily_block_count` is the total number of blocks mined on a given day, and the `miner_daily_block_count` are the number of blocks mined by a specific miner. We do not know the identify of all miners and a lot of them are labelled as unkown

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_miner_hashrate_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |

### Data Overview

| Field                    | Type      | Description                                                                    |
| ------------------------ | --------- | ------------------------------------------------------------------------------ |
| date                     | _string_  | The date in _YYYY-MM-DD_                                                       |
| miner               | _string_  | Public key hash (address) of the miner                   |
| miner_name               | _string_  | Human readable name of the miner in our database, if known.                    |
| total_daily_hashrate     | _decimal_ | The hashrate of the blockchain for the day. Denominated in Th/s.               |
| miner_daily_hashrate     | _decimal_  | The hashrate contribution of the given miner for the day. Denominated in Th/s. |
| miner_daily_hashrate_pct | _decimal_  | The percentage of the daily hashrate contributed by the miner. (_miner_daily_hashrate_/_total_daily_hashrate_)*100                                                                          |
| miner_daily_block_count  | _integer_  | The total number of blocks mined by the miner on this date                            |
| miner_daily_uncle_count  | _integer_  | The total number of uncles mined by the miner on this date                                                                          |
| miner_daily_uncle_pct    | _decimal_  | (_miner_daily_uncle_count_/_miner_daily_block_count_)*100                            |
| total_daily_block_count  | _integer_  | The total number of blocks mined on the blockchain on this date.                                                                          |
| total_daily_uncle_count  | _integer_  | The total number of uncles mined on the blockchain on this date.                            |
| total_daily_uncle_pct    | _decimal_  | (_total_daily_uncle_count_/_total_daily_block_count_)*100                                                                          |

## ETH Miner Rewards

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_rewards_historical/last?format=json&token=eth&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-07-23",
    "miner_name": "Nanopool",
    "miner_daily_block_reward": 1604.3125,
    "miner_daily_block_reward_usd": 359940.49,
    "miner_daily_uncle_reward": 76,
    "miner_daily_uncle_reward_usd": 17051.22
  },
  {
    "date": "2019-07-23",
    "miner_name": "Spark Pool",
    "miner_daily_block_reward": 3048,
    "miner_daily_block_reward_usd": 683843.47,
    "miner_daily_uncle_reward": 141,
    "miner_daily_uncle_reward_usd": 31634.49
  }
]
```

This endpoint returns the daily block rewards and uncle rewards by miner. The `miner_daily_block_reward` and `miner_daily_uncle_reward` are denomiated ETH.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_miner_rewards_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |

### Data Overview

| Field | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| date       | _string_ | The date in _YYYY-MM-DD_                                 |
| miner_name    | _string_ | Human readable name of the miner in our database, if known. |
| miner_daily_block_reward     | _decimal_ | The total amount of block rewards earned by this miner on this date. Denominated in ETH.                                               |
| miner_daily_block_reward_usd     | _decimal_ | _miner_daily_block_reward_ * _price_usd_                                              |
| miner_daily_uncle_reward     | _decimal_ | The total amount of uncle rewards earned by this miner on this date. Denominated in ETH.                                                                         |
| miner_daily_uncle_reward_usd     | _decimal_ | _miner_daily_uncle_reward_ * _price_usd_                                               |
