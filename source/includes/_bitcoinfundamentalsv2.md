# Bitcoin Fundamentals

## BTC On-chain Volume

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

This endpoint returns the full historical on-chain volume of Bitcoin since it's genesis in 2009. The volume is separated into 'real' volume and 'change' volume.

Our current heuristic for 'change' related volume is for whenever BTC in a transaction
is sent back to the same address that sent the BTC. The 'real' volume is simply the
remainder left over after subtracting the change.

```shell
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last?format=json&token=btc&window=1h&from_date=2014-03-12&to_date=2014-03-12&limit=2&key=API_KEY"
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
| hour \*           | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                 |
| datetime *        | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`        |
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
| datetime *     | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`        |

---

## BTC Active Addresses

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

## BTC Total Hashrate

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_hashrate_window_historical/last?format=json&window=1d&token=btc&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2020-01-14",
    "hashrate": 99607271.22,
    "block_count": 145,
  },
  {
    "date": "2020-01-15",
    "hashrate": 80799093.578,
    "block_count": 110,
  }
]
```

This endpoint returns the daily hashrate and blocks mined for a given day. The `hashrate` is denominated in TH/s and `block_count` is the total number of blocks mined, for a given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_hashrate_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                                                                     |
| window       | _string_  | `1d` only. `1h` not supported currently.                                                    |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                    | Type      | Description                                                                                                         |
| ------------------------ | --------- | ------------------------------------------------------------------------------------------------------------------- |
| date                     | _string_  | The date in _YYYY-MM-DD_                                                                                            |
| hashrate                 | _decimal_ | The hashrate of the blockchain for the day. Denominated in Th/s.                                                    |
| block_count              | _integer_ | The total number of blocks mined on the blockchain on this date.                                                    |

## BTC Total Rewards

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_rewards_window_historical/last?format=json&token=btc&window=1d&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2020-01-14",
    "block_reward": 1838.721577,
    "block_reward_usd": 15756511.73
  },
  {
    "date": "2020-01-15",
    "block_reward": 1460.60649732,
    "block_reward_usd": 12738482.28
  }
]
```

This endpoint returns the daily coinbase rewards. The `block_reward` is denominated BTC.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_rewards_window_historical/last`

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
| block_reward                 | _decimal_ | The total amount of block rewards earned on this date. Denominated in BTC.               |
| block_reward_usd             | _decimal_ | _block_reward_ \* _price_usd_                                                            |

## BTC New Addresses

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the full historical number of unique addresses that appeared for the first time in a transaction as well as the total number of addresses on the Bitcoin network every day throughout it's history.

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_new_address_window_historical/last?format=json&token=btc&window=1d&from_date=2019-12-04&to_date=2019-12-05&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-12-04",
    "number_of_new_addresses": 395937,
    "total_number_of_addresses": 586240871
  },
  {
    "date": "2019-12-05",
    "number_of_new_addresses": 380820,
    "total_number_of_addresses": 586621691
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_new_address_window_historical/last`

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

| Field                     | Type      | Description                                                                                                  |
| ------------------------- | --------- | ------------------------------------------------------------------------------------------------------ |
| date                      | _string_  | The date in _YYYY-MM-DD_                                                                               |
| number_of_new_addresses   | _integer_ | The total number of distinct addresses that appeared for the first time in a transaction on the Bitcoin network on this date     |
| total_number_of_addresses | _integer_ | The cumulative total of distinct addresses appeared for the first time in a transaction on the Bitcoin network on this date |

## BTC Address Balances

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the full historical number of unique addresses holding a given amount of bitcoin.  We have bucketed the amounts of Bitcoin held into distinct categories (greater than 1, greater than 100 etc.)

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_address_balance_group_window_historical/last?format=json&token=btc&window=1d&from_date=2019-12-04&to_date=2019-12-05&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-12-04",
    "balance_greater_than_0": 28153270,
    "balance_greater_than_1": 778513,
    "balance_greater_than_10": 152666,
    "balance_greater_than_100": 16273,
    "balance_greater_than_1000": 2128,
    "balance_greater_than_10000": 108
  },
  {
    "date": "2019-12-05",
    "balance_greater_than_0": 28173349,
    "balance_greater_than_1": 778406,
    "balance_greater_than_10": 152705,
    "balance_greater_than_100": 16220,
    "balance_greater_than_1000": 2131,
    "balance_greater_than_10000": 107
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_address_balance_group_window_historical/last`

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

| Field                         | Type      | Description                                                                                            |
| ----------------------------- | --------- | ------------------------------------------------------------------------------------------------------ |
| date                          | _string_  | The date in _YYYY-MM-DD_                                                                               |
| balance_greater_than_0        | _integer_ | The number of unique addresses holding more than `0` BTC on this date                                  |
| balance_greater_than_1        | _integer_ | The number of unique addresses holding at least `1` BTC on this date                                   |
| balance_greater_than_10       | _integer_ | The number of unique addresses holding at least `10` BTC on this date                                  |
| balance_greater_than_100      | _integer_ | The number of unique addresses holding at least `100` BTC on this date                                 |
| balance_greater_than_1000     | _integer_ | The number of unique addresses holding at least `1000` BTC on this date                                |
| balance_greater_than_10000    | _integer_ | The number of unique addresses holding at least `10000` BTC on this date                               |

## BTC Spent Outputs Profit Ratio

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

This endpoint returns the historical spent outputs profit ratio (SOPR) as defined by Renato Shirakashi. The data starts from 2010-10-10 when we start tracking a non-zero price for Bitcoin because UTXOs with a non-zero realised price will have an infinite profit ratio when created with an effective price of $0.

SOPR shows whether Bitcoin outputs (UTXOs) were spent at a profit or a loss by dividing their value when they are spent, by their value when they were created.

If the ratio is greater than one, this means that a UTXO was spent when it was worth more than when it was created. SOPR is calculated by adding of the USD value of the UTXOs spent in a time window, and dividing it by the sum of USD values of these UTXOs at the time when they were created. The average price of Bitcoin in a given time window is used to determine its USD value. 


```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_sopr_window_historical/last?window=1h&limit=2&from_date=2019-10-10&to_date=2019-10-11&format=json&token=btc&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-10-11",
    "hour": "22:00:00", // not available when window 1d
    "datetime": "2010-10-11 22:00:00", // not available when window 1d
    "sopr": 0.9934
  },
  {
    "date": "2019-10-11",
    "hour": "23:00:00", // not available when window 1d
    "datetime": "2019-10-11 23:00:00", // not available when window 1d
    "sopr": 0.9943
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_sopr_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                  |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field          | Type      | Description                                                                                                                  |
| -------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------- |
| date           | _string_  | The date in _YYYY-MM-DD_                                                                                                     |
| sopr           | _decimal_ | The average ratio between the realised price of UTXOs spent during this time period, divided by their price at the time of creation
| hour \*        | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                 |
| datetime *     | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`        |

## BTC UTXO Age

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_utxo_age_window_historical/last?window=1d&format=json&token=btc&from_date=2019-09-01&to_date=2019-09-02&key=API_KEY"
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
