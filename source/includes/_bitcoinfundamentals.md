# Bitcoin Fundamentals

<aside class="warning">
Please switch to the Bitcoin Fundamentals <code>V2</code> endpoint. Bitcoin Fundamentals <code>V1</code> is no longer updated.
</aside>

## BTC On-chain Volume

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

This endpoint returns the full historical on-chain volume of Bitcoin since it's genesis in 2009. The volume is separated into 'real' volume and 'change' volume.

Our current heuristic for 'change' related volume is for whenever BTC in a transaction
is sent back to the same address that sent the BTC. The 'real' volume is simply the
remainder left over after subtracting the change.

```shell
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&key=API_KEY&token=btc"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2014-02-04",
    "price_usd": 841.73,
    "volume_change": 60604.1,
    "volume_change_usd": 51012300,
    "volume_gross": 788252,
    "volume_real": 727648,
    "volume_real_usd": 612483000
  },
  {
    "date": "2014-02-05",
    "price_usd": 893.72,
    "volume_change": 152871,
    "volume_change_usd": 136624000,
    "volume_gross": 771870,
    "volume_real": 618999,
    "volume_real_usd": 553212000
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `btc`) |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field             | Type      | Description                                                                                                                                        |
| ----------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                                           |
| price_usd         | _decimal_ | The daily average price of BTC in USD (the daily mean of minute-level price data)                                                                  |
| volume_change     | _decimal_ | The total sum of BTC sent to (locked by) addresses that were also on the sending side of the same transaction                                      |
| volume_change_usd | _decimal_ | _volume_change_ \* _price_usd_                                                                                                                     |
| volume_gross      | _decimal_ | The total sum of BTC sent by (unlocked by) addresses in transactions with a timestamp that occurs on this date. Does not include coinbase rewards. |
| volume_real       | _decimal_ | _volume_gross_ - _volume_change_                                                                                                                   |
| volume_real_usd   | _decimal_ | _volume_real_ \* _price_usd_                                                                                                                       |

---

## BTC On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

This endpoint returns the daily number of transactions on the full historical Bitcoin blockchain
for every day since it's genesis in 2009.

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

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `btc`) |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field          | Type      | Description                                                                                                                  |
| -------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------- |
| date           | _string_  | The date in _YYYY-MM-DD_                                                                                                     |
| number_of_txns | _integer_ | The number of transactions included in blocks with a timestamp that occurs during this date (includes coinbase transactions) |

---

## BTC Active addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

This endpoint returns the daily number of active addresses on the Bitcoin blockchain for each day
of its existence. An address is defined as 'active' if it has sent or received bitcoin
in a transaction with a timestamp on that day. Only the distinct number of addresses are
counted, i.e. an address which sends thousands of transactions per day is only counted once
as an _active_sender_ with the same logic applied to distinct receiving addresses.

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

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field             | Type      | Description                                                                                            |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------ |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                               |
| active_senders    | _integer_ | The total number of distinct addresses that sent BTC in transactions with a timestamp on this date     |
| active_recipients | _integer_ | The total number of distinct addresses that received BTC in transactions with a timestamp on this date |

---

## BTC Supply

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

This endpoint returns the historical supply of BTC on the Bitcoin blockchain for each day
of its existence. This is the sum of BTC paid out in coinbase rewards.

Since there is no
requirement for a miner who successfully mines a block to pay themselves any or all of the
block reward, we cannot simply multiply the number of blocks by the current reward level for
those block(s). There have been instances where no coinbase reward was claimed at all, meaning
those bitcoins are lost from the total supply forever.

The supply generated by each mined block is the sum of the outputs (which includes the value of
any coinbase reward up to the maximum permissible claimed by the miner), minus the sum of the
inputs sent in that block.

This metric includes bitcoins that have been locked by so-called 'burn' addresses (addresses
for which there is likely no known private key hence those bitcoins are also lost forever).
An example of this is the lowest possible bitcoin address of `1111111111111111111114oLvT2`.

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

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_supply_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field  | Type     | Description                                                              |
| ------ | -------- | ------------------------------------------------------------------------ |
| date   | _string_ | The date in _YYYY-MM-DD_                                                 |
| supply | _float_  | The cumulative sum of bitcoins generated by mined blocks up to this date |

---

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
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field         | Type      | Description                                                                                                         |
| ------------- | --------- | ------------------------------------------------------------------------------------------------------------------- |
| date          | _string_  | The date in _YYYY-MM-DD_                                                                                            |
| marketcap_usd | _decimal_ | The total USD market capitalization of BTC on this date. (_price_usd_ \* _supply_)                                  |
| nvt           | _decimal_ | Ratio comprising the total BTC Market Cap divided by the on-chain volume. (_marketcap_usd_ / _volume_real_usd_) |

## BTC Fees

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_fees_historical/last?&token=btc&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-08-13",
    "total_fee": 75.09047834,
    "avg_size_bytes": 503,
    "total_fee_usd": 837178.32,
    "avg_satoshis_per_byte": 40,
    "avg_fee": 0.0002,
    "avg_fee_usd": 2.26
  },
  {
    "date": "2019-08-14",
    "total_fee": 58.70170397,
    "avg_size_bytes": 481,
    "total_fee_usd": 613648.29,
    "avg_satoshis_per_byte": 34,
    "avg_fee": 0.0002,
    "avg_fee_usd": 1.7
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
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field                 | Type      | Description                                                                                       |
| --------------------- | --------- | ------------------------------------------------------------------------------------------------- |
| date                  | _string_  | The date in _YYYY-MM-DD_                                                                          |
| total_fee             | _decimal_ | The total amount of fees paid by all transactions that occurred on this date. Denominated in BTC. |
| avg_size_bytes        | _integer_ | The average transaction size to the nearest byte for transactions that occurred on this date.     |
| total_fee_usd         | _decimal_ | _total_fee_ \* _price_                                                                            |
| avg_satoshis_per_byte | _integer_ | The average number of satoshis paid per byte for transactions that occurred on this date          |
| avg_fee               | _decimal_ | The average amount of fees paid per transaction that occurred on this date. Denominated in BTC.   |
| avg_fee_usd           | _decimal_ | _avg_fee_ \* _price_usd_                                                                              |

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
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field  | Type      | Description                                                                                                                                         |
| ------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1-3m   | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred 1 to 3 months prior to this date.         |
| 12-18m | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred 12 to 18 months prior to this date.       |
| 18-24m | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred 18 to 24 months prior to this date.       |
| 1d-1w  | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred 1 day to 1 week prior to this date.       |
| 1w-1m  | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred 1 week to 1 month prior to this date.     |
| 2-3y   | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred 2 to 3 years prior to this date.          |
| 3-5y   | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred 3 to 5 years prior to this date.          |
| 3-6m   | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred 3 to 6 months prior to this date.         |
| 5-10y  | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred 5 to 10 years prior to this date.         |
| 6-12m  | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred 6 to 12 months prior to this date.        |
| <1d    | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred less than a day prior to this date.       |
| >10y   | _decimal_ | Proportion of bitcoin supply on this date held in unspent outputs (UTXOs) from transactions that occurred greater than 10 years prior to this date. |
| date   | _string_  | The date in _YYYY-MM-DD_                                                                                                                            |

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
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field                    | Type     | Description                                                                                                         |
| ------------------------ | -------- | ------------------------------------------------------------------------------------------------------------------- |
| date                     | _string_ | The date in _YYYY-MM-DD_                                                                                            |
| miner_name               | _string_ | Human readable name of the miner in our database, if known.                                                         |
| miner_daily_block_count  | _integer_ | The total number of blocks mined by the miner on this date                                                          |
| total_daily_block_count  | _integer_ | The total number of blocks mined on the blockchain on this date.                                                    |
| miner_daily_hashrate     | _decimal_ | The hashrate contribution of the given miner for the day. Denominated in Th/s.                                      |
| total_daily_hashrate     | _decimal_ | The hashrate of the blockchain for the day. Denominated in Th/s.                                                    |
| miner_daily_hashrate_pct | _decimal_ | The percentage of the daily hashrate contributed by the miner. (_miner_daily_hashrate_/_total_daily_hashrate_)\*100 |

## BTC Miner Rewards

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_rewards_historical/last?format=json&token=btc&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-07-27",
    "miner_name": "AntPool",
    "miner_daily_block_reward": 239.4406,
    "miner_daily_block_reward_usd": 1920851.96
  },
  {
    "date": "2018-07-27",
    "miner_name": "BTC.TOP",
    "miner_daily_block_reward": 213.9951,
    "miner_daily_block_reward_usd": 1716721.89
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
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field                        | Type     | Description                                         |
| ---------------------------- | -------- | --------------------------------------------------- |
| date                         | _string_ | The date in _YYYY-MM-DD_                                 |
| miner_name                   | _string_ | Human readable name of the miner in our database, if known. |
| miner_daily_block_reward                    | _decimal_ | The total amount of block rewards earned by this miner on this date. Denominated in BTC.                                               |                                               |
| miner_daily_block_reward_usd | _decimal_ | _miner_daily_block_reward_ * _price_usd_                                               |
