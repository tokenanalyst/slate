# Entity to Entity Flows

For Bitcoin, the currently supported Miners/Exchanges are:

| Name           | `from_entity`    | `to_entity`                                                                           |
|----------------|------------------|---------------------------------------------------------------------------------------|
| AntPool        | `antpool`        | `bitstamp`, `bittrex`                                                                 |
| BTC.TOP        | `btc.top`        | `binance`, `bitfinex`, `bitmex`, `bitstamp`, `bittrex`, `huobi`, `kraken`, `poloniex` |    
| BitClubNetwork | `bitclubnetwork` | `bitfinex`, `bitstamp`                                                                |
| F2Pool         | `f2pool`         | `binance`, `bitfinex`, `bitstamp`, `bittrex`, `huobi`, `kraken`, `poloniex`           |
| SlushPool      | `slushpool`      | `binance`, `bitfinex`, `bitmex`, `bitstamp`, `bittrex`, `huobi`, `kraken`, `poloniex` |
| viaBTC         | `viabtc`         | `bitmex`, `bitstamp`, `bittrex`, `huobi`, `poloniex`                                  |

The above table defines supported pairs of the query parameters `from_entity` and `to_entity`. 

## Entity to Entity Full Historical Flows

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the full historical on-chain entity-to-entity flows.

```shell
curl "https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?window=1h&limit=2&from_entity=antpool&to_entity=bittrex&format=json&token=btc&key=APIKEY"
```

> The above command returns JSON structured like this:

```json
[
    {
        "date": "2019-10-07",
        "hour": "13:00:00", // not available when window 1d
        "datetime": "2019-10-07 13:00:00", // not available when window 1d
        "value": 0,
        "value_usd": 0,
        "number_of_txns": 0,
        "avg_txn_value": 0,
        "avg_txn_value_usd": 0
    },
    {
        "date": "2019-10-07",
        "hour": "14:00:00", // not available when window 1d
        "datetime": "2019-10-07 14:00:00", // not available when window 1d
        "value": 0,
        "value_usd": 0,
        "number_of_txns": 0,
        "avg_txn_value": 0,
        "avg_txn_value_usd": 0
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
| token        | _string_  | `btc`                                                                                     |                                       |
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
| avg_txn_value                           | _decimal_ | The average amount BTC transferred per transaction into the given exchange on this date.                                                                                                                                  |
| avg_txn_value_usd                       | _decimal_ | The USD value of the average amount of BTC transferred per transaction into the given exchange on this date.                                                                                                          |
| date                                    | _string_  | The date in _YYYY-MM-DD_                                                                                                                                                                                                  |
| datetime *                              | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field and appears when window is `1h`                                                                               |
| hour *                                  | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field and appears when window is `1h`                                                                                                        |
| number_of_txns                          | _integer_ | The number of transactions of sending BTC into an exchange on this date/hour
| value                                   | _decimal_ | The total value of transactions of sending BTC into an exchange
| value_usd                               | _decimal_ | The USD value of transactions of sending the BTC into an exchange
