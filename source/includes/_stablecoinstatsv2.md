# Stablecoin Stats

The stablecoins we currently support are:

| Name                 | Symbol       |
| -------------------- | ------------ |
| Tether (Omni)        | `usdt_omni`  |
| Tether               | `usdt_erc20` |
| USDC                 | `usdc`       |
| Paxos Standard Token | `pax`        |
| TrueUSD              | `tusd`       |
| Gemini Dollar        | `gusd`       |
| Dai                  | `dai`        |

We have slightly different endpoints for Tether (usdt_omni) due to the nature of OMNI blockchian

## Tether (Omni) On-chain Volume

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last?format=json&token=usdt_omni&window=1h&from_date=2018-09-10&to_date=2018-09-12&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-09-12",
    "hour": "22:00:00", // not available when window 1d
    "datetime": "2018-09-10 22:00:00", // not available when window 1d
    "volume": 3253506.56,
    "volume_usd": 3245372.75
  },
  {
    "date": "2018-09-12",
    "hour": "23:00:00", // not available when window 1d
    "datetime": "2018-09-12 23:00:00", // not available when window 1d
    "volume": 3820308.81,
    "volume_usd": 3815724.25
  }
]
```

This endpoint returns the full historical on-chain volume of Tether on the OMNI blockchain since it went live on 2014-10-06. Values are calculated over the window (either 1 hour or 1 day). `hour` is in UTC

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| window    | _string_ | `1h` or `1d`                                        |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field       | Type      | Description                                                                                                                                 |
| ----------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| date        | _string_  | The date in _YYYY-MM-DD_                                                                                                                    |
| hour \*     | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                          |
| datetime \* | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h` |
| volume      | _decimal_ | The total sum of Tether (usdt_omni) sent by addresses in transactions with a timestamp that occurs within the window.                       |
| volume_usd  | _decimal_ | _volume_ \* _price_usd_                                                                                                                     |

## Tether (Omni) On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_window_historical/last?format=json&token=usdt_omni&from_date=2017-12-17&to_date=2017-12-18&limit=2&window=1h&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2017-12-18",
    "hour": "22:00:00", // not available when window 1d
    "datetime": "2017-12-18 22:00:00", // not available when window 1d
    "number_of_txns": 121
  },
  {
    "date": "2017-12-18",
    "hour": "23:00:00", // not available when window 1d
    "datetime": "2017-12-18 23:00:00", // not available when window 1d
    "number_of_txns": 89
  }
]
```

This endpoint returns the daily number of Tether (usdt_omni) transactions on the full Omni blockchain for every day of it's existence 2014-10-06

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| window    | _string_ | `1h` or `1d`                                        |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field          | Type      | Description                                                                                                                                 |
| -------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| date           | _string_  | The date in _YYYY-MM-DD_                                                                                                                    |
| hour \*        | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                          |
| datetime \*    | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h` |
| number_of_txns | _integer_ | The number of stablecoin transactions included in blocks with a timestamp that occurs on this date                                          |

## Tether (Omni) Active Addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_window_historical/last?&token=usdt_omni&format=json&from_date=2019-02-17&to_date=2019-02-18&window=1d&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-02-17",
    "active_recipients": 6320,
    "active_senders": 5860
  },
  {
    "date": "2019-02-18",
    "active_recipients": 8347,
    "active_senders": 6787
  }
]
```

This endpoint returns the active addresses of Tether (usdt_omni) tokens for every day of it's existence since 2014-10-06. An address is defined as 'active' if it has transacted during the given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The stablecoin you want the transaction count for   |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field             | Type      | Description                                                                                                                                      |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                                         |
| active_senders    | _integer_ | The total number of distinct addresses that sent Tether (usdt_omni) in transactions with a timestamp on this date (includes smart contracts)     |
| active_recipients | _integer_ | The total number of distinct addresses that received Tether (usdt_omni) in transactions with a timestamp on this date (includes smart contracts) |

## Tether (Omni) Supply

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_supply_window_historical/last?&token=usdt_omni&format=json&window=1d&from_date=2019-08-14&to_date=2019-08-15&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-08-14",
    "supply": 2545000000
  },
  {
    "date": "2019-08-15",
    "supply": 2545000000
  }
]
```

This endpoint returns the historical supply of Tether (usdt_omni) on the OMNI blockchain for every day of it's existence.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_supply_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field  | Type      | Description                                                                   |
| ------ | --------- | ----------------------------------------------------------------------------- |
| date   | _string_  | The date in _YYYY-MM-DD_                                                      |
| supply | _decimal_ | The cumulative sum of Tether generated by minting and burning up to this date |

## Tether (ERC20) Supply

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_supply_window_historical/last?&token=usdt_erc20&format=json&window=1d&from_date=2019-06-11&to_date=2019-06-12&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-06-11",
    "supply": 800010000
  },
  {
    "date": "2019-06-12",
    "supply": 800010000
  }
]
```

This endpoint returns the historical supply of the Tether ERC20 token (usdt_erc20) on the Ethereum blockchain for every day of it's existence.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_supply_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_erc20`                                         |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field  | Type      | Description                                                                   |
| ------ | --------- | ----------------------------------------------------------------------------- |
| date   | _string_  | The date in _YYYY-MM-DD_                                                      |
| supply | _decimal_ | The cumulative sum of Tether generated by minting and burning up to this date |

## Tether (Omni) NVT

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_nvt_window_historical/last?&token=usdt_omni&format=json&window=1d&from_date=2019-08-19&to_date=2019-08-20&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-08-19",
    "marketcap_usd": 2545000000,
    "nvt": 9.4917
  },
  {
    "date": "2019-08-20",
    "marketcap_usd": 2545000000,
    "nvt": 8.6839
  }
]
```

This endpoint returns the NVT Ratio (Network Value to Transactions Ratio) for Tether (usdt_omni). This is the ratio of the Market Cap divided by the volume transmitted by the blockchain. Special thanks to Willy Woo and Chris Burniske for coming up with it!

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_nvt_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field         | Type      | Description                                                                                                                |
| ------------- | --------- | -------------------------------------------------------------------------------------------------------------------------- |
| date          | _string_  | The date in _YYYY-MM-DD_                                                                                                   |
| marketcap_usd | _decimal_ | The total USD market capitalization of Tether (usdt*omni) on this date. (\_price_usd* \* _supply_)                         |
| nvt           | _decimal_ | Ratio comprising the total Tether (usdt*omni) Market Cap divided by the on-chain volume. (\_marketcap_usd* / _volume_usd_) |

## Tether (Omni) Fees

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_fees_window_historical/last?&token=usdt_omni&format=json&window=1d&from_date=2019-08-13&to_date=2019-08-14&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-08-13",
    "total_fee": 19.5264,
    "total_fee_usd": 19.5264,
    "avg_fee": 0.0003,
    "avg_fee_usd": 0.0003
  },
  {
    "date": "2019-08-14",
    "total_fee": 8.1131,
    "total_fee_usd": 8.1131,
    "avg_fee": 0.0002,
    "avg_fee_usd": 0.0002
  }
]
```

This endpoint returns the historical supply of Tether (usdt_omni) on the OMNI blockchain for every day of it's existence 2014-10-06

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_fees_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `usdt_omni`                                         |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field         | Type      | Description                                                                                                    |
| ------------- | --------- | -------------------------------------------------------------------------------------------------------------- |
| date          | _string_  | The date in _YYYY-MM-DD_                                                                                       |
| total_fee     | _decimal_ | The sum of fees paid in transactions that occurred on this date. Denominated in Tether (usdt_omni)             |
| total_fee_usd | _decimal_ | _total_fee_ \* _price_usd_                                                                                     |
| avg_fee       | _decimal_ | The average amount of fees paid per transaction that occurred on this date. Denominated in Tether (usdt_omni). |
| avg_fee_usd   | _decimal_ | _avg_fee_ \* _price_usd_                                                                                       |

## Stablecoin On-chain Volume

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last?format=json&token=usdc&window=1d&from_date=2019-09-25&to_date=2019-09-26&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-09-25",
    "volume": 219830971.166091,
    "volume_usd": 219830971.17
  },
  {
    "date": "2018-09-26",
    "volume": 58031092.284338,
    "volume_usd": 58031092.28
  }
]
```

This endpoint returns the full historical on-chain volume of any of the stablecoins that we support.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The token you want the volume for                   |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field      | Type      | Description                                                                                               |
| ---------- | --------- | --------------------------------------------------------------------------------------------------------- |
| date       | _string_  | The date in _YYYY-MM-DD_                                                                                  |
| volume     | _decimal_ | The total sum of Stablecoins sent by addresses in transactions with a timestamp that occurs on this date. |
| volume_usd | _decimal_ | _volume_ \* _price_usd_                                                                                   |

## Stablecoin On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_window_historical/last?format=json&token=dai&window=1d&from_date=2017-12-18&to_date=2017-12-20&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2017-12-18",
    "number_of_txns": 161
  },
  {
    "date": "2017-12-19",
    "number_of_txns": 599
  },
  {
    "date": "2017-12-20",
    "number_of_txns": 515
  }
]
```

This endpoint returns the number of token transfers on the Ethereum blockchain for the given stablecoin you select for every day of its existence.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The stablecoin you want the transaction count for   |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field          | Type      | Description                                                                                        |
| -------------- | --------- | -------------------------------------------------------------------------------------------------- |
| date           | _string_  | The date in _YYYY-MM-DD_                                                                           |
| number_of_txns | _integer_ | The number of stablecoin transactions included in blocks with a timestamp that occurs on this date |

## Stablecoin Active addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_window_historical/last?&token=usdc&format=json&window=1d&from_date=2018-11-11&to_date=2018-11-12&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-11-11",
    "active_senders": 67,
    "active_recipients": 67
  },
  {
    "date": "2018-11-12",
    "active_senders": 126,
    "active_recipients": 110
  }
]
```

This endpoint returns the active addresses of stabelecoin tokens for every day of their existence. An address is defined as 'active' if it has transacted during the given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The stablecoin you want the transaction count for   |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field             | Type      | Description                                                                                                                               |
| ----------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                                  |
| active_senders    | _integer_ | The total number of distinct addresses that sent Stablecoins in transactions with a timestamp on this date (includes smart contracts)     |
| active_recipients | _integer_ | The total number of distinct addresses that received Stablecoins in transactions with a timestamp on this date (includes smart contracts) |
