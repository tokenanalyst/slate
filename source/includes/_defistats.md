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