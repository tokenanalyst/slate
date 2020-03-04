# Exchange Flows

For the native tokens, the exchanges we currently support are:

| Native Token          | Symbol | Supported Exchanges                                                                                       |
------------------------|--------|-----------------------------------------------------------------------------------------------------------|
| Bitcoin               | `btc`  | `binance`, `bittrex`, `bitstamp`, `bitmex`, `bitfinex`, `deribit`, `huobi`, `kraken`, `okex`, `poloniex`  | 
| Ethereum              | `eth`  | `binance`, `bittrex`, `bitstamp`, `bitfinex`, `gemini`, `huobi`, `kraken`, `kucoin`, `okex`, `poloniex`   |

For stablecoins, the exchanges we currently support are:

| Name                 | Symbol       | Supported Exchanges                                    |
| -------------------- | ------------ | ------------------------------------------------------ |
| Tether (Omni)        | `usdt_omni`  | `bitfinex`, `kraken`, `huobi`, `okex`, `poloniex`      |
| Tether               | `usdt_erc20` | `binance`, `bitfinex`, `bittrex`, `kucoin`, `poloniex` |
| USD Coin             | `usdc`       | `binance`, `bitfinex`
| Paxos Standard Token | `pax`        | `binance`, `bitfinex`, `bittrex`
| TrueUSD              | `tusd`       | `binance`, `bittrex`
| Multi-Collateral Dai | `dai`        | `bittrex`

For ERC20 tokens, the exchanges we currently support are:

| ERC20 token                   | Symbol | Supported exchanges |
| ------------------------------| ------ | ------------------- |
| Maker                         | `mkr`  | `bittrex`, `kucoin` |
| Basic Attention Token         | `bat`  | `binance`, `bittrex`, `poloniex` |
| OmiseGo                       | `omg`  | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Augur                         | `rep`  | `binance`, `bittrex`, `kraken`, `poloniex` |
| Golem                         | `gnt`  | `binance`, `bittrex`, `poloniex` |
| ZRX                           | `zrx`  | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Decentraland                  | `mana` | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Numerai                       | `nmr`  | `bittrex` |
| Loom Network                  | `loom` | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Status                        | `snt`  | `kucoin`, `poloniex` |
| Civic                         | `cvc`  | `binance`, `bittrex`, `kucoin`, `poloniex` |
| Kyber Network                 | `knc`  | `binance`, `kucoin`, `poloniex` |
| iExec RLC                     | `rlc`  | `bittrex` |
| ChainLink                     | `link` | `binance` |

## Full Historical Inflows

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the inflow of a given token we support from exchange wallets for as far back as we track. The average inflow is the average transaction value for transactions flowing into exchange wallets on a given day.

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?format=json&token=btc&exchange=binance&direction=inflow&window=1h&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-10-04",
    "hour": "11:00:00", // not available when window 1d
    "datetime": "2019-10-04 11:00:00", // not available when window 1d
    "inflow": 146.78124811,
    "inflow_usd": 1197591.43,
    "number_of_txns": 358,
    "avg_txn_value": 0.41000349,
    "avg_txn_value_usd": 3345.23
  },
  {
    "date": "2019-10-04",
    "hour": "12:00:00", // not available when window 1d
    "datetime": "2019-10-04 12:00:00", // not available when window 1d
    "inflow": 134.97661825,
    "inflow_usd": 1101849.66,
    "number_of_txns": 177,
    "avg_txn_value": 0.76257976,
    "avg_txn_value_usd": 6225.14
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?`

### URL Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | A token from the [table](#exchange-flows) that we support                                                    |
| direction    | _string_  | `inflow`                                                                                  |
| exchange     | _string_  | An exchange from the [table](#exchange-flows) that we support                                                |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                                 | Type      | Description                                                                                                                                       |
| ------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value                         | _decimal_ | The average amount of a given token transferred per transaction into the given exchange on this date.                                             |
| avg_txn_value_usd                     | _decimal_ | The USD value of the average amount of tokens transferred per transaction into the exchange on this date.                                         |
| date                                  | _string_  | The date in _YYYY-MM-DD_                                                                                                                          |
| datetime *                            | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone).                                                                       |
| hour *                                | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone).                                                                                                |
| inflow                                | _decimal_ | The total amount of tokens that flowed into the exchange on this date. Denominated by the given token.                                            |
| inflow_usd                            | _decimal_ | The USD value of the total amount of tokens that flowed into the exchange on this date                                                            |
| number_of_txns                        | _integer_ | The number of transactions sending tokens into a given exchange on this date.                                                                     |

Note: All fields with a \* are optional and appears when window is `1h`. 


## Full Historical Outflows

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the outflow of a given token from exchange wallets for as far back as we track. The average outflow is the average transaction value for transactions flowing out of exchange wallets on a given day.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?`

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=btc&exchange=binance&direction=outflow&window=1h&format=json&limit=2&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-10-04",
    "hour": "11:00:00", // not available when window 1d
    "datetime": "2019-10-04 11:00:00", // not available when window 1d
    "outflow": 215.79754153,
    "outflow_usd": 1760696.88,
    "number_of_txns": 7,
    "avg_txn_value": 30.82822022,
    "avg_txn_value_usd": 251528.13
  },
  {
    "date": "2019-10-04",
    "hour": "12:00:00", // not available when window 1d
    "datetime": "2019-10-04 12:00:00", // not available when window 1d
    "outflow": 143.59191158,
    "outflow_usd": 1172183.26,
    "number_of_txns": 4,
    "avg_txn_value": 35.89797789,
    "avg_txn_value_usd": 293045.82
  }
]
```

### URL Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | A token from the [table](#exchange-flows) that we support                                                    |
| direction    | _string_  | `outflow`                                                                                 |
| exchange     | _string_  | An exchange from the [table](#exchange-flows) that we support                                              |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                                   | Type      | Description                                                                                                                                 |
| --------------------------------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------|
| avg_txn_value                           | _decimal_ | The average amount of a given token transferred per transaction out of the given exchange on this date.                                     |
| avg_txn_value_usd                       | _decimal_ | The USD value of the average amount of tokens transferred per transaction out of the given exchange on this date.                           |
| date                                    | _string_  | The date in _YYYY-MM-DD_                                                                                                                    |
| datetime *                              | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`       |
| hour *                                  | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                |
| number_of_txns                          | _decimal_ | The number of transactions sending tokens out of this exchange on this date.                                                                   |
| outflow                                 | _decimal_ | The total amount of tokens that flowed out of the exchange on this date. Denominated by the given token.                                    |
| outflow_usd                             | _decimal_ | The USD value of the total amount of tokens that flowed out of the exchange on this date                                                    |

## Exchange to Exchange Flows

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the full historical inter-flows from an exchange *to* another exchange of that we have labelled. 

For this endpoint, the tokens we currently support are `btc` and `eth`.

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?`

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?format=json&token=btc&window=1h&limit=2&from_date=2019-11-01&to_date=2019-11-09&from_entity=binance&to_entity=huobi&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-11-09",
    "hour": "22:00:00", // not available when window 1d
    "datetime": "2019-11-09 22:00:00", // not available when window 1d
    "value": 1.56713953,
    "value_usd": 13816.08,
    "number_of_txns": 3,
    "avg_txn_value": 0.52237984,
    "avg_txn_value_usd": 4605.36
  },
  {
    "date": "2019-11-09",
    "hour": "23:00:00", // not available when window 1d
    "datetime": "2019-11-09 23:00:00", // not available when window 1d
    "value": 3.540122,
    "value_usd": 31248.74,
    "number_of_txns": 2,
    "avg_txn_value": 1.770061,
    "avg_txn_value_usd": 15624.37
  }
]
```

### URL Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | A token from the [table](#exchange-flows) that we support                                                                             |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_entity  | _string_  | An exchange from the [table](#exchange-flows) that we support                                                |
| to_entity    | _string_  | An exchange from the [table](#exchange-flows) that we support. Cannot be the same as ```from_entity```       |                                                
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field             | Type      | Description                                                                                                                           |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value     | _decimal_ | The average amount tokens transferred per transaction out of the given exchange to another exchange on this date.                    |
| avg_txn_value_usd | _decimal_ | The USD value of the average amount of tokens transferred per transaction out of the given exchange to another exchange on this date.    |
| date              | _string_  | The date in _YYYY-MM-DD_                                                                                                              |
| datetime *        | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone).                                                           |
| hour *            | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone).                                                                                    |
| number_of_txns    | _integer_ | The number of transactions sending tokens into from an exchange to another exchange on this date.                                        |
| value             | _decimal_ | The total amount of tokens transferred from an exchange to another exchange on this date.                                             |
| value_usd         | _decimal_ | The value in USD of the total amount of tokens transferred from an exchange to another exchange on this date.                         |

Note: All fields with a \* are optional and appears when window is `1h`
