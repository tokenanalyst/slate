# Ethereum Fundamentals

## ETH On-chain Volume

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last?format=json&token=eth&window=1d&from_date=2015-08-07&to_date=2015-08-08&key=API_KEY"
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

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `eth`) |
| window       | _string_  | `1h` or `1d`                                                       |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


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
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_window_historical/last?format=json&token=eth&window=1d&from_date=2015-08-07&to_date=2015-08-09&key=API_KEY"
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

This endpoint returns the number of transactions, where ETH value transferred was > 0, on the full historical Ethereum blockchain for every day since its genesis in 2015. This endpoint would exclude smart contract calls or token transfers where 0 ETH was transferred between accounts.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `eth`) |
| window       | _string_  | `1h` or `1d`                                                         |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field          | Type      | Description                                                                                 |
| -------------- | --------- | ------------------------------------------------------------------------------------------- |
| date           | _string_  | The date in _YYYY-MM-DD_                                                                    |
| number_of_txns | _integer_ | The number of transactions included in blocks with a timestamp that occurs during this date |

## ETH Active addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_window_historical/last?&token=eth&format=json&from_date=2015-08-11&to_date=2015-08-12&window=1d&key=API_KEY"
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

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field             | Type      | Description                                                                                            |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------ |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                               |
| active_senders    | _integer_ | The total number of distinct addresses that sent ETH in transactions with a timestamp on this date     |
| active_recipients | _integer_ | The total number of distinct addresses that received ETH in transactions with a timestamp on this date |

## ETH Supply

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_supply_window_historical/last?&token=eth&format=json&window=1d&from_date=2015-07-30&to_date=2015-07-31&key=API_KEY"
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

`GET https://api.tokenanalyst.io/analytics/private/v1/token_supply_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field  | Type      | Description                                                                             |
| ------ | --------- | --------------------------------------------------------------------------------------- |
| date   | _string_  | The date in _YYYY-MM-DD_                                                                |
| supply | _decimal_ | The cumulative sum of ether (ETH) generated by mining and uncle rewards up to this date |

## ETH NVT

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_nvt_window_historical/last?&token=eth&format=json&window=1d&from_date=2015-09-02&to_date=2015-09-03&key=API_KEY"
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

`GET https://api.tokenanalyst.io/analytics/private/v1/token_nvt_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field         | Type      | Description                                                                                                         |
| ------------- | --------- | ------------------------------------------------------------------------------------------------------------------- |
| date          | _string_  | The date in _YYYY-MM-DD_                                                                                            |
| marketcap_usd | _decimal_ | The total USD market capitalization of ETH on this date. (_price_usd_ \* _supply_)                                  |
| nvt           | _decimal_ | Ratio comprising the total ETH Market Cap divided by the on-chain volume. (_marketcap_usd_ / _volume_external_usd_) |

## ETH Fees

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_fees_window_historical/last?&token=eth&format=json&window=1d&from_date=2015-10-19&to_date=2015-10-20&key=API_KEY"
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

`GET https://api.tokenanalyst.io/analytics/private/v1/token_fees_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


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

## ETH Total Hashrate

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_hashrate_window_historical/last?format=json&window=1d&token=eth&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2020-01-27",
    "hashrate": 157.4803,
    "block_count": 6552,
  },
  {
    "date": "2020-01-28",
    "hashrate": 154.7753,
    "block_count": 6511,
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
| token        | _string_  | `eth`                                                                                     |
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

## ETH Total Rewards

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_rewards_window_historical/last?format=json&token=eth&window=1d&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2020-01-27",
    "block_reward": 13678.125,
    "block_reward_usd": 2306321.47
  },
  {
    "date": "2020-01-28",
    "block_reward": 13565.375,
    "block_reward_usd": 2333781.64
  }
]
```

This endpoint returns the daily coinbase rewards. The `block_reward` (incl. uncle rewards) is denominated ETH.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_rewards_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `eth`                                                                                     |
| window       | _string_  | `1d` only. `1h` not supported currently.                                                  |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                        | Type      | Description                                                                              |
| ---------------------------- | --------- | ---------------------------------------------------------------------------------------- |
| date                         | _string_  | The date in _YYYY-MM-DD_                                                                 |
| block_reward                 | _decimal_ | The total amount of block rewards earned on this date. Denominated in ETH.               |
| block_reward_usd             | _decimal_ | _block_reward_ \* _price_usd_                                                            |

## ETH New Addresses

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the full historical number of unique addresses that appeared for the first time in a transaction as well as the total number of addresses on the Ethereum network every day throughout it's history.

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_new_address_window_historical/last?format=json&token=eth&window=1d&from_date=2019-12-04&to_date=2019-12-05&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-12-04",
    "number_of_new_addresses": 52926,
    "total_number_of_addresses": 77017751
  },
  {
    "date": "2019-12-05",
    "number_of_new_addresses": 75678,
    "total_number_of_addresses": 77093429
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
| token        | _string_  | `eth`                                                                                     |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                     | Type      | Description                                                                                                  |
| ------------------------- | --------- | ------------------------------------------------------------------------------------------------------ |
| date                      | _string_  | The date in _YYYY-MM-DD_                                                                               |
| number_of_new_addresses   | _integer_ | The total number of distinct addresses that appeared for the first time in a transaction on the Ethereum network on this date     |
| total_number_of_addresses | _integer_ | The cumulative total of distinct addresses appeared for the first time in a transaction on the Ethereum network on this date |
