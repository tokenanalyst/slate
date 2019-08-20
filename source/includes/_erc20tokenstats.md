# ERC20 Token Stats

ERC20 tokens we currently support are:

| Name                  | Symbol  |
| --------------------- | ------- |
| Maker                 | `mkr`   |
| Basic Attention Token | `bat`   |
| OmiseGo               | `omg`   |
| Augur                 | `rep`   |
| Golem                 | `gnt`   |
| ZRX                   | `zrx`   |
| Zilliqa               | `zil`   |
| Decentraland          | `mana`  |
| Numerai               | `nmr`   |
| Tokencard             | `tkn`   |
| Bancor                | `bnt`   |
| Loom Network          | `loom`  |
| Status                | `snt`   |
| Civic                 | `cvc`   |
| Kyber Network         | `knc`   |
| iExec RLC             | `rlc`   |
| ChainLink             | `link`  |
| Ocean Protocol        | `ocean` |
| Fetch.ai.             | `fet`   |

## ERC20 On-chain Volume

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&token=zrx&key=API_KEY"
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

This endpoint returns the full historical on-chain volume of any of the major ERC20 tokens that we support.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last`

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
| volume    | _decimal_ | The total sum of ERC20 token sent by addresses in transactions with a timestamp that occurs on this date. |
| price_usd     | _decimal_ | The daily average price of the ERC20 token (the daily mean of minute-level price data) |
| volume_usd    | _decimal_ |  _volume_ * _price_usd_  |

## ERC20 On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&token=mana&key=API_KEY"
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

This endpoint returns the number of token transfers on the blockchain for the given token for every day since its existence.

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
| number_of_txns | _integer_ | The number of ERC20 transactions included in blocks with a timestamp that occurs on this date |


## ERC20 Active addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last?&token=gnt&format=json&key=API_KEY"
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

This endpoint returns the active addresses of ERC20 tokens for every day of their existence. An address is defined as 'active' if it has transacted during the given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last`

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
| active_senders | _integer_ | The total number of distinct addresses that sent ERC20 tokens in transactions with a timestamp on this date (includes smart contracts) |
| active_recipients | _integer_ | The total number of distinct addresses that received ERC20 tokens in transactions with a timestamp on this date (includes smart contracts) |