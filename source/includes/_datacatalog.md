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
        "name": "entity_to_entity_flow_window_historical",
        "description": "On-chain flows between entities",
        "tier": 2
    },
    {
        "name": "token_supply_window_historical",
        "description": "Token supply over time",
        "tier": 1
    },
    {
        "name": "token_price_usd_window_historical",
        "description": "Historical token prices in USD",
        "tier": 1
    },
    ...
]
```

### Data Overview

All of the following dataset queries will have the same metadata at the top of the JSON structure.

| Field | Type     | Description                                                                     |
| ----- | -------- | ------------------------------------------------------------------------------- |
| name  | _string_ | The name of the dataset type that can be used in subsequent Data Catalog calls. |
| description  | _string_ | A description of the dataset type. |
| tier  | _string_ | Numerical representation of the type of subscription required to access this set where 0 = Free, 2 = Pro, 3 = Enterprise. |


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
    "description": "",
    "tier": 2,
    "jobs": [
        {
            "name": "btc_exchange_outflow_1h",
            "schema": {
                "date": {
                    "type": "date",
                    "format": "{date_format}"
                },
                "hour": {
                    "type": "hour",
                    "format": "{hour_format}"
                },
                "outflow": {
                    "type": "float",
                    "precision": "{satoshi_precision}"
                },
                "datetime": {
                    "type": "datetime",
                    "format": "{datetime_format}"
                },
                "outflow_usd": {
                    "type": "float",
                    "precision": "{usd_precision}"
                },
                "avg_txn_value": {
                    "type": "float",
                    "precision": "{satoshi_precision}"
                },
                "number_of_txns": {
                    "type": "int"
                },
                "avg_txn_value_usd": {
                    "type": "float",
                    "precision": "{usd_precision}"
                }
            },
            "endpoints": [
                {
                    "url_parameters": "token=btc&window=1h&exchange=binance&direction=outflow",
                    "name": "btc_binance_outflow_1h_historical",
                    "parameters": {
                        "token": "btc",
                        "window": "1h",
                        "exchange": "binance",
                        "direction": "outflow"
                    }
                },
                {
                    "url_parameters": "token=btc&window=1h&exchange=kraken&direction=outflow",
                    "name": "btc_kraken_outflow_1h_historical",
                    "parameters": {
                        "token": "btc",
                        "window": "1h",
                        "exchange": "kraken",
                        "direction": "outflow"
                    }
                },
                ...
            ]
        },
        {
            "name": "erc20_exchange_split_outflow_historical",
            "schema": {
                "date": {
                    "type": "date",
                    "format": "{date_format}"
                },
                "hour": {
                    "type": "hour",
                    "format": "{hour_format}"
                },
                "outflow": {
                    "type": "float",
                    "precision": "{default_precision}"
                },
                "datetime": {
                    "type": "datetime",
                    "format": "{datetime_format}"
                },
                "outflow_usd": {
                    "type": "float",
                    "precision": "{usd_precision}"
                },
                "avg_txn_value": {
                    "type": "float",
                    "precision": "{default_precision}"
                },
                "number_of_txns": {
                    "type": "int"
                },
                "avg_txn_value_usd": {
                    "type": "float",
                    "precision": "{usd_precision}"
                }
            },
            "endpoints": [
                {
                    "url_parameters": "token=usdt_erc20&window=1h&exchange=binance&direction=outflow",
                    "name": "usdt_erc20_binance_outflow_1h_historical",
                    "parameters": {
                        "token": "usdt_erc20",
                        "window": "1h",
                        "exchange": "binance",
                        "direction": "outflow"
                    }
                },
                {
                    "url_parameters": "token=usdt_erc20&window=1h&exchange=bitfinex&direction=outflow",
                    "name": "usdt_erc20_bitfinex_outflow_1h_historical",
                    "parameters": {
                        "token": "usdt_erc20",
                        "window": "1h",
                        "exchange": "bitfinex",
                        "direction": "outflow"
                    }
                },
                ...
            ]
        },
        ...
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
| name             | _string_ | The name of the dataset             |
| schema              | _object_ | The sschema for the dataset                                    |
| endpoints                  | _string_ | The list of possible parameters combination for the dataset                                     |
| endpoints.name                  | _string_ | The name of the parameter combination                                       |
| endpoints.parameters                  | _object_ | Parameters                                       |
| endpoints.url_parameters                  | _string_ | Parameters in url query parameters format                                       |

You can also filter the endpoints by parameters. i.e. if you want to filter where the exchange is "binance", you can call:

```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical?exchange=binance"
```

The can also be combined:
```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical?exchange=binance&token=btc"
```

```shell
curl "https://api.tokenanalyst.io/catalog/data/entity_to_entity_flow_window_historical?token=eth&to_entity=binance&window=1h"
```

## Supported Values

The following list of API calls allow you to query all the possible values for a given parameter, optionally filtering by a second parameter. This would allow you to for example query all the tokens supported by a given dataset type, or the tokens supported for a given exchange. 

## Possible values

Return an array of supported values for a given parameter.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/{parameter}`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/exchange_flow_window_historical/token"
```

> The above command returns an array like the below:

```json
[
    "rep",
    "rlc",
    "link",
    "dai",
    "usdc",
    "mana",
    "omg",
    "gnt",
    "btc",
    "bat",
    "usdt_omni",
    "pax",
    "cvc",
    "mkr",
    "knc",
    "usdt_erc20",
    "tusd",
    "loom",
    "nmr",
    "snt",
    "eth",
    "zrx"
]
```

### URL Segments

| Parameter | Type     | Description                       |
| --------- | -------- | --------------------------------- |
| name      | _string_ | The dataset type name (see above) |
| parameter | _string_ | The parameter to get possible values of |

## Possible values, filtered

Return an array of supported values for a given parameter, filtering by another parameter.

### HTTP Request

`GET https://api.tokenanalyst.io/catalog/data/{name}/{filter_parameter}/{filter_value}/{parameter}`

<img src="https://img.shields.io/badge/Tier-Free-green.svg"/>


```shell
curl "https://api.tokenanalyst.io/catalog/data/entity_to_entity_flow_window_historical/window/1h/to_entity"
```

> The above command returns an array like the below:

```json
[
    "binance",
    "bitfinex",
    "bitmex",
    "bitstamp",
    "bittrex",
    "deribit",
    "huobi",
    "kraken",
    "kucoin",
    "okex",
    "poloniex"
]
```

### URL Segments

| Parameter | Type     | Description                       |
| --------- | -------- | --------------------------------- |
| name      | _string_ | The dataset type name (see above) |
| filter_parameter | _string_ | The parameter to use as a filter |
| filter_value | _string_ | The value to filter with |
| parameter | _string_ | The parameter to get possible values of |

