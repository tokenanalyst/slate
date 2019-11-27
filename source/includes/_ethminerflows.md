# Ethereum Miner Flows

## Miners to Exchanges Full Historical Flows

This endpoint returns the full historical flows of ETH from miners *to* exchanges that we have labelled.


For Ethereum, the currently supported Exchanges/Miners are:

| Name           | `to_entity`    | `from_entity`                                                                                                                                                                                                                                      |
|----------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Binance        | `binance`      | `2miners: pplns`,`2miners: solo`,`altpool.pro`,`btc.com pool`,`beeppool`,`coinotron 3`, `cruxpool`,`dwarfpool 1`,`eth.solopool.org`,`ethermine`,`ethpool 2`,`f2pool 2`,`minerall pool`,`miningpoolhub`,`nanopool`,`uleypool`,`w pool`,`zhizhu.top` |                                                                                     
| Bitfinex       | `bitfinex`     | `2miners: pplns`, `coinotron 3`, `dwarfpool 1`, `ethermine`, `f2pool 2`, `miningpoolhub`, `nanopool`, `spark pool`, `w pool`                                                                                                                       |                                                                                     
| Bittrex        | `bittrex`      | `2miners: pplns`,`2miners: solo`, `btc.com pool`, `baikalmine 1`, `beeppool`, `coinotron 3`, `dwarfpool 1`,`eth.solopool.org`, `ethermine`,`f2pool 2`,`minerall pool`,`miningpoolhub`,`nanopool`, `w pool`, `zhizhu.top`                           |                                                                                       
| Kraken         | `kraken`       | `2miners: pplns`, `btc.com pool`, `coinotron 3`, `cruxpool`, `dwarfpool 1`, `ethermine`, `ethpool 2`, `f2pool 2`,`minerall pool`,`miningpoolhub`,`nanopool`, `w pool`                                                                              |                                                                                       
| Kucoin         | `kucoin`       | `2miners: pplns`, `dwarfpool 1`, `ethermine`, `f2pool 2`, `miningpoolhub`, `nanopool`, `w pool`                                                                                                                                                    |                                                                                  
| Poloniex       | `poloniex`     | `coinotron 3`, `dwarfpool 1`, `ethermine`, `minerall pool`, `nanopool`                                                                                                                                                                             |        

The above table defines supported pairs of the query parameters `to_entity` and `from_entity`. 

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>


```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?ormat=json&to_entity=binance&from_entity=2miners:%20pplns&token=eth&window=1h&limit=2&key=APIKEY"
```

> The above command returns JSON structured like this:

```json
[
    {
        "date": "2019-11-27",
        "hour": "08:00:00", // not available when window 1d
        "datetime": "2019-11-17 08:00:00", // not available when window 1d
        "value": 0.05637151,
        "value_usd": 8.26,
        "number_of_txns": 1,
        "avg_txn_value": 0.05637151,
        "avg_txn_value_usd": 8.26
    },
    {
        "date": "2019-11-27",
        "hour": "09:00:00", // not available when window 1d
        "datetime": "2019-11-17 09:00:00", // not available when window 1d
        "value": 0.10035594,
        "value_usd": 14.35,
        "number_of_txns": 2,
        "avg_txn_value": 0.05017797,
        "avg_txn_value_usd": 7.18
    }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `eth`                                                                                     |                                       |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_entity  | _string_  | A miner from the table that we support
| to_entity    | _string_  | An exchange from the table that we support
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                                   | Type      | Description                                                                                                                                                                                                               |
| --------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| avg_txn_value                           | _decimal_ | The average amount of ETH transferred per transaction into the given exchange on this date.                                                                                                                                  |
| avg_txn_value_usd                       | _decimal_ | The USD value of the average amount of ETH transferred per transaction into the given exchange on this date.                                                                                                          |
| date                                    | _string_  | The date in _YYYY-MM-DD_                                                                                                                                                                                                  |
| datetime *                              | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`                                                                               |
| hour *                                  | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                                                                                        |
| number_of_txns                          | _integer_ | The number of transactions sending ETH into an exchange on this date/hour
| value                                   | _decimal_ | The total value of transactions sending ETH into an exchange
| value_usd                               | _decimal_ | The USD value of transactions sending ETH into an exchange
