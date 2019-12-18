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

## Dataset results

All of the following dataset queries will have the below metadata at the top of the JSON structure:

### Dataset base metadata

| Field            | Type     | Description                                                                                                               |
| ---------------- | -------- | ------------------------------------------------------------------------------------------------------------------------- |
| name             | _string_ | The name of the dataset type.                                                                                             |
| description.text | _string_ | A description of the dataset type.                                                                                        |
| tier.value       | _number_ | Numerical representation of the type of subscription required to access this set where 0 = Free, 2 = Pro, 3 = Enterprise. |
| schema.json      | _string_ | JSON schema representation of the return values and types.                                                                |

## Datasets by Name

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
                    "is_api_active": null
                }
            },
            {
                "direction": "inflow",
                "exchange": "poloniex",
                "token": "bat",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?direction=inflow&window=1h&token=bat&exchange=poloniex",
                    "is_api_active": null
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

## Datasets by Name and Token

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
                    "is_api_active": null
                }
            },
            {
                "direction": "outflow",
                "exchange": "bittrex",
                "token": "btc",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?token=btc&exchange=bittrex&direction=outflow&window=1h",
                    "is_api_active": null
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

## Datasets by Name and Exchange

Return a list of all the datasets of a given dataset type, filtered by exchange name. Please note this can only be specified to exchange related dataset types.

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
                    "is_api_active": null
                }
            },
            {
                "direction": "outflow",
                "exchange": "huobi",
                "token": "bat",
                "window": "1h",
                "location": {
                    "api": "https://api.tokenanalyst.io/analytics/private/v1/exchange_flow_window_historical/last?direction=outflow&window=1h&token=bat&exchange=huobi",
                    "is_api_active": null
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