
# ERC20 Fundamentals

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
| Fetch.ai.             | `fet`   |

## ERC20 On-chain Volume

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last?format=json&token=zrx&window=1d&from_date=2017-08-13&to_date=2017-08-14&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2017-08-13",
    "volume": 82750000,
    "volume_usd": 14909136.52
  },
  {
    "date": "2017-08-14",
    "volume": 52500000,
    "volume_usd": 11388781.29
  }
]
```

This endpoint returns the full historical on-chain volume of any of the major ERC20 tokens that we support.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The token you want the volume for                   |
| window    | _string_  | `1d` (no support for 1h at this time)              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |



### Data Overview

| Field | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| date       | _string_ | The date in _YYYY-MM-DD_ |
| volume    | _decimal_ | The total sum of ERC20 token sent by addresses in transactions with a timestamp that occurs on this date. |
| volume_usd    | _decimal_ |  _volume_ * _price_usd_  |

## ERC20 On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_window_historical/last?format=json&token=mana&from_date=2017-09-15&to_date=2017-09-16&window=1d&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
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

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The token you want the transaction count for        |
| window    | _string_  | `1d` (no support for 1h at this time)              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |



### Data Overview

| Field | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| date       | _string_ | The date in _YYYY-MM-DD_ |
| number_of_txns | _integer_ | The number of ERC20 transactions included in blocks with a timestamp that occurs on this date |


## ERC20 Active addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_window_historical/last?&token=gnt&format=json&from_date=2016-11-11&to_date=2016-12&window=1d&key=API_KEY"
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

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The token you want the transaction count for        |
| window    | _string_  | `1d` (no support for 1h at this time)              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| date       | _string_ | The date in _YYYY-MM-DD_ |
| active_senders | _integer_ | The total number of distinct addresses that sent ERC20 tokens in transactions with a timestamp on this date (includes smart contracts) |
| active_recipients | _integer_ | The total number of distinct addresses that received ERC20 tokens in transactions with a timestamp on this date (includes smart contracts) |
