---
title: TokenAnalyst Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href="https://sid296635.typeform.com/to/abg0kL" target="_blank">Get your API key</a>

# includes:
#   - errors

search: true
---

# Introduction

Welcome to the TokenAnalyst API. We provide simple and powerful endpoints, which you can use to get information on basic transaction data and aggregate on-chain statistics derived directly from the blockchain. This API reference provides information on available endpoints and how to interact with them.

# Authentication

TokenAnalyst uses API keys to allow access to the API. To obtain your API key contact us <a href="https://sid296635.typeform.com/to/abg0kL" target="_blank">here</a>
.

TokenAnalyst expects for the API key to be included in all API requests to the server. You can simply include the key in the URL parameters like:

`key=API_KEY`

<aside class="notice">
You must replace <code>API_KEY</code> with your personal API key.
</aside>

# Bitcoin Blockchain Stats

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

# Ethereum Blockchain Stats

## On-chain Volume

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

## On-chain Transaction Count

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

# ERC20 Token Stats

ERC20 tokens we currently support are:

| Name                  | Symbol  |
| --------------------- | ------- |
| Binance Coin          | `bnb`   |
| Maker                 | `mkr`   |
| Basic Attention Token | `bat`   |
| Venchain              | `ven`   |
| OmiseGo               | `omg`   |
| Augur                 | `rep`   |
| Golem                 | `gnt`   |
| ZRX                   | `zrx`   |
| Zilliqa               | `zil`   |
| Decentraland          | `mana`  |
| Numerai               | `nmr`   |
| Storj                 | `storj` |
| Tokencard             | `tkn`   |
| Bancor                | `bnt`   |
| Icon                  | `icx`   |
| Loom Network          | `loom`  |
| Status                | `snt`   |
| Civic                 | `cvc`   |
| Kyber Network         | `knc`   |
| iExec RLC             | `rlc`   |

## On-chain Volume

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&key=API_KEY&token=btc"
```

> The above command returns JSON structured like this:

```json
[
  {
    "address": "0xE41d2489571d322189246DaFA5ebDe1F4699F498",
    "date": "2017-10-07",
    "volume": "6388336.865940487",
    "price_usd": "0.19459583",
    "volume_usd": "1243143.7061382495"
  },
  {
    "address": "0xE41d2489571d322189246DaFA5ebDe1F4699F498",
    "date": "2017-10-08",
    "volume": "1.7540869392539065E7",
    "price_usd": "0.19433333",
    "volume_usd": "3408775.5565827326"
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

## On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&key=API_KEY&token=mana"
```

> The above command returns JSON structured like this:

```json
[
  {
    "tokenaddress": "0x0F5D2fB29fb7d3CFeE444a200298f468908cC942",
    "date": "2017-09-06",
    "number_of_token_transfers": "4"
  },
  {
    "tokenaddress": "0x0F5D2fB29fb7d3CFeE444a200298f468908cC942",
    "date": "2017-09-15",
    "number_of_token_transfers": "5512"
  },
  {
    "tokenaddress": "0x0F5D2fB29fb7d3CFeE444a200298f468908cC942",
    "date": "2017-09-16",
    "number_of_token_transfers": "4822"
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
| token     | _string_ | The token you want the transaction count for                   |

# Stablecoin Stats

The stablecoins we currently support are:

| Name                 | Symbol |
| -------------------- | ------ |
| Tether               | `usdt` |
| USDC                 | `usdc` |
| Paxos Standard Token | `pax`  |
| TrueUSD              | `tusd` |
| Gemini Dollar        | `gusd` |
| Dai                  | `dai`  |

## On-chain Volume

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&key=API_KEY&token=usdc"
```

> The above command returns JSON structured like this:

```json
[
  {
    "address": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
    "date": "2018-09-10",
    "volume": "22.2",
    "price_usd": "0.0",
    "volume_usd": "0.0"
  },
  {
    "address": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
    "date": "2018-09-12",
    "volume": "2.5",
    "price_usd": "0.0",
    "volume_usd": "0.0"
  }
]
```

This endpoint returns the full historical on-chain volume of any of the stablecoins that we support.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The token you want the volume for                   |

## On-chain Transaction Count

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&key=API_KEY&token=dai"
```

> The above command returns JSON structured like this:

```json
[
  {
    "tokenaddress": "0x89d24A6b4CcB1B6fAA2625fE562bDD9a23260359",
    "date": "2017-12-18",
    "number_of_token_transfers": "161"
  },
  {
    "tokenaddress": "0x89d24A6b4CcB1B6fAA2625fE562bDD9a23260359",
    "date": "2017-12-19",
    "number_of_token_transfers": "599"
  },
  {
    "tokenaddress": "0x89d24A6b4CcB1B6fAA2625fE562bDD9a23260359",
    "date": "2017-12-20",
    "number_of_token_transfers": "515"
  }
]
```

This endpoint returns the number of token transfers on the Ethereum blockchain for the given stablecoin for every day since its existence.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | The stablecoin you want the transaction count for                   |

# Bitcoin Exchange Flows

For Bitcoin currently supported exchanges are: `binance`, `bittrex`, `bitstamp`, `poloniex`, `bitmex`, `bitfinex`

## Full Historical Inflow to Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the inflow of BTC into exchange wallets for as far back as we track. The average inflow is the average transaction value for transactions flowing into exchange wallets on a given day. 

```shell
curl "https://ws.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?format=json&key=API_KEY&token=btc&exchange=binance&direction=inflow"
```

> The response looks like:

```json
[
  {
    "avg_txn_value": "0.01",
    "date": "2017-06-23",
    "entity": "Binance",
    "inflow": "0.01",
    "number_of_entity_receiving_addresses": "1",
    "number_of_nonentity_sending_addresses": "1",
    "number_of_txns": "1",
    "inflow_usd": "27.34",
    "avg_txn_value_usd": "27.34"
  }
]
```

### HTTP Request

`GET https://ws.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?`

### URL Parameters

| Parameter | Type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| key       | _string_ | Your unique API key                                  |
| format    | _string_ | What format you want your data in (`json` or `csv`)  |
| token     | _string_ | `btc`                                                |
| direction | _string_ | Either `inflow` or `outflow` (in this case `inflow`) |
| exchange  | _string_ | An exchange from the list of ones we support         |

## Full Historical Outflows from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the outflow of BTC from exchange wallets for as far back as we track. The average outflow is the average transaction value for transactions flowing out of exchange wallets on a given day. 


### HTTP Request

`GET https://ws.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?`

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?token=btc&exchange=binance&direction=outflow&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "avg_txn_value": "26.73",
    "date": "2017-07-05",
    "entity": "Binance",
    "number_of_entity_sending_addresses": "23",
    "number_of_nonentity_receiving_addresses": "1",
    "number_of_txns": "3",
    "outflow": "26.73",
    "outflow_usd": "69375.93",
    "avg_txn_value_usd": "69375.93"
  }
]
```

### URL Parameters

| Parameter | Type     | Description                                           |
| --------- | -------- | ----------------------------------------------------- |
| key       | _string_ | Your unique API key                                   |
| format    | _string_ | What format you want your data in (`json` or `csv`)   |
| token     | _string_ | `btc`                                                 |
| direction | _string_ | Either `inflow` or `outflow` (in this case `outflow`) |
| exchange  | _string_ | An exchange from the list of ones we support          |

## Full Historical Top 10 Inflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the top 10 transactions (in terms of total BTC sent) flowing into exchange wallets for every day that the exchange wallets we track have been live on the blockchain. 


### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?`

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?token=btc&exchange=binance&direction=inflow&format=json&key=API_KEY"
```

> This is what the response looks like

```json
[
  {
    "date": "2017-06-23",
    "entity": "Binance",
    "rank": "1",
    "transactionhash": "0546f2545393d706b3b77ec251be93af12038dc28eefd5dc0d27acea9f0613a0",
    "transactionid": "0546f2545393d706b3b77ec251be93af12038dc28eefd5dc0d27acea9f0613a0",
    "value": "0.01",
    "value_usd": "52.51"
  }
]
```

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `btc`                                               |
| direction | _string_ | `inflow`                                            |
| exchange  | _string_ | An exchange from the list of ones we support        |

# Ethereum Exchange Flows

For Ethereum currently supported exchanges are: `binance`, `kraken`, `bitfinex`, `poloniex`, `bittrex`, `kucoin`

## Full Historical Inflow to Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the inflow of ETH into exchange wallets for as far back as we track. The average inflow is the average transaction value for transactions flowing into exchange wallets on a given day. 


### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_historical/last?`

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?token=eth&exchange=binance&direction=inflow&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2016-03-17",
    "inflow": "1.8164",
    "price": "11.640834",
    "inflow_usd": "21.144410613632203",
    "number_of_txns": "8",
    "avg_inflow": "0.22705",
    "avg_inflow_usd": "2.6430513267040254"
  }
]
```

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |
| direction | _string_ | `inflow`                                            |
| exchange  | _string_ | An exchange from the list of ones we support        |

## Full Historical Outflows from Exchanges

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the outflow of ETH from exchange wallets for as far back as we track. The average outflow is the average transaction value for transactions flowing out of exchange wallets on a given day. 

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?`

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_historical/last?token=eth&exchange=binance&direction=outflow&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "date": "2017-08-05",
    "outflow": "89.82616451000001",
    "price": "238.7136",
    "outflow_usd": "21442.72643330973",
    "number_of_txns": "18",
    "avg_outflow": "4.990342472777779",
    "avg_outflow_usd": "1191.2625796283182"
  }
]
```

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |
| direction | _string_ | `outflow`                                           |
| exchange  | _string_ | An exchange from the list of ones we support        |

## Full Historical Top 10 Inflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the top 10 transactions (in terms of total ETH sent) flowing into exchange wallets for every day that the exchange wallets we track have been live on the blockchain. 

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_top10_historical/last?`

> This is an example:

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?token=btc&exchange=binance&direction=inflow&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "toaddress": "0x7eD1E469fCb3EE19C0366D829e291451bE638E59",
    "fromaddress": "0x5207Df8126b150f4D332D646cd4608de95e65C0d",
    "transactionhash": "0xbe03be5a0d978d11f746358165c2287be1aad08c9f0ebeb326443a1c2b98a57a",
    "value": "1.09895",
    "date": "2016-03-17",
    "rank": "1",
    "value_usd": "12.79"
  }
]
```

### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |
| direction | _string_ | `inflow`                                            |
| exchange  | _string_ | An exchange from the list of ones we support        |

## Full Historical Top 10 Outflow Large Value Transactions

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the top 10 transactions (in terms of total ETH sent) flowing out of exchange wallets for every day that the exchange wallets we track have been live on the blockchain. 

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_top10_historical/last?`

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_top10_historical/last?token=btc&exchange=binance&direction=outflow&format=json&key=API_KEY"
```

> The response looks like:

```json
[
  {
    "toaddress": "0x70077eA7a9f6322F229261596EAdca64DC1b1e25",
    "fromaddress": "0x3f5CE5FBFe3E9af3971dD833D26bA9b5C936f0bE",
    "transactionhash": "0xf7e7b5a201d26b605e2f29d54878b4abc0e8c03bba6d691e0177deffef2b46f5",
    "value": "15.159998190000001",
    "date": "2017-08-05",
    "rank": "1",
    "value_usd": "3618.9"
  }
]
```


### URL Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | `eth`                                               |
| direction | _string_ | `outflow`                                           |
| exchange  | _string_ | An exchange from the list of ones we support        |
