# Prices (USD)
The US Dollar (_USD_) price of each asset we support is available through this endpoint. The hourly price is the hourly closing price for each asset. The daily price is the mean of the hourly closing prices for each asset.

## Supported Assets

The list of assets we currently support is:

| Name                      | API Parameter |
|---------------------------|---------------|
| Basic Attention Token     | _bat_         |
| Bitcoin Cash              | _bch_         |
| Binance Coin              | _bnb_         |
| Bancor                    | _bnt_         |
| Bitcoin                   | _btc_         |
| Bitcoin BEP2 (Binance Chain)   | _btcb_        |
| Bezant                    | _bznt_        |
| Civic                     | _cvc_         |
| Dai                       | _dai_         |
| Ethereum Classic          | _etc_         |
| Ethereum                  | _eth_         |
| Fetch                     | _fet_         |
| Fantom                    | _ftm_         |
| Golem                     | _gnt_         |
| Gemini Dollar             | _gusd_        |
| ICON                      | _icx_         |
| Kyber Network             | _knc_         |
| Chainlink                 | _link_        |
| Loom Network              | _loom_        |
| Litecoin                  | _ltc_         |
| Decentraland              | _mana_        |
| Matic Network             | _matic_       |
| Mithril                   | _mith_        |
| Maker                     | _mkr_         |
| Numeraire                 | _nmr_         |
| OmiseGO                   | _omg_         |
| 1Coin                     | _one_         |
| Paxos Standard Token      | _pax_         |
| Augur                     | _rep_         |
| iExec                     | _rlc_         |
| Status                    | _snt_         |
| Storj                     | _storj_       |
| Monolith                  | _tkn_         |
| TrueUSD                   | _tusd_        |
| USD Coin                  | _usdc_        |
| StableUSD (Binance chain) | _usdsb_       |
| Tether                    | _usdt_erc20_  |
| Monero                    | _xmr_         |
| Ripple                    | _xrp_         |
| Zcash                     | _zec_         |
| 0x                        | _zrx_         |


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
| token     | _string_ | `btc`                                               |
| window    | _string_ | `1h` or `1d`                                        |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |


### Data Overview

| Field         | Type     | Description                                          |
| ------------- | -------- | ---------------------------------------------------- |
| date         | _string_ | The date in _YYYY-MM-DD_                                                  |
| datetime *   | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h`                                                                               |
| hour *       | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field field and appears when window is `1h`                                                                                                        |
| price_usd    | _decimal_ | The daily price of the token in USD (the hourly or daily mean of minute-level price data) |
