# DeFi metrics

The decentralized finance (DeFi) projects we currently cover are

| Name     | API Parameter |
| -------- | ------------- |
| Dharma   | `dharma`      |
| Compound | `compound`    |

## Number of loans originated

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/project_loans_originated_historical/last?project=dharma&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2019-03-14 00:00:00.000",
    "loans_originated": 4
  },
  {
    "date": "2019-03-15 00:00:00.000",
    "loans_originated": 20
  }
]
```

This endpoint returns the number of loans that have been originated in various decentralized finance ('DeFi') projects throughout the project's lifespan on the blockchain.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/project_loans_originated_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| project   | _string_ | An project from the list of ones we cover (Above)   |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| date       | _string_ | The date in _YYYY-MM-DD_  _HH:MM:SS.MS_ |
| loans_originated | _integer_ | The number of loans originated on the specified de-fi project on this date. |



## Loan Origination Stats By Token

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/project_loan_stats_historical/last?project=compound&format=json&key=API_KEY"
```

> The response looks like:

```json
[
    {
        "date": "2019-05-07",
        "token": "DAI",
        "txns": 3,
        "volume": 4024.14,
        "volume_usd": 4186.93,
        "price": 1.04
    },
    {
        "date": "2019-05-07",
        "token": "ETH",
        "txns": 8,
        "volume": 16.30051781573815,
        "volume_usd": 2883.87,
        "price": 176.92
    }
]
```

This endpoint returns the number of transactions, volume, and volume_usd by date of loans generated (by token) on the Compound Protocol

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/project_loan_stats_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| project   | _string_ | An project from the list of ones we cover (Above)   |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| date       | _string_ | The date in _YYYY-MM-DD_ |
| token | _string_ | The symbol of the token that is being used for the loan that is being generated |
| txns | _string_ | The number of transactions (of the specified token) related to loan generations on Compound. |
| volume | _string_ | The total amount of the specified token given out in loans generated on Compound on this date. Denominated in the specified token. |
| volume_usd | _string_ | _volume_ * _price_  |
| price | _string_ | The daily average price of the specified token in USD (the daily mean of minute-level price data) |
