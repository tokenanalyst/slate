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
curl "https://api.tokenanalyst.io/analytics/private/v1/token_volume_historical/last?format=json&token=zrx&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2017-08-11",
    "volume": "1.00001170833E9",
    "price_usd": "0.11",
    "volume_usd": "1.1305799085E8"
  },
  {
    "date": "2017-08-13",
    "volume": "8.275E7",
    "price_usd": "0.18",
    "volume_usd": "1.490913652E7"
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
curl "https://api.tokenanalyst.io/analytics/private/v1/token_count_historical/last?format=json&token=mana&key=API_KEY"
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
| token     | _string_ | The token you want the transaction count for        |
