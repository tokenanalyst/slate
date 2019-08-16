# Binance Token Stats (BETA)

We support all tokens issued on Binance chain, but only have price data for the following:

| Name                  | Symbol |
| --------------------- | ------ |
| Binance Coin          | `bnb`  |
| Stable USD            | `usdsb`|
| Harmony.One           | `one ` |
| Bitcoin BEP2          | `btcb` |
| Bezant                | `bznt` |
| Ankr                  | `ankr` |
| Mithril               | `mith` |
| Fantom                | `ftm`  |


## BEP2 On-chain Volume

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&token=mith&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2017-08-11",
    "volume": 100001170833,
    "price_usd": 0.11,
    "volume_usd": 1305799085
  },
  {
    "date": "2017-08-13",
    "volume": 82753422,
    "price_usd": 0.18,
    "volume_usd": 1490913652
  }
]
```

This endpoint returns the full historical on-chain volume of all BEP2 tokens. Note, wo don't have price data for all the tokens

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The token you want the volume for                   |

### Data Overview

| Field                        | Type     | Description                                         |
| ---------------------------- | -------- | --------------------------------------------------- |
| date                         | _string_ | The date in _YYYY-MM-DD_                                 |
| volume                   | _decimal_ | The total sum of the BEP2 token sent by addresses in transactions with a timestamp that occurs on this date. |
| price_usd     | _decimal_ | The daily average price of specified BEP2 token in USD (the daily mean of minute-level price data)                                                |
| volume_usd                    | _decimal_ | _volume_ * _price_usd_                                             |                                               |

## BEP2 On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&token=bnb&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2017-09-06",
    "number_of_txns": 4
  },
  {
    "date": "2017-09-15",
    "number_of_txns": 5512
  },
  {
    "date": "2017-09-16",
    "number_of_txns": 4822
  }
]
```

This endpoint returns the full historical on-chain transaction count of all BEP2 tokens 

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The token you want the transaction count for        |

### Data Overview

| Field | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| date       | _string_ | The date in _YYYY-MM-DD_ |
| number_of_txns | _integer_ | The number of BEP2 token transactions for the specified token included in blocks with a timestamp that occurs on this date |


## BEP2 Active addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last?&token=ankr&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2016-11-11",
    "active_senders": 23,
    "active_receipients": 31
  },
  {
    "date": "2016-11-12",
    "active_senders": 332,
    "active_receipients": 23
  }
]
```

This endpoint returns the active addresses of BEP2 tokens for every day of their existence. An address is defined as 'active' if it has transacted during the given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The token you want the transaction count for   |

| Field | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| date       | _string_ | The date in _YYYY-MM-DD_ |
| active_senders | _integer_ | The total number of distinct addresses that sent the specified BEP2 token in transactions with a timestamp on this date |
| active_recipients | _integer_ | The total number of distinct addresses that received the specified BEP2 token in transactions with a timestamp on this date |