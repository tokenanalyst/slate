# BTC UTXO Metrics

## BTC UTXO Average Age

This endpoint returns the average age of the current bitcoin supply held in unspent transaction outputs stratified by their age. For instance outputs in the category `12-18m` are unspent outputs (UTXOs) from transactions that occurred `12-18m` ago. Time is measured relative to blocktime assuming 6 blocks are generated per hour. This means that the proportion of UTXOs in the `<1d` category were generated less than or equal to 144 blocks ago (`6 blocks * 24 hours`).

The age in block height is used over the block timestamp because the block timestamp serves as a source of variation when calculating the blockhash and is only accurate to within an hour or two. By using timestamps some UTXOs could be considered older than a previously generated UTXO. By using block-age from current the blockheight, the age of utxos is strictly ordinal as blockheight is strictly sequential.


<img src="https://s3.amazonaws.com/www.tokenanalyst.io/img/weight_avg_age_eqn.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last?metric=avg_age&limit=2&window=1d&format=json&token=btc&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
   "date": "2019-10-16",
   "1-3m": 1429.2267,
   "12-18m": 10891.7902,
   "18-24m": 15520.8613,
   "1d-1w": 90.3656,
   "1w-1m": 435.0935,
   "2-3y": 21635.8451,
   "3-5y": 35142.7048,
   "3-6m": 3189.9665,
   "5-10y": 56884.8621,
   "6-12m": 6392.2049,
   "<1d": 12.0231,
   ">10y": 95228.0092
  },
  {
   "date": "2019-10-17",
   "1-3m": 1425.9911,
   "12-18m": 10888.0116,
   "18-24m": 15524.2703,
   "1d-1w": 90.6531,
   "1w-1m": 437.233,
   "2-3y": 21629.4766,
   "3-5y": 35148.2189,
   "3-6m": 3192.6356,
   "5-10y": 56902.5727,
   "6-12m": 6385.1655,
   "<1d": 11.1082,
   ">10y": 95242.9982
}
  }
]
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| metric       | _string_  | `avg_age`                                                                                 |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| token        | _string_  | `btc`                                                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field  | Type      | Description                                                                                                                                         |
| ------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| date   | _string_  | The date in _YYYY-MM-DD_                                                                                                                            |
| <1d    | _decimal_ | The average age of unspent outputs (UTXOs) on this date from transactions that occurred less than a day prior to this date.       |
| 1d-1w  | _decimal_ | The average age of unspent outputs (UTXOs) on this date from transactions that occurred 1 day to 1 week prior to this date.       |
| 1w-1m  | _decimal_ | The average age of unspent outputs (UTXOs) on this date from transactions that occurred 1 week to 1 month prior to this date.     |
| 1-3m   | _decimal_ | The average age of unspent outputs (UTXOs) on this date from transactions that occurred 1 to 3 months prior to this date.         |
| 3-6m   | _decimal_ | The average age of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 6 months prior to this date.         |
| 6-12m  | _decimal_ | The average age of unspent outputs (UTXOs) on this date from transactions that occurred 6 to 12 months prior to this date.        |
| 12-18m | _decimal_ | The average age of unspent outputs (UTXOs) on this date) from transactions that occurred 12 to 18 months prior to this date.       |
| 18-24m | _decimal_ | The average age of unspent outputs (UTXOs) on this date from transactions that occurred 18 to 24 months prior to this date.       |
| 2-3y   | _decimal_ | The average age of unspent outputs (UTXOs) on this date from transactions that occurred 2 to 3 years prior to this date.          |
| 3-5y   | _decimal_ | The average age of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 5 years prior to this date.          |
| 5-10y  | _decimal_ | The average age of unspent outputs (UTXOs) on this date from transactions that occurred 5 to 10 years prior to this date.         |
| >10y   | _decimal_ | The average age of unspent outputs (UTXOs) on this date from transactions that occurred greater than 10 years prior to this date. |

## BTC UTXO Average Value

This endpoint returns the average value of unspent transaction outputs (UTXOs) stratified by their current age. For instance outputs in the category `12-18m` are unspent outputs (UTXOs) from transactions that occurred `12-18m` ago. Time is measured relative to blocktime assuming 6 blocks are generated per hour. This means that the average value of UTXOs in the `>10y` category is the average for unspent outputs that were generated 525, 600 blocks ago (`6 blocks * 24 hours * 365 days * 10 years`).

The age in block height is used over the block timestamp because the block timestamp serves as a source of variation when calculating the blockhash and is only accurate to within an hour or two. By using timestamps some UTXOs could be considered older than a previously generated UTXO. By using block-age from current the blockheight, the age of utxos is strictly ordinal as blockheight is strictly sequential.


<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last?metric=avg_age&limit=2&window=1d&format=json&token=btc&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
   "date": "2019-10-16",
   "1-3m": 0.3169,
   "12-18m": 0.2018,
   "18-24m": 0.3342,
   "1d-1w": 0.3745,
   "1w-1m": 0.3462,
   "2-3y": 0.2303,
   "3-5y": 0.0834,
   "3-6m": 0.2905,
   "5-10y": 0.2852,
   "6-12m": 0.3736,
   "<1d": 0.4967,
   ">10y": 50.6428
  },
  {
   "date": "2019-10-17",
   "1-3m": 0.3153,
   "12-18m": 0.2001,
   "18-24m": 0.3353,
   "1d-1w": 0.384,
   "1w-1m": 0.3132,
   "2-3y": 0.2309,
   "3-5y": 0.0834,
   "3-6m": 0.2895,
   "5-10y": 0.2848,
   "6-12m": 0.3728,
   "<1d": 0.8995,
   ">10y": 50.6194
}
  }
]
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| metric       | _string_  | `avg_value`                                                                                 |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| token        | _string_  | `btc`                                                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field  | Type      | Description                                                                                                                                         |
| ------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| date   | _string_  | The date in _YYYY-MM-DD_                                                                                                                            |
| <1d    | _decimal_ | The average value of unspent outputs (UTXOs) on this date from transactions that occurred less than a day prior to this date.       |
| 1d-1w  | _decimal_ | The average value of unspent outputs (UTXOs) on this date from transactions that occurred 1 day to 1 week prior to this date.       |
| 1w-1m  | _decimal_ | The average value of unspent outputs (UTXOs) on this date from transactions that occurred 1 week to 1 month prior to this date.     |
| 1-3m   | _decimal_ | The average value of unspent outputs (UTXOs) on this date from transactions that occurred 1 to 3 months prior to this date.         |
| 3-6m   | _decimal_ | The average value of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 6 months prior to this date.         |
| 6-12m  | _decimal_ | The average value of unspent outputs (UTXOs) on this date from transactions that occurred 6 to 12 months prior to this date.        |
| 12-18m | _decimal_ | The average value of unspent outputs (UTXOs) on this date) from transactions that occurred 12 to 18 months prior to this date.       |
| 18-24m | _decimal_ | The average value of unspent outputs (UTXOs) on this date from transactions that occurred 18 to 24 months prior to this date.       |
| 2-3y   | _decimal_ | The average value of unspent outputs (UTXOs) on this date from transactions that occurred 2 to 3 years prior to this date.          |
| 3-5y   | _decimal_ | The average value of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 5 years prior to this date.          |
| 5-10y  | _decimal_ | The average value of unspent outputs (UTXOs) on this date from transactions that occurred 5 to 10 years prior to this date.         |
| >10y   | _decimal_ | The average value of unspent outputs (UTXOs) on this date from transactions that occurred greater than 10 years prior to this date. |  

## BTC UTXO Count

This endpoint returns the count of unspent transaction outputs (UTXOs) stratified by their age. For instance the category `12-18m` contains the count of currently unspent outputs from transactions that occurred `12-18m` ago. Time is measured relative to blocktime assuming 6 blocks are generated per hour. This means that the count of UTXOs in the `<1d` category were from UTXOs generated less than or equal to `144 blocks ago (6 blocks * 24 hours)`.

The age in block height is used over the block timestamp because the block timestamp serves as a source of variation when calculating the blockhash and is only accurate to within an hour or two. By using timestamps some UTXOs could be considered older than a previously generated UTXO. By using block-age from current the blockheight, the age of utxos is strictly ordinal as blockheight is strictly sequential.


<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last?metric=count&limit=2&window=1d&format=json&token=btc&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
   "date": "2019-10-16",
   "1-3m": 5608778,
   "12-18m": 5737941,
   "18-24m": 6219351,
   "1d-1w": 1139380,
   "1w-1m": 3060596,
   "2-3y": 7402366,
   "3-5y": 11597627,
   "3-6m": 7248319,
   "5-10y": 8067592,
   "6-12m": 6916852,
   "<1d": 349249,
   ">10y": 32772
  },
  {
   "date": "2019-10-17",
   "1-3m": 5615040,
   "12-18m": 5753489,
   "18-24m": 6214569,
   "1d-1w": 1141220,
   "1w-1m": 2987535,
   "2-3y": 7412377,
   "3-5y": 11613309,
   "3-6m": 7282144,
   "5-10y": 8071654,
   "6-12m": 6916407,
   "<1d": 323682,
   ">10y": 32815
}
  }
]
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| metric       | _string_  | `count`                                                                                 |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| token        | _string_  | `btc`                                                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field  | Type      | Description                                                                                                                                         |
| ------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| date   | _string_  | The date in _YYYY-MM-DD_                                                                                                                            |
| <1d    | _decimal_ | The count of unspent outputs (UTXOs) on this date from transactions that occurred less than a day prior to this date.       |
| 1d-1w  | _decimal_ | The count of unspent outputs (UTXOs) on this date from transactions that occurred 1 day to 1 week prior to this date.       |
| 1w-1m  | _decimal_ | The count of unspent outputs (UTXOs) on this date from transactions that occurred 1 week to 1 month prior to this date.     |
| 1-3m   | _decimal_ | The count of unspent outputs (UTXOs) on this date from transactions that occurred 1 to 3 months prior to this date.         |
| 3-6m   | _decimal_ | The count of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 6 months prior to this date.         |
| 6-12m  | _decimal_ | The count of unspent outputs (UTXOs) on this date from transactions that occurred 6 to 12 months prior to this date.        |
| 12-18m | _decimal_ | The count of unspent outputs (UTXOs) on this date) from transactions that occurred 12 to 18 months prior to this date.       |
| 18-24m | _decimal_ | The count of unspent outputs (UTXOs) on this date from transactions that occurred 18 to 24 months prior to this date.       |
| 2-3y   | _decimal_ | The count of unspent outputs (UTXOs) on this date from transactions that occurred 2 to 3 years prior to this date.          |
| 3-5y   | _decimal_ | The count of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 5 years prior to this date.          |
| 5-10y  | _decimal_ | The count of unspent outputs (UTXOs) on this date from transactions that occurred 5 to 10 years prior to this date.         |
| >10y   | _decimal_ | The count of unspent outputs (UTXOs) on this date from transactions that occurred greater than 10 years prior to this date. |  

## BTC UTXO Median Age

This endpoint returns the median age of the current bitcoin supply held in unspent transaction outputs stratified by their age. For instance outputs in the category `12-18m` are unspent outputs (UTXOs) from transactions that occurred `12-18m` ago. Time is measured relative to blocktime assuming 6 blocks are generated per hour. This means that the median age of UTXOs in the `<1d` category were generated less than or equal to `144 blocks ago (6 blocks * 24 hours)`.

The age in block height is used over the block timestamp because the block timestamp serves as a source of variation when calculating the blockhash and is only accurate to within an hour or two. By using timestamps some UTXOs could be considered older than a previously generated UTXO. By using block-age from current the blockheight, the age of utxos is strictly ordinal as blockheight is strictly sequential.


<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last?metric=count&limit=2&window=1d&format=json&token=btc&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
   "date": "2019-10-16",
   "1-3m": 1428.5,
   "12-18m": 10879.8333,
   "18-24m": 15663.8333,
   "1d-1w": 88.5,
   "1w-1m": 430.5,
   "2-3y": 21493.1667,
   "3-5y": 35925.1667,
   "3-6m": 3146.5,
   "5-10y": 55743.8333,
   "6-12m": 6271.8333,
   "<1d": 11.5,
   ">10y": 96415.8333
  },
  {
   "date": "2019-10-17",
   "1-3m": 1435.8333,
   "12-18m": 10885.1667,
   "18-24m": 15663.8333,
   "1d-1w": 87.3333,
   "1w-1m": 433.1667,
   "2-3y": 21482.5,
   "3-5y": 35903.8333,
   "3-6m": 3149.1667,
   "5-10y": 55765.1667,
   "6-12m": 6266.5,
   "<1d": 10.3333,
   ">10y": 96426.5
}
  }
]
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| metric       | _string_  | `median_age`                                                                                 |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| token        | _string_  | `btc`                                                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field  | Type      | Description                                                                                                                                         |
| ------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| date   | _string_  | The date in _YYYY-MM-DD_                                                                                                                            |
| <1d    | _decimal_ | The median age of unspent outputs (UTXOs) on this date from transactions that occurred less than a day prior to this date.       |
| 1d-1w  | _decimal_ | The median age of unspent outputs (UTXOs) on this date from transactions that occurred 1 day to 1 week prior to this date.       |
| 1w-1m  | _decimal_ | The median age of unspent outputs (UTXOs) on this date from transactions that occurred 1 week to 1 month prior to this date.     |
| 1-3m   | _decimal_ | The median age of unspent outputs (UTXOs) on this date from transactions that occurred 1 to 3 months prior to this date.         |
| 3-6m   | _decimal_ | The median age of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 6 months prior to this date.         |
| 6-12m  | _decimal_ | The median age of unspent outputs (UTXOs) on this date from transactions that occurred 6 to 12 months prior to this date.        |
| 12-18m | _decimal_ | The median age of unspent outputs (UTXOs) on this date) from transactions that occurred 12 to 18 months prior to this date.       |
| 18-24m | _decimal_ | The median age of unspent outputs (UTXOs) on this date from transactions that occurred 18 to 24 months prior to this date.       |
| 2-3y   | _decimal_ | The median age of unspent outputs (UTXOs) on this date from transactions that occurred 2 to 3 years prior to this date.          |
| 3-5y   | _decimal_ | The median age of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 5 years prior to this date.          |
| 5-10y  | _decimal_ | The median age of unspent outputs (UTXOs) on this date from transactions that occurred 5 to 10 years prior to this date.         |
| >10y   | _decimal_ | The median age of unspent outputs (UTXOs) on this date from transactions that occurred greater than 10 years prior to this date. | 

## BTC UTXO Total Value

This endpoint returns the total BTC value of the current bitcoin supply held in unspent transaction outputs stratified by their age. For instance outputs in the category `12-18m` are unspent outputs (UTXOs) from transactions that occurred `12-18m` ago. Time is measured relative to blocktime assuming 6 blocks are generated per hour. This means that the BTC value of UTXOs in the `<1d` category were generated less than or equal to `144 blocks ago (6 blocks * 24 hours)`.

The age in block height is used over the block timestamp because the block timestamp serves as a source of variation when calculating the blockhash and is only accurate to within an hour or two. By using timestamps some UTXOs could be considered older than a previously generated UTXO. By using block-age from current the blockheight, the age of utxos is strictly ordinal as blockheight is strictly sequential.


<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last?metric=count&limit=2&window=1d&format=json&token=btc&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
   "date": "2019-10-16",
   "1-3m": 1777347.3869,
   "12-18m": 1158032.9532,
   "18-24m": 2078703.5591,
   "1d-1w": 426700.584,
   "1w-1m": 1059641.5382,
   "2-3y": 1704598.3775,
   "3-5y": 967616.1339,
   "3-6m": 2105447.8466,
   "5-10y": 2300642.2641,
   "6-12m": 2584202.2294,
   "<1d": 173486.1721,
   ">10y": 1659664.5
  },
  {
   "date": "2019-10-17",
   "1-3m": 1770545.9191,
   "12-18m": 1151530.6676,
   "18-24m": 2083877.5908,
   "1d-1w": 438182.7858,
   "1w-1m": 935844.8516,
   "2-3y": 1711474.8656,
   "3-5y": 968321.7507,
   "3-6m": 2108284.9723,
   "5-10y": 2299152.7543,
   "6-12m": 2578503.3151,
   "<1d": 291163.752,
   ">10y": 1661075.32
}
  }
]
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| metric       | _string_  | `total_value`                                                                                 |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| token        | _string_  | `btc`                                                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field  | Type      | Description                                                                                                                                         |
| ------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| date   | _string_  | The date in _YYYY-MM-DD_                                                                                                                            |
| <1d    | _decimal_ | The total value of unspent outputs (UTXOs) on this date from transactions that occurred less than a day prior to this date.       |
| 1d-1w  | _decimal_ | The total value of unspent outputs (UTXOs) on this date from transactions that occurred 1 day to 1 week prior to this date.       |
| 1w-1m  | _decimal_ | The total value of unspent outputs (UTXOs) on this date from transactions that occurred 1 week to 1 month prior to this date.     |
| 1-3m   | _decimal_ | The total value of unspent outputs (UTXOs) on this date from transactions that occurred 1 to 3 months prior to this date.         |
| 3-6m   | _decimal_ | The total value of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 6 months prior to this date.         |
| 6-12m  | _decimal_ | The total value of unspent outputs (UTXOs) on this date from transactions that occurred 6 to 12 months prior to this date.        |
| 12-18m | _decimal_ | The total value of unspent outputs (UTXOs) on this date) from transactions that occurred 12 to 18 months prior to this date.       |
| 18-24m | _decimal_ | The total value of unspent outputs (UTXOs) on this date from transactions that occurred 18 to 24 months prior to this date.       |
| 2-3y   | _decimal_ | The total value of unspent outputs (UTXOs) on this date from transactions that occurred 2 to 3 years prior to this date.          |
| 3-5y   | _decimal_ | The total value of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 5 years prior to this date.          |
| 5-10y  | _decimal_ | The total value of unspent outputs (UTXOs) on this date from transactions that occurred 5 to 10 years prior to this date.         |
| >10y   | _decimal_ | The total value of unspent outputs (UTXOs) on this date from transactions that occurred greater than 10 years prior to this date. |  

## BTC UTXO Weighted Average Age

This endpoint returns the weighted average age of the current bitcoin supply held in unspent transaction outputs stratified by their age.
The weighted average age is sum of the ages of UTXOs multiplied by their bitocoinvalue, divided by the total bitcoin value in that stratum. For instance outputs in the category `12-18m` are unspent outputs (UTXOs) from transactions that occurred `12-18m` ago. Time is measured relative to blocktime assuming 6 blocks are generated per hour. This means that the proportion of UTXOs in the `<1d` category were generated less than or equal to `144 blocks ago (6 blocks * 24 hours)`.

<img src="images/weight_avg_age_eqn.svg"/>

The age in block height is used over the block timestamp because the block timestamp serves as a source of variation when calculating the blockhash and is only accurate to within an hour or two. By using timestamps some UTXOs could be considered older than a previously generated UTXO. By using block-age from current the blockheight, the age of utxos is strictly ordinal as blockheight is strictly sequential.


<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last?metric=count&limit=2&window=1d&format=json&token=btc&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
   "date": "2019-10-16",
   "1-3m": 1545.2336,
   "12-18m": 11035.8792,
   "18-24m": 15596.1418,
   "1d-1w": 76.1194,
   "1w-1m": 451.0636,
   "2-3y": 20471.2648,
   "3-5y": 33903.6172,
   "3-6m": 3142.9224,
   "5-10y": 64551.2214,
   "6-12m": 6871.3697,
   "<1d": 10.3378,
   ">10y": 95306.9022
  },
  {
   "date": "2019-10-17",
   "1-3m": 1553.5454,
   "12-18m": 11016.0713,
   "18-24m": 15595.3426,
   "1d-1w": 78.7768,
   "1w-1m": 452.0231,
   "2-3y": 20477.4807,
   "3-5y": 33919.834,
   "3-6m": 3157.0836,
   "5-10y": 64560.6276,
   "6-12m": 6884.0698,
   "<1d": 6.1814,
   ">10y": 95325.3456
}
}
  }
]
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_utxo_metric_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| metric       | _string_  | `weighted_avg_age`                                                                                 |
| window       | _string_  | `1d` (no support for 1h at this time)                                                     |
| token        | _string_  | `btc`                                                                                     |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field  | Type      | Description                                                                                                                                         |
| ------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1-3m   | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date from transactions that occurred 1 to 3 months prior to this date.         |
| 12-18m | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date) from transactions that occurred 12 to 18 months prior to this date.       |
| 18-24m | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date from transactions that occurred 18 to 24 months prior to this date.       |
| 1d-1w  | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date from transactions that occurred 1 day to 1 week prior to this date.       |
| 1w-1m  | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date from transactions that occurred 1 week to 1 month prior to this date.     |
| 2-3y   | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date from transactions that occurred 2 to 3 years prior to this date.          |
| 3-5y   | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 5 years prior to this date.          |
| 3-6m   | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date from transactions that occurred 3 to 6 months prior to this date.         |
| 5-10y  | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date from transactions that occurred 5 to 10 years prior to this date.         |
| 6-12m  | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date from transactions that occurred 6 to 12 months prior to this date.        |
| <1d    | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date from transactions that occurred less than a day prior to this date.       |
| >10y   | _decimal_ | The weighted average age of unspent outputs (UTXOs) on this date from transactions that occurred greater than 10 years prior to this date. |
| date   | _string_  | The date in _YYYY-MM-DD_   
