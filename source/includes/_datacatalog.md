# Data Catalog

The TokenAnalyst Data Catalog is a RESTful service that allows you to find the API endpoints of all 1000+ datasets that we offer, along with all possible values for each particular dataset.

## Dataset Types

Return a list of all the current Dataset types that can be used for further Data Catalog queries.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data"
```

> The above command returns JSON structured like this:

```json
[
    {
        "name": "exchange_flow_window_historical"
    },
    {
        "name": "exchange_flow_window_static"
    },
    {
        "name": "token_nvt_window_historical"
    },
]
```

### Data Overview

| Field | Type     | Description                                                                     |
| ----- | -------- | ------------------------------------------------------------------------------- |
| name  | _string_ | The name of the dataset type that can be used in subsequent Data Catalog calls. |

## Dataset Results

All of the following dataset queries will have the below metadata at the top of the JSON structure:

### Dataset base metadata

| Field            | Type     | Description                                                                                                               |
| ---------------- | -------- | ------------------------------------------------------------------------------------------------------------------------- |
| name             | _string_ | The name of the dataset type.                                                                                             |
| description.text | _string_ | A description of the dataset type.                                                                                        |
| tier.value       | _number_ | Numerical representation of the type of subscription required to access this set where 0 = Free, 2 = Pro, 3 = Enterprise. |
| schema.json      | _string_ | JSON schema representation of the return values and types.                                                                |

## By Name

Return a list of all the datasets of a given dataset type.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical"
```

> The above command returns JSON structured like this:

```json
{
        "name": "exchange_flow_window_historical",
        "description": {
            "text": "Description for dataset exchange_flow_window_historical"
        },
        "tier": {
            "value": 3
        },
        "schema": {
            "json": "{\"avg_txn_value\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"avg_txn_value_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"date\":{\"format\":\"{date_format}\",\"type\":\"date\"},\"datetime\":{\"format\":\"{datetime_format}\",\"type\":\"datetime\"},\"hour\":{\"format\":\"{hour_format}\",\"type\":\"hour\"},\"inflow\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"inflow_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"number_of_txns\":{\"type\":\"int\"}}"
        },
        "exchange_flow_window_historical": [
            {
                "direction": "inflow",
                "exchange": "bittrex",
                "token": "btc",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=btc&direction=inflow&window=1h&exchange=bittrex",
                    "is_api_active": true
                }
            },
            {
                "direction": "inflow",
                "exchange": "poloniex",
                "token": "bat",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?direction=inflow&window=1h&token=bat&exchange=poloniex",
                    "is_api_active": true
                }
            },
        ]
}
```

### URL Segments

| Parameter | Type     | Description                       |
| --------- | -------- | --------------------------------- |
| name      | _string_ | The dataset type name (see above) |

### Dataset Values

| Field                  | Type     | Description                                          |
| ---------------------- | -------- | ---------------------------------------------------- |
| direction*             | _string_ | The flow direction to / from an exchange             |
| exchange*              | _string_ | The exchange name                                    |
| token                  | _string_ | The token code                                       |
| window                 | _string_ | The time window for each datapoint                   |
| from_entity*           | _string_ | The origin entity of a transaction                   |
| to_entity*             | _string_ | The destination entity of a transaction              |
| location.api           | _string_ | The full API URL to access this dataset              |
| location.is_api_active | _bool_   | Signify whether this API URL is currently accessible |

(*) Availability dependant on dataset type

## By Token

Return a list of all the datasets of a given dataset type, filtered by token.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/token/{token}`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical/token/btc"
```

> The above command returns JSON structured like this:

```json
{
        "name": "exchange_flow_window_historical",
        "description": {
            "text": "Description for dataset exchange_flow_window_historical"
        },
        "tier": {
            "value": 3
        },
        "schema": {
            "json": "{\"avg_txn_value\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"avg_txn_value_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"date\":{\"format\":\"{date_format}\",\"type\":\"date\"},\"datetime\":{\"format\":\"{datetime_format}\",\"type\":\"datetime\"},\"hour\":{\"format\":\"{hour_format}\",\"type\":\"hour\"},\"inflow\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"inflow_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"number_of_txns\":{\"type\":\"int\"}}"
        },
        "exchange_flow_window_historical": [
           {
                "direction": "inflow",
                "exchange": "bittrex",
                "token": "btc",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=btc&direction=inflow&window=1h&exchange=bittrex",
                    "is_api_active": true
                }
            },
            {
                "direction": "outflow",
                "exchange": "bittrex",
                "token": "btc",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=btc&exchange=bittrex&direction=outflow&window=1h",
                    "is_api_active": true
                }
            },
        ]
}
```

### URL Segments

| Parameter | Type     | Description                           |
| --------- | -------- | ------------------------------------- |
| name      | _string_ | The dataset type name (see above)     |
| token     | _string_ | The token code to filter by, i.e. btc |

### Dataset Values

| Field                  | Type     | Description                                          |
| ---------------------- | -------- | ---------------------------------------------------- |
| direction*             | _string_ | The flow direction to / from an exchange             |
| exchange*              | _string_ | The exchange name                                    |
| token                  | _string_ | The token code                                       |
| window                 | _string_ | The time window for each datapoint                   |
| from_entity*           | _string_ | The origin entity of a transaction                   |
| to_entity*             | _string_ | The destination entity of a transaction              |
| location.api           | _string_ | The full API URL to access this dataset              |
| location.is_api_active | _bool_   | Signify whether this API URL is currently accessible |

(*) Availability dependant on dataset type

## By Exchange

Return a list of all the datasets of a given dataset type, filtered by exchange name. Please note this can only be specified for exchange related dataset types.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/exchange/{exchange}`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical/exchange/huobi"
```

> The above command returns JSON structured like this:

```json
{
        "name": "exchange_flow_window_historical",
        "description": {
            "text": "Description for dataset exchange_flow_window_historical"
        },
        "tier": {
            "value": 3
        },
        "schema": {
            "json": "{\"avg_txn_value\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"avg_txn_value_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"date\":{\"format\":\"{date_format}\",\"type\":\"date\"},\"datetime\":{\"format\":\"{datetime_format}\",\"type\":\"datetime\"},\"hour\":{\"format\":\"{hour_format}\",\"type\":\"hour\"},\"inflow\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"inflow_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"number_of_txns\":{\"type\":\"int\"}}"
        },
        "exchange_flow_window_historical": [
           {
                "direction": "outflow",
                "exchange": "huobi",
                "token": "btc",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=btc&direction=outflow&window=1h&exchange=huobi",
                    "is_api_active": true
                }
            },
            {
                "direction": "outflow",
                "exchange": "huobi",
                "token": "bat",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?direction=outflow&window=1h&token=bat&exchange=huobi",
                    "is_api_active": true
                }
            },
        ]
}
```

### URL Segments

| Parameter | Type     | Description                            |
| --------- | -------- | -------------------------------------- |
| name      | _string_ | The dataset type name (see above)      |
| exchange  | _string_ | The name of the exchange, i.e. binance |

### Dataset Values

| Field                  | Type     | Description                                          |
| ---------------------- | -------- | ---------------------------------------------------- |
| direction*             | _string_ | The flow direction to / from an exchange             |
| exchange*              | _string_ | The exchange name                                    |
| token                  | _string_ | The token code                                       |
| window                 | _string_ | The time window for each datapoint                   |
| from_entity*           | _string_ | The origin entity of a transaction                   |
| to_entity*             | _string_ | The destination entity of a transaction              |
| location.api           | _string_ | The full API URL to access this dataset              |
| location.is_api_active | _bool_   | Signify whether this API URL is currently accessible |

(*) Availability dependant on dataset type

## By Exchange and Token

Return a list of all the datasets of a given dataset type, filtered by exchange name. Please note this can only be specified for exchange related dataset types.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/exchange/{exchange}/token/{token}`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical/exchange/binance/token/btc"
```

> The above command returns JSON structured like this:

```json
{
        "name": "exchange_flow_window_historical",
        "description": {
            "text": "Description for dataset exchange_flow_window_historical"
        },
        "tier": {
            "value": 3
        },
        "schema": {
            "json": "{\"avg_txn_value\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"avg_txn_value_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"date\":{\"format\":\"{date_format}\",\"type\":\"date\"},\"datetime\":{\"format\":\"{datetime_format}\",\"type\":\"datetime\"},\"hour\":{\"format\":\"{hour_format}\",\"type\":\"hour\"},\"inflow\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"inflow_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"number_of_txns\":{\"type\":\"int\"}}"
        },
        "exchange_flow_window_historical": [
            {
                "direction": "outflow",
                "exchange": "binance",
                "token": "btc",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=btc&direction=outflow&window=1h&exchange=binance",
                    "is_api_active": true
                }
            },
            {
                "direction": "inflow",
                "exchange": "binance",
                "token": "btc",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=btc&exchange=binance&direction=inflow&window=1h",
                    "is_api_active": true
                }
            },
        ]
}
```

### URL Segments

| Parameter | Type     | Description                            |
| --------- | -------- | -------------------------------------- |
| name      | _string_ | The dataset type name (see above)      |
| exchange  | _string_ | The name of the exchange, i.e. binance |
| token     | _string_ | The token code to filter by, i.e. btc  |

### Dataset Values

| Field                  | Type     | Description                                          |
| ---------------------- | -------- | ---------------------------------------------------- |
| direction*             | _string_ | The flow direction to / from an exchange             |
| exchange*              | _string_ | The exchange name                                    |
| token                  | _string_ | The token code                                       |
| window                 | _string_ | The time window for each datapoint                   |
| from_entity*           | _string_ | The origin entity of a transaction                   |
| to_entity*             | _string_ | The destination entity of a transaction              |
| location.api           | _string_ | The full API URL to access this dataset              |
| location.is_api_active | _bool_   | Signify whether this API URL is currently accessible |

(*) Availability dependant on dataset type

## By Window

Return a list of all the datasets of a given dataset type, filtered by time windows.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/window/{window}`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical/window/1h"
```

> The above command returns JSON structured like this:

```json
{
        "name": "exchange_flow_window_historical",
        "description": {
            "text": "Description for dataset exchange_flow_window_historical"
        },
        "tier": {
            "value": 3
        },
        "schema": {
            "json": "{\"avg_txn_value\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"avg_txn_value_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"date\":{\"format\":\"{date_format}\",\"type\":\"date\"},\"datetime\":{\"format\":\"{datetime_format}\",\"type\":\"datetime\"},\"hour\":{\"format\":\"{hour_format}\",\"type\":\"hour\"},\"inflow\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"inflow_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"number_of_txns\":{\"type\":\"int\"}}"
        },
        "exchange_flow_window_historical": [
            {
                "direction": "inflow",
                "exchange": "bittrex",
                "token": "btc",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=btc&direction=inflow&window=1h&exchange=bittrex",
                    "is_api_active": true
                }
            },
            {
                "direction": "inflow",
                "exchange": "poloniex",
                "token": "bat",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?direction=inflow&window=1h&token=bat&exchange=poloniex",
                    "is_api_active": true
                }
            },
        ]
}
```

### URL Segments

| Parameter | Type     | Description                       |
| --------- | -------- | --------------------------------- |
| name      | _string_ | The dataset type name (see above) |
| window    | _string_ | The data window, i.e. 1h          |

### Dataset Values

| Field                  | Type     | Description                                          |
| ---------------------- | -------- | ---------------------------------------------------- |
| direction*             | _string_ | The flow direction to / from an exchange             |
| exchange*              | _string_ | The exchange name                                    |
| token                  | _string_ | The token code                                       |
| window                 | _string_ | The time window for each datapoint                   |
| from_entity*           | _string_ | The origin entity of a transaction                   |
| to_entity*             | _string_ | The destination entity of a transaction              |
| location.api           | _string_ | The full API URL to access this dataset              |
| location.is_api_active | _bool_   | Signify whether this API URL is currently accessible |

(*) Availability dependant on dataset type

## By Direction

Return a list of all the datasets of a given dataset type, filtered by flow direction. Please note this is only valid for certain datasets.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/direction/{direction}`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical/direction/inflow"
```

> The above command returns JSON structured like this:

```json
{
        "name": "exchange_flow_window_historical",
        "description": {
            "text": "Description for dataset exchange_flow_window_historical"
        },
        "tier": {
            "value": 3
        },
        "schema": {
            "json": "{\"avg_txn_value\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"avg_txn_value_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"date\":{\"format\":\"{date_format}\",\"type\":\"date\"},\"datetime\":{\"format\":\"{datetime_format}\",\"type\":\"datetime\"},\"hour\":{\"format\":\"{hour_format}\",\"type\":\"hour\"},\"inflow\":{\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"inflow_usd\":{\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"number_of_txns\":{\"type\":\"int\"}}"
        },
        "exchange_flow_window_historical": [
            {
                "direction": "inflow",
                "exchange": "bittrex",
                "token": "btc",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=btc&direction=inflow&window=1h&exchange=bittrex",
                    "is_api_active": true
                }
            },
            {
                "direction": "inflow",
                "exchange": "poloniex",
                "token": "bat",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?direction=inflow&window=1h&token=bat&exchange=poloniex",
                    "is_api_active": true
                }
            },
        ]
}
```

### URL Segments

| Parameter | Type     | Description                       |
| --------- | -------- | --------------------------------- |
| name      | _string_ | The dataset type name (see above) |
| direction | _string_ | The flow direction, i.e. inflow   |

### Dataset Values

| Field                  | Type     | Description                                          |
| ---------------------- | -------- | ---------------------------------------------------- |
| direction*             | _string_ | The flow direction to / from an exchange             |
| exchange*              | _string_ | The exchange name                                    |
| token                  | _string_ | The token code                                       |
| window                 | _string_ | The time window for each datapoint                   |
| from_entity*           | _string_ | The origin entity of a transaction                   |
| to_entity*             | _string_ | The destination entity of a transaction              |
| location.api           | _string_ | The full API URL to access this dataset              |
| location.is_api_active | _bool_   | Signify whether this API URL is currently accessible |

(*) Availability dependant on dataset type

## By Origin Entity

Return a list of all the datasets of a given dataset type, filtered by to origin entity of the transactions. Please note that this is only valid for certain datasets.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/from_entity/{from_entity}`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/entity_to_entity_flow_window_historical/from_entity/ethermine"
```

> The above command returns JSON structured like this:

```json
{
        "name": "entity_to_entity_flow_window_historical",
        "description": {
            "text": "Description for dataset entity_to_entity_flow_window_historical"
        },
        "tier": {
            "value": 3
        },
        "schema": {
            "json": "{\"avg_txn_value\":{\"agg_string\":\"value / number_of_txns\",\"aggregate_type\":\"custom\",\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"avg_txn_value_usd\":{\"agg_string\":\"value_usd / number_of_txns\",\"aggregate_type\":\"custom\",\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"date\":{\"format\":\"{date_format}\",\"type\":\"date\"},\"datetime\":{\"format\":\"{datetime_format}\",\"type\":\"datetime\"},\"hour\":{\"format\":\"{hour_format}\",\"type\":\"hour\"},\"number_of_txns\":{\"aggregate_type\":\"sum\",\"type\":\"int\"},\"value\":{\"aggregate_type\":\"sum\",\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"value_usd\":{\"aggregate_type\":\"sum\",\"precision\":\"{usd_precision}\",\"type\":\"float\"}}"
        },
        "entity_to_entity_flow_window_historical": [
            {
                "from_entity": "ethermine",
                "to_entity": "poloniex",
                "token": "eth",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?token=eth&window=1h&from_entity=ethermine&to_entity=poloniex",
                    "is_api_active": true
                }
            },
            {
                "from_entity": "ethermine",
                "to_entity": "kucoin",
                "token": "eth",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?token=eth&window=1h&from_entity=ethermine&to_entity=kucoin",
                    "is_api_active": true
                }
            },
        ]
}
```

### URL Segments

| Parameter   | Type     | Description                                 |
| ----------- | -------- | ------------------------------------------- |
| name        | _string_ | The dataset type name (see above)           |
| from_entity | _string_ | The name of the origin entity, i.e. binance |

### Dataset Values

| Field                  | Type     | Description                                          |
| ---------------------- | -------- | ---------------------------------------------------- |
| direction*             | _string_ | The flow direction to / from an exchange             |
| exchange*              | _string_ | The exchange name                                    |
| token                  | _string_ | The token code                                       |
| window                 | _string_ | The time window for each datapoint                   |
| from_entity*           | _string_ | The origin entity of a transaction                   |
| to_entity*             | _string_ | The destination entity of a transaction              |
| location.api           | _string_ | The full API URL to access this dataset              |
| location.is_api_active | _bool_   | Signify whether this API URL is currently accessible |

(*) Availability dependant on dataset type

## By Destination Entity

Return a list of all the datasets of a given dataset type, filtered by to destination entity of the transactions. Please note that this is only valid for certain datasets.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/to_entity/{to_entity}`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/entity_to_entity_flow_window_historical/to_entity/bittrex"
```

> The above command returns JSON structured like this:

```json
{
        "name": "entity_to_entity_flow_window_historical",
        "description": {
            "text": "Description for dataset entity_to_entity_flow_window_historical"
        },
        "tier": {
            "value": 3
        },
        "schema": {
            "json": "{\"avg_txn_value\":{\"agg_string\":\"value / number_of_txns\",\"aggregate_type\":\"custom\",\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"avg_txn_value_usd\":{\"agg_string\":\"value_usd / number_of_txns\",\"aggregate_type\":\"custom\",\"precision\":\"{usd_precision}\",\"type\":\"float\"},\"date\":{\"format\":\"{date_format}\",\"type\":\"date\"},\"datetime\":{\"format\":\"{datetime_format}\",\"type\":\"datetime\"},\"hour\":{\"format\":\"{hour_format}\",\"type\":\"hour\"},\"number_of_txns\":{\"aggregate_type\":\"sum\",\"type\":\"int\"},\"value\":{\"aggregate_type\":\"sum\",\"precision\":\"{satoshi_precision}\",\"type\":\"float\"},\"value_usd\":{\"aggregate_type\":\"sum\",\"precision\":\"{usd_precision}\",\"type\":\"float\"}}"
        },
        "entity_to_entity_flow_window_historical": [
            {
                "from_entity": "2miners: pplns,2miners: solo",
                "to_entity": "bittrex",
                "token": "eth",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?token=eth&window=1h&from_entity=2miners: pplns,2miners: solo&to_entity=bittrex",
                    "is_api_active": true
                }
            },
            {
                "from_entity": "beeppool",
                "to_entity": "bittrex",
                "token": "eth",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/entity_to_entity_flow_window_historical/last?token=eth&window=1h&from_entity=beeppool&to_entity=bittrex",
                    "is_api_active": true
                }
            },
        ]
}
```

### URL Segments

| Parameter | Type     | Description                                      |
| --------- | -------- | ------------------------------------------------ |
| name      | _string_ | The dataset type name (see above)                |
| to_entity | _string_ | The name of the destination entity, i.e. binance |

### Dataset Values

| Field                  | Type     | Description                                          |
| ---------------------- | -------- | ---------------------------------------------------- |
| direction*             | _string_ | The flow direction to / from an exchange             |
| exchange*              | _string_ | The exchange name                                    |
| token                  | _string_ | The token code                                       |
| window                 | _string_ | The time window for each datapoint                   |
| from_entity*           | _string_ | The origin entity of a transaction                   |
| to_entity*             | _string_ | The destination entity of a transaction              |
| location.api           | _string_ | The full API URL to access this dataset              |
| location.is_api_active | _bool_   | Signify whether this API URL is currently accessible |

(*) Availability dependant on dataset type

## Supported Values

The following list of API calls provide arrays of valid values for certain dataset types. For example the list of supported exchanges for a given token, or the supported data windows for a given dataset.

## Tokens

Return an array of tokens supported for this dataset.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/tokens`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical/tokens"
```

> The above command returns an array like the below:

```json
[
    "btc",
    "bat",
    "eth",
    "usdt_omni",
    "usdt_erc20",
    "pax",
    "usdc",
    "zrx",
    "loom",
    "tusd",
    "link",
    "mana",
    "omg",
    "gnt",
    "cvc",
    "knc",
    "rep",
    "dai",
    "mkr",
    "nmr",
    "rlc",
    "snt"
]
```

### URL Segments

| Parameter | Type     | Description                       |
| --------- | -------- | --------------------------------- |
| name      | _string_ | The dataset type name (see above) |

## Exchanges

Return an array of exchanges supported for this dataset and token. Please note this only applies to datasets that involve exchanges.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/tokens/{token}/exchanges`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical/token/btc/exchanges"
```

> The above command returns an array like the below:

```json
[
    "bitstamp",
    "binance",
    "bittrex",
    "bitfinex",
    "bitmex",
    "kraken",
    "huobi",
    "poloniex",
    "kucoin",
    "okex",
    "deribit"
]
```

### URL Segments

| Parameter | Type     | Description                       |
| --------- | -------- | --------------------------------- |
| name      | _string_ | The dataset type name (see above) |
| token     | _string_ | The token code                    |

## Windows

Return an array of supported data windows for this dataset type

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/windows`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical/windows"
```

> The above command returns an array like the below:

```json

    [
      "1d",
      "1h"
    ]

```

### URL Segments

| Parameter | Type     | Description                       |
| --------- | -------- | --------------------------------- |
| name      | _string_ | The dataset type name (see above) |

## Directions

Return an array of supported flow directions. Only applies to datasets that involve exchanges.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/directions`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical/directions"
```

> The above command returns an array like the below:

```json

    [
      "outflow",
      "inflow"
    ]

```

### URL Segments

| Parameter | Type     | Description                       |
| --------- | -------- | --------------------------------- |
| name      | _string_ | The dataset type name (see above) |

## Origin Entities

Return an array of supported origin entities for this dataset. Only applies to datasets that involve entity to entity flows.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/from_entities`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/entity_to_entity_flow_window_historical/from_entities"
```

> The above command returns an array like the below:

```json

    [
      "2miners: pplns",
      "2miners: solo",
      "altpool.pro",
      "beeppool",
      "btc.com pool",
      "coinotron 3",
      "cruxpool",
      "dwarfpool 1",
      "eth.solopool.org",
      "ethermine"
    ]

```

### URL Segments

| Parameter | Type     | Description                       |
| --------- | -------- | --------------------------------- |
| name      | _string_ | The dataset type name (see above) |

## Destination Entities

Return an array of supported destination entities for this dataset. Only applies to datasets that involve entity to entity flows.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/to_entities`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/entity_to_entity_flow_window_historical/to_entities"
```

> The above command returns an array like the below:

```json

    [
      "binance",
      "bitfinex",
      "bittrex",
      "kraken",
      "kucoin",
      "poloniex",
    ]

```

### URL Segments

| Parameter | Type     | Description                       |
| --------- | -------- | --------------------------------- |
| name      | _string_ | The dataset type name (see above) |

