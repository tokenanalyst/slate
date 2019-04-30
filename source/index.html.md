---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href="https://sid296635.typeform.com/to/abg0kL" target="_blank">Get your API key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the TokenAnalyst API. We provide simple and powerful endpoints, which you can use to get information on basic transaction data and aggregate on-chain statistics derived directly from the blockchain. This API reference provides information on available endpoints and how to interact with it.

# Authentication

TokenAnalyst uses API keys to allow access to the API. To obtain your API key contact us <a href="https://sid296635.typeform.com/to/abg0kL" target="_blank">here</a>
.

TokenAnalyst expects for the API key to be included in all API requests to the server. You can simply include the key in the URL parameters like:

`key=API_KEY`

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: API_KEY"
```

<aside class="notice">
You must replace <code>API_KEY</code> with your personal API key.
</aside>

# Bitcoin Blockchain Stats

## On-chain Volume

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&key=aeab6c818c7a5bda1c88432628589ec64ddf7bb4153639177f60258b9bb86451&token=btc"
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

| Parameter | Type     | Description                                                   |
| --------- | -------- | ------------------------------------------------------------- |
| key       | _string_ | Your unique API key                                           |
| format    | _string_ | What format you want your data in (currently we support JSON) |
| token     | _string_ | The token you want the volume for (in this case `btc`)        |

## On-chain Transaction Count

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&key=aeab6c818c7a5bda1c88432628589ec64ddf7bb4153639177f60258b9bb86451&token=btc"
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

| Parameter | Type     | Description                                                   |
| --------- | -------- | ------------------------------------------------------------- |
| key       | _string_ | Your unique API key                                           |
| format    | _string_ | What format you want your data in (currently we support JSON) |
| token     | _string_ | The token you want the volume for (in this case `btc`)        |

# Ethereum Blockchain Stats

## On-chain Volume

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&key=aeab6c818c7a5bda1c88432628589ec64ddf7bb4153639177f60258b9bb86451&token=eth"
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

This endpoint returns the full historical on-chain volume of Ethereum since it's genesis in 2015. The volume is separated into 'internal' volume and 'external' volume.

'Internal' transactions are transfers of ETH that are initiated by smart contracts. While contracts can't initiate transactions on their own, when certain functions are called on from the outside, the smart contract can generate transfers of ETH towards multiple addresses (other contracts and non-contract addresses). At TokenAnalyst, we track every function call and event that happens on Ethereum and thus we are able to derive an accurate 'internal' ETH on-chain volume (something that is missed by many data providers). The 'external' transaction volume is that which can be seen on the surface by looking at the blockchain using standard web3 calls - 'normal' ETH transactions mined on each block.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last`

### Query Parameters

| Parameter | Type     | Description                                                   |
| --------- | -------- | ------------------------------------------------------------- |
| key       | _string_ | Your unique API key                                           |
| format    | _string_ | What format you want your data in (currently we support JSON) |
| token     | _string_ | The token you want the volume for (in this case `eth`)        |

## On-chain Transaction Count

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&key=aeab6c818c7a5bda1c88432628589ec64ddf7bb4153639177f60258b9bb86451&token=eth"
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

This endpoint returns the number of transactions on the full historical Ethereum blockchain for every day since it's genesis in 2009.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last`

### Query Parameters

| Parameter | Type     | Description                                                   |
| --------- | -------- | ------------------------------------------------------------- |
| key       | _string_ | Your unique API key                                           |
| format    | _string_ | What format you want your data in (currently we support JSON) |
| token     | _string_ | The token you want the volume for (in this case `eth`)        |
