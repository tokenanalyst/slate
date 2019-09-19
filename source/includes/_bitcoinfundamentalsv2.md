# Bitcoin Fundamentals

## BTC On-chain Volume

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

This endpoint returns the full historical on-chain volume of Bitcoin since it's genesis in 2009. The volume is separated into 'real' volume and 'change' volume.

Our current heuristic for 'change' related volume is for whenever BTC in a transaction
is sent back to the same address that sent the BTC. The 'real' volume is simply the
remainder left over after subtracting the change.

```shell
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last?format=json&key=API_KEY&token=btc&window=1h"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2014-03-12",
    "hour": "22:00:00", // not available when window 1d
    "datetime": "2014-03-12 22:00:00", // not available when window 1d
    "volume_gross": 18162.41657378,
    "volume_change": 1437.98486305,
    "volume_real": 16724.43171073,
    "volume_change_usd": 891507.43,
    "volume_real_usd": 10368645.44
  },
  {
    "date": "2014-03-12",
    "hour": "23:00:00", // not available when window 1d
    "datetime": "2014-03-12 23:00:00", // not available when window 1d
    "volume_gross": 51391.70115624,
    "volume_change": 904.51484837,
    "volume_real": 50487.18630787,
    "volume_change_usd": 560383.11,
    "volume_real_usd": 31278830.3
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | The token you want the volume for (in this case `btc`)                                    |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field             | Type      | Description                                                                                                                                        |
| ----------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                                           |
| hour \*           | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field field and appears when window is `1h`                                 |
| datetime *        | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h`        |
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
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_window_historical/last?format=json&token=btc&window=1h&from_date=2009-03-12&to_date=2009-03-12&limit=3&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2009-03-12",
    "hour": "21:00:00", // not available when window 1d
    "datetime": "2009-03-12 21:00:00", // not available when window 1d
    "number_of_txns": 7
  },
  {
    "date": "2009-03-12",
    "hour": "22:00:00", // not available when window 1d
    "datetime": "2009-03-12 22:00:00", // not available when window 1d
    "number_of_txns": 6
  },
  {
    "date": "2009-03-12",
    "hour": "23:00:00", // not available when window 1d
    "datetime": "2009-03-12 23:00:00", // not available when window 1d
    "number_of_txns": 5
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | The token you want the volume for (in this case `btc`)                                    |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field          | Type      | Description                                                                                                                  |
| -------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------- |
| date           | _string_  | The date in _YYYY-MM-DD_                                                                                                     |
| number_of_txns | _integer_ | The number of transactions included in blocks with a timestamp that occurs during this date (includes coinbase transactions) |
| hour \*        | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                 |
| datetime *     | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h`        |

---

## BTC Active addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

This endpoint returns the daily number of active addresses on the Bitcoin blockchain for each day
of its existence. An address is defined as 'active' if it has sent or received bitcoin
in a transaction with a timestamp on that day. Only the distinct number of addresses are
counted, i.e. an address which sends thousands of transactions per day is only counted once
as an _active_sender_ with the same logic applied to distinct receiving addresses.

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_window_historical/last?format=json&token=btc&window=1d&from_date=2018-10-10&to_date=2018-10-18&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-10-17",
    "active_senders": 477052,
    "active_recipients": 490874
  },
  {
    "date": "2018-10-18",
    "active_senders": 459061,
    "active_recipients": 479728
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_window_historical/last`

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
curl "https://api.tokenanalyst.io/analytics/private/v1/token_supply_window_historical/last?format=json&token=btc&window=1d&from_date=2016-10-10&to_date=2016-10-12&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2016-10-10",
    "supply": 15922677.2953033
  },
  {
    "date": "2016-10-11",
    "supply": 15924414.7953033
  },
  {
    "date": "2016-10-12",
    "supply": 15926214.7953033
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_supply_window_historical/last`

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

| Field  | Type     | Description                                                              |
| ------ | -------- | ------------------------------------------------------------------------ |
| date   | _string_ | The date in _YYYY-MM-DD_                                                 |
| supply | _float_  | The cumulative sum of bitcoins generated by mined blocks up to this date |

---

## BTC NVT

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_nvt_window_historical/last?format=json&token=btc&window=1d&from_date=2011-10-10&to_date=2012-09-01&limit=3&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2012-08-30",
    "marketcap_usd": 89396489.26,
    "nvt": 0.8546
  },
  {
    "date": "2012-08-31",
    "marketcap_usd": 89460189.25,
    "nvt": 1.1035
  },
  {
    "date": "2012-09-01",
    "marketcap_usd": 89533444.23,
    "nvt": 1.1367
  }
]
```

This endpoint returns the NVT Ratio (Network Value to Transactions Ratio) for BTC. This is the ratio of the Market Cap divided by the volume transmitted by the blockchain. Special thanks to Willy Woo and Chris Burniske for coming up with it!

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_nvt_window_historical/last`

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

| Field         | Type      | Description                                                                                                     |
| ------------- | --------- | --------------------------------------------------------------------------------------------------------------- |
| date          | _string_  | The date in _YYYY-MM-DD_                                                                                        |
| marketcap_usd | _decimal_ | The total USD market capitalization of BTC on this date. (_price_usd_ \* _supply_)                              |
| nvt           | _decimal_ | Ratio comprising the total BTC Market Cap divided by the on-chain volume. (_marketcap_usd_ / _volume_real_usd_) |

## BTC Fees

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_fees_window_historical/last?format=json&token=btc&window=1d&from_date=2014-03-12&to_date=2014-03-15&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2014-03-14",
    "total_fee": 13.6553,
    "avg_size_bytes": 575,
    "total_fee_usd": 8480.11,
    "avg_satoshis_per_byte": 33.6015,
    "avg_fee": 0.0002,
    "avg_fee_usd": 0.12
  },
  {
    "date": "2014-03-15",
    "total_fee": 10.9136,
    "avg_size_bytes": 508,
    "total_fee_usd": 6774.36,
    "avg_satoshis_per_byte": 35.6095,
    "avg_fee": 0.0002,
    "avg_fee_usd": 0.11
  }
]
```

This endpoint returns the total and average fees spent on the Bitcoin network for every day of it's existence. The `total_fee` is denominated in Bitcoin, the `price` is the price of Bitcoin on that day, and the `avg_fee` is denominated in Bitcoin. Since fees are paid to miners as part of the coinbase transaction, these transactions are not included when
calculating metrics such as the average fee per transaction (`avg_fee`). Before 2010 there was little activity on the blockchain besides mining, i.e. the chain was dominated by coinbase transactions.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_fees_window_historical/last`

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

| Field                 | Type      | Description                                                                                       |
| --------------------- | --------- | ------------------------------------------------------------------------------------------------- |
| date                  | _string_  | The date in _YYYY-MM-DD_                                                                          |
| total_fee             | _decimal_ | The total amount of fees paid by all transactions that occurred on this date. Denominated in BTC. |
| avg_size_bytes        | _integer_ | The average transaction size to the nearest byte for transactions that occurred on this date.     |
| total_fee_usd         | _decimal_ | _total_fee_ \* _price_                                                                            |
| avg_satoshis_per_byte | _integer_ | The average number of satoshis paid per byte for transactions that occurred on this date          |
| avg_fee               | _decimal_ | The average amount of fees paid per transaction that occurred on this date. Denominated in BTC.   |
| avg_fee_usd           | _decimal_ | _avg_fee_ \* _price_usd_                                                                          |

## BTC UTXO Age

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_utxo_age_window_historical/last?window=1d&exchange=binance&direction=outflow&format=json&token=btc&from_date=2019-09-01&to_date=2019-09-02&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-09-01",
    "1-3m": 0.0812,
    "12-18m": 0.1705,
    "18-24m": 0.0795,
    "1d-1w": 0.0219,
    "1w-1m": 0.0646,
    "2-3y": 0.0491,
    "3-5y": 0.0657,
    "3-6m": 0.1322,
    "5-10y": 0.1438,
    "6-12m": 0.1105,
    "<1d": 0.0131,
    ">10y": 0.0679
  },
  {
    "date": "2019-09-02",
    "1-3m": 0.0815,
    "12-18m": 0.1705,
    "18-24m": 0.0798,
    "1d-1w": 0.0226,
    "1w-1m": 0.0634,
    "2-3y": 0.0491,
    "3-5y": 0.0658,
    "3-6m": 0.1317,
    "5-10y": 0.1436,
    "6-12m": 0.1109,
    "<1d": 0.0132,
    ">10y": 0.068,
    "date": "2019-03-15"
  }
]
```

This endpoint returns the proportion of the current bitcoin supply held in unspent transaction outputs stratified by their age. For instance outputs in the category `12-18m` are unspent outputs (UTXOs) from transactions that occurred `12-18m` ago. Time is measured relative to blocktime assuming 6 blocks are generated per hour. This means that the proportion of UTXOs in the `<1d` category were generated less than or equal to `144 blocks ago (6 blocks * 24 hours)`.

The age in block height is used over the block timestamp because the block timestamp serves as a source of variation when calculating the blockhash and is only accurate to within an hour or two. By using timestamps some UTXOs could be considered older than a previously generated UTXO. By using block-age from current the blockheight, the age of utxos is strictly ordinal as blockheight is strictly sequential.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_utxo_age_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| token        | _string_  | `btc`                                                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

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
curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_hashrate_window_historical/last?format=json&token=btc&key=API_KEY"
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

## BTC Miner Rewards

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_miner_hashrate_window_historical/last?format=json&token=btc&window=1d&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-09-03",
    "miner_name": "BitFury",
    "miner_daily_block_count": 4,
    "miner_daily_hashrate": 2141915.4344,
    "total_daily_block_count": 103,
    "total_daily_hashrate": 55154322.4359,
    "miner_daily_hashrate_pct": 3.8835
  },
  {
    "date": "2019-09-03",
    "miner_name": "Huobi.pool",
    "miner_daily_block_count": 4,
    "miner_daily_hashrate": 2141915.4344,
    "total_daily_block_count": 103,
    "total_daily_hashrate": 55154322.4359,
    "miner_daily_hashrate_pct": 3.8835
  }
]
```

This endpoint returns the daily coinbase rewards by miner (incl. txn fees). The `miner_daily_block_reward` is denomiated BTC.

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
