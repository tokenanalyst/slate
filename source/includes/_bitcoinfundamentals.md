# Bitcoin Fundamentals

## On-chain Volume

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&key=API_KEY&token=btc"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2009-04-13",
    "volume_gross": "50.0",
    "volume_change": "40.0",
    "volume_real": "10.0",
    "price_usd": "",
    "volume_real_usd": "",
    "volume_change_usd": ""
  },
  {
    "date": "2009-04-18",
    "volume_gross": "182.51",
    "volume_change": "17.49",
    "volume_real": "165.01999999999998",
    "price_usd": "",
    "volume_real_usd": "",
    "volume_change_usd": ""
  }
]
```

This endpoint returns the full historical on-chain volume of Bitcoin since it's genesis in 2009. The volume is separated into 'real' volume and 'change' volume.

Our current heuristic for 'change' related volume is for whenever BTC in a transaction is sent back to the same address that sent the BTC. The 'real' volume is simply the remainder left over after subtracting the change.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `btc`) |

## On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&key=API_KEY&token=btc"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2009-03-12",
    "number_of_txns": "119"
  },
  {
    "date": "2009-03-13",
    "number_of_txns": "114"
  },
  {
    "date": "2009-03-14",
    "number_of_txns": "110"
  }
]
```

This endpoint returns the number of transactions on the full historical Bitcoin blockchain for every day since it's genesis in 2009.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `btc`) |

## Active addresses

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last?&token=btc&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2009-01-12",
    "active_senders": "3",
    "active_recipients": "1"
  },
  {
    "date": "2009-01-14",
    "active_senders": "3",
    "active_recipients": "0"
  }
]
```

This endpoint returns the active addresses on the Bitcoin blockchain for every day of its existence. An address is defined as 'active' if it has transacted during the given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`  