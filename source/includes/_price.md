# Prices (USD)
The US Dollar (_USD_) price of each asset we support is available through this endpoint. The hourly price is the hourly closing price for each asset. The daily price is the mean of the hourly closing prices for each asset.

## Supported Assets

The list of assets we currently support is:

| Name                      | API Parameter |
|---------------------------|---------------|
| Basic Attention Token     | `bat`         |
| Bitcoin Cash              | `bch`         |
| Binance Coin              | `bnb`         |
| Bancor                    | `bnt`         |
| Bitcoin                   | `btc`         |
| Bitcoin BEP2 (Binance Chain)   | `btcb`        |
| Bezant                    | `bznt`        |
| Civic                     | `cvc`         |
| Dai                       | `dai`         |
| Ethereum Classic          | `etc`         |
| Ethereum                  | `eth`         |
| Fetch                     | `fet`         |
| Fantom                    | `ftm`         |
| Golem                     | `gnt`         |
| Gemini Dollar             | `gusd`        |
| ICON                      | `icx`         |
| Kyber Network             | `knc`         |
| Chainlink                 | `link`        |
| Loom Network              | `loom`        |
| Litecoin                  | `ltc`         |
| Decentraland              | `mana`        |
| Matic Network             | `matic`       |
| Mithril                   | `mith`        |
| Maker                     | `mkr`         |
| Numeraire                 | `nmr`         |
| OmiseGO                   | `omg`         |
| 1Coin                     | `one`         |
| Paxos Standard Token      | `pax`         |
| Augur                     | `rep`         |
| iExec                     | `rlc`         |
| Status                    | `snt`         |
| Storj                     | `storj`       |
| Monolith                  | `tkn`         |
| TrueUSD                   | `tusd`        |
| USD Coin                  | `usdc`        |
| StableUSD (Binance chain) | `usdsb`       |
| Tether                    | `usdt_erc20`  |
| Monero                    | `xmr`         |
| Ripple                    | `xrp`         |
| Zcash                     | `zec`         |
| 0x                        | `zrx`         |


## Token Price

<img src="https://img.shields.io/badge/Tier-Hobbyist-blue.svg"/>

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/token_price_usd_window_historical/last?token=btc&window=1h&format=json&key=API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2017-12-27",
    "hour": "05:00:00", // not available when window 1d
    "datetime": "2017-12-27 05:00:00", // not available when window 1d
    "price_usd": 16416.71,
  },
  {
    "date": "2017-12-28",
    "hour": "06:00:00", // not available when window 1d
    "datetime": "2017-12-27 06:00:00", // not available when window 1d
    "price_usd": 13868.98,
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/token_price_usd_window_historical/last?`

### Query Parameters

| Parameter | Type     | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| key       | _string_ | Your unique API key                                 |
| format    | _string_ | What format you want your data in (`json` or `csv`) |
| token     | _string_ | A token from the [table](#supported-assets) that we support                                   |
| window    | _string_ | `1h` or `1d`                                        |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field         | Type     | Description                                          |
| ------------- | -------- | ---------------------------------------------------- |
| date         | _string_ | The date in _YYYY-MM-DD_                                                  |
| datetime *   | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`                                                                               |
| hour *       | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                                                                                        |
| price_usd    | _decimal_ | The daily price of the token in USD (the hourly or daily mean of minute-level price data) |
