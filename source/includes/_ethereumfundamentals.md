# Ethereum Fundamentals

## ETH On-chain Volume

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&key=API_KEY&token=eth"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2015-08-07",
    "volume_internal": "39.7",
    "volume_external": "2008602.5114319662",
    "price_usd": "1.25",
    "volume_internal_usd": "49.625",
    "volume_external_usd": "2510753.139289958"
  },
  {
    "date": "2015-08-08",
    "volume_internal": "3568.434161233944",
    "volume_external": "1681503.1468948543",
    "price_usd": "1.7404166",
    "volume_internal_usd": "6210.56221437989",
    "volume_external_usd": "2926516.067163448"
  }
]
```

This endpoint returns the full historical on-chain volume of Ethereum since it went live in 2015. The volume is separated into 'internal' volume and 'external' volume.

'Internal' transactions are transfers of ETH that are initiated by smart contracts. While contracts can't initiate transactions on their own, when certain functions are called on from the outside, the smart contract can generate transfers of ETH towards multiple addresses (other contracts and non-contract addresses). At TokenAnalyst, we track every function call and event that happens on Ethereum and thus we are able to derive an accurate 'internal' ETH on-chain volume. The 'external' transaction volume is that which can be seen on the surface by looking at the blockchain using standard web3 calls - 'normal' ETH transactions included on each block.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `eth`) |

## ETH On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&key=API_KEY&token=eth"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2015-08-07",
    "number_of_txns": "1975"
  },
  {
    "date": "2015-08-08",
    "number_of_txns": "2036"
  },
  {
    "date": "2015-08-09",
    "number_of_txns": "1249"
  }
]
```

This endpoint returns the number of transactions on the full historical Ethereum blockchain for every day since its genesis in 2015.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last`

### Query Parameters

| Parameter | Type     | Description                                            |
| --------- | -------- | ------------------------------------------------------ |
| key       | _string_ | Your unique API key                                    |
| format    | _string_ | What format you want your data in (`json` or `csv`)    |
| token     | _string_ | The token you want the volume for (in this case `eth`) |


## ETH Active addresses

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last?&token=eth&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2016-11-11",
    "active_senders": "9513",
    "active_receivers": "14658"
  },
  {
    "date": "2016-11-12",
    "active_senders": "8838",
    "active_receivers": "13746"
  }
]
```

This endpoint returns the active addresses on the Ethereum blockchain for every day of its existence. An address is defined as 'active' if it has transacted during the given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_active_address_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`    

## ETH Supply

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_supply_historical/last?&token=eth&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2015-07-30",
    "supply": "39311.09375",
  },
  {
    "date": "2015-07-31",
    "supply": "75502.8125"
  }
]
```

This endpoint returns the historical supply of ETH on the Ethereum blockchain for every day of its existence.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_supply_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`  

## ETH NVT

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_nvt_historical/last?&token=eth&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2015-09-02",
    "marketcap_usd": "98056055.37",
    "nvt": "262.70"
  },
  {
    "date": "2015-09-03",
    "marketcap_usd": "91877253.74",
    "nvt": "130.90"
  }
]
```

This endpoint returns the NVT Ratio (Network Value to Transactions Ratio) for ETH. This is the ratio of the Market Cap divided by the volume transmitted by the blockchain. Special thanks to Willy Woo and Chris Burniske for coming up with it!

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_nvt_historical/last`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`  