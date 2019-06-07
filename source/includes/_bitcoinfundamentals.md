# Bitcoin Fundamentals

## BTC On-chain Volume

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

## BTC On-chain Transaction Count

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

## BTC Active addresses

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

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
| token     | _string_ | `btc`                                               |

## BTC Supply

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_supply_historical/last?&token=btc&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2009-01-12",
    "supply": "50"
  },
  {
    "date": "2009-01-13",
    "supply": "750"
  }
]
```

This endpoint returns the historical supply of BTC on the Bitcoin blockchain for every day of its existence.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_supply_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |

## BTC NVT

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_nvt_historical/last?&token=btc&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2014-09-24",
    "marketcap_usd": "5708841339.86",
    "nvt": "33.195"
  },
  {
    "date": "2014-09-25",
    "marketcap_usd": "5516694629.19",
    "nvt": "35.833"
  }
]
```

This endpoint returns the NVT Ratio (Network Value to Transactions Ratio) for BTC. This is the ratio of the Market Cap divided by the volume transmitted by the blockchain. Special thanks to Willy Woo and Chris Burniske for coming up with it!

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_nvt_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |

## BTC Fees

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_fees_historical/last?&token=btc&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "day": "2012-08-10",
    "total_fee": 44.53058517,
    "avg_size_bytes": 403,
    "price": 9.1,
    "total_fee_usd": 405.23,
    "avg_satoshis_per_byte": 389,
    "avg_fee": 156935.983,
    "avg_fee_usd": 0.01
  },
  {
    "day": "2012-08-11",
    "total_fee": 19.13775992,
    "avg_size_bytes": 393,
    "price": 9.1,
    "total_fee_usd": 174.15,
    "avg_satoshis_per_byte": 147,
    "avg_fee": 57749.962,
    "avg_fee_usd": 0.01
  }
]
```

This endpoint returns the total and average fees spent on the Bitcoin network for every day of it's existence. The `total_fee` is denominated in Bitcoin, the `price` is the price of Bitcoin on that day, and the `avg_fee` is denominated in Bitcoin.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_nvt_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |
