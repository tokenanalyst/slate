# Stablecoin Stats

The stablecoins we currently support are:

| Name                 | Symbol |
| -------------------- | ------ |
| Tether               | `usdt_erc20` |
| USDC                 | `usdc` |
| Paxos Standard Token | `pax`  |
| TrueUSD              | `tusd` |
| Gemini Dollar        | `gusd` |
| Dai                  | `dai`  |

## Stablecoin On-chain Volume

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&token=usdc&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-09-10",
    "volume": 22.2,
    "price_usd": 0.0,
    "volume_usd": 0.0
  },
  {
    "date": "2018-09-12",
    "volume": 2.5,
    "price_usd": 0.0,
    "volume_usd": 0.0
  }
]
```

This endpoint returns the full historical on-chain volume of any of the stablecoins that we support.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The token you want the volume for                   |

### Data Overview

| Field | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| date       | _string_ | The date in _YYYY-MM-DD_ |
| volume    | _decimal_ | The total sum of Stablecoins sent by addresses in transactions with a timestamp that occurs on this date. |
| price_usd     | _decimal_ | The daily average price of the Stablecoins (the daily mean of minute-level price data) |
| volume_usd    | _decimal_ |  _volume_ * _price_usd_  |

## Stablecoin On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&token=dai&key=API_KEY"
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

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The stablecoin you want the transaction count for   |

### Data Overview

| Field | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| date       | _string_ | The date in _YYYY-MM-DD_ |
| number_of_txns | _integer_ | The number of stablecoin transactions included in blocks with a timestamp that occurs on this date |

## Stablecoin Active addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last?&token=usdc&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2016-11-11",
    "active_senders": 23,
    "active_recipients": 31
  },
  {
    "date": "2016-11-12",
    "active_senders": 332,
    "active_recipients": 23
  }
]
```

This endpoint returns the active addresses of stabelecoin tokens for every day of their existence. An address is defined as 'active' if it has transacted during the given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The stablecoin you want the transaction count for 

### Data Overview

| Field | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| date       | _string_ | The date in _YYYY-MM-DD_ |
| active_senders | _integer_ | The total number of distinct addresses that sent Stablecoins in transactions with a timestamp on this date (includes smart contracts) |
| active_recipients | _integer_ | The total number of distinct addresses that received Stablecoins in transactions with a timestamp on this date (includes smart contracts) |