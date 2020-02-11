# Token Fundamentals

The stablecoins we currently support are:

| Name                 | Symbol       |
| -------------------- | ------------ |
| Tether               | `usdt_erc20` |
| USDC                 | `usdc`       |
| Paxos Standard Token | `pax`        |
| TrueUSD              | `tusd`       |
| Gemini Dollar        | `gusd`       |
| Multi-Collateral Dai | `dai`        |


The ERC20 tokens we currently support are:

| Name                  | Symbol  |
| --------------------- | ------- |
| Maker                 | `mkr`   |
| Basic Attention Token | `bat`   |
| OmiseGo               | `omg`   |
| Augur                 | `rep`   |
| Golem                 | `gnt`   |
| ZRX                   | `zrx`   |
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


## Token On-chain Volume

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

This endpoint returns the full historical on-chain volume of any of the tokens that we support.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | A token from the [table](#token-fundamentals) that we support                   |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field      | Type      | Description                                                                                               |
| ---------- | --------- | --------------------------------------------------------------------------------------------------------- |
| date       | _string_  | The date in _YYYY-MM-DD_                                                                                  |
| volume     | _decimal_ | The total sum of tokens sent by addresses in transactions with a timestamp that occurs on this date. |
| volume_usd | _decimal_ | _volume_ \* _price_usd_                                                                                   |

## Token On-chain Transaction Count

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

This endpoint returns the number of token transfers on the Ethereum blockchain for the given token you select for every day of its existence.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | A token from the [table](#token-fundamentals) that we support    |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field          | Type      | Description                                                                                        |
| -------------- | --------- | -------------------------------------------------------------------------------------------------- |
| date           | _string_  | The date in _YYYY-MM-DD_                                                                           |
| number_of_txns | _integer_ | The number of token transactions included in blocks with a timestamp that occurs on this date |

## Token Active Addresses

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

This endpoint returns the active addresses of a supported token for every day of their existence. An address is defined as 'active' if it has transacted during the given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_window_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | A token from the [table](#token-fundamentals) that we support    |
| window    | _string_ | `1d` (no support for 1h at this time)               |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field             | Type      | Description                                                                                                                               |
| ----------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                                  |
| active_senders    | _integer_ | The total number of distinct addresses that sent tokens in transactions with a timestamp on this date (includes smart contracts)     |
| active_recipients | _integer_ | The total number of distinct addresses that received tokens in transactions with a timestamp on this date (includes smart contracts) |
