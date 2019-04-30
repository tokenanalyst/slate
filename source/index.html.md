---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Bitcoin Exchange Flows 


For Bitcoin currently supported exchanges are: binance, bittrex, bitstamp, poloniex, bitmex, bitfinex

## 24h Inflow to Exchanges


> This is an example

```shell
$ curl https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_historical
&token=btc
&exchange=binance
&direction=inflow
&format=json
&key=API_KEY
```

> The response looks like:

```json
[
  {
    "avg_txn_value":"0.01",
    "date":"2017-06-23",
    "entity":"Binance",
    "inflow":"0.01",
    "number_of_entity_receiving_addresses":"1",
    "number_of_nonentity_sending_addresses":"1",
    "number_of_txns":"1",
    "inflow_usd":"27.34",
    "avg_txn_value_usd":"27.34"
},...]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_historical`


### URL Parameters

Parameter | Description
--------- | -----------
token | btc 
exchange | An exchange from the list 
direction | Either inflow or outflow
format | Either json or csv
key | API key


## 24h Outflows from Exchanges

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_historical`

> This is an example:

```shell
$ curl https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_historical
&token=btc
&exchange=binance
&direction=outflow
&format=json
&key=API_KEY
```

> The response looks like: 

```json
[
  {
    "avg_txn_value":"26.73",
    "date":"2017-07-05",
    "entity":"Binance",
    "number_of_entity_sending_addresses":"23",
    "number_of_nonentity_receiving_addresses":"1",
    "number_of_txns":"3",
    "outflow":"26.73",
    "outflow_usd":"69375.93",
    "avg_txn_value_usd":"69375.93"
  },...]
```

### URL Parameters

Parameter | Description
--------- | -----------
token |  btc 
exchange | An exchange from the list 
direction | Either inflow or outflow
format | Either json or csv
key | API key

## 24h Top 10 Inflow Large Value Transactions 

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_top10_historical`

```shell
$ curl https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_top10_historical
&token=btc
&exchange=binance
&direction=infow
&format=json
&key=API_KEY
```

> This is what the response looks like

```json
[
  {
    "datetime": "2019-04-29T18:04:21Z",
    "entity": "Bitfinex",
    "i": "1",
    "transactionhash": "260eec6c4f34eeea7104fe129ebb6799e503f98db4235b8ffc68cbe7c94220b9",
    "transactionid": "91b913b574c573367fc3d0d8eee2ced0671eb4bb444c61c84994d3b0b69545f2",
    "value": "3500.0",
    "value_usd": "18312422.1"
  },...
]
```

### URL Parameters

Parameter | Description
--------- | -----------
token |  btc 
exchange | An exchange from the list 
direction | Either inflow or outflow (in this case inflow)
format | Either json or csv
key | API key

# Ethereum Exchange Flows

For Ethereum currently supported exchanges are: binance, kraken, bitfinex, poloniex, bittrex, kucoin 

## 24h Inflow to Exchanges

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_historical`

> This is an example:

```shell
$ curl https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_historical
&token=eth
&exchange=binance
&direction=inflow
&format=json
&key=API_KEY
```

> The response looks like:

```json
[
  {
    "interval": "0",
    "inflow": "5911.448933881129",
    "number_of_txns": "1547",
    "avg_txn_value": "3.821233958552766",
    "inflow_usd": "928740.6196874918",
    "avg_txn_value_usd": "600.3494632756896",
    "inflow_pct_change": "-2.9685234253404533",
    "avg_txn_value_pct_change": "-16.014772376555182",
    "inflow_usd_pct_change": "-3.864169979573276",
    "avg_txn_value_usd_pct_change": "-16.789995864672665",
    "entity": "Binance"
  }
]
```

### URL Parameters

Parameter | Description
--------- | -----------
token |  eth 
exchange | An exchange from the list 
direction | Either inflow or outflow
format | Either json or csv
key | API key

## 24h Outflows from Exchanges 

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_historical`

> This is an example:

```shell
$ curl https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_historical
&token=eth
&exchange=binance
&direction=outflow
&format=json
&key=API_KEY
```

> The response looks like:

```json
[
  {
    "interval": "0",
    "outflow": "3385.888988630001",
    "number_of_txns": "219",
    "avg_txn_value": "15.460680313379001",
    "outflow_usd": "531632.257609205",
    "avg_txn_value_usd": "2427.5445552931737",
    "outflow_pct_change": "26.88818573447446",
    "avg_txn_value_pct_change": "-12.510885635134056",
    "outflow_usd_pct_change": "25.514392540253446",
    "avg_txn_value_usd_pct_change": "-13.458112906035282",
    "entity": "Binance"
  }
]
```

### URL Parameters

Parameter | Description
--------- | -----------
token |  eth 
exchange | An exchange from the list 
direction | Either inflow or outflow
format | Either json or csv
key | API key


## 24h Top 10 Inflow Large Value Transactions 

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_top10_historical`

> This is an example:

```shell
$ curl https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_top10_historical
&token=eth
&exchange=binance
&direction=infow
&format=json
&key=API_KEY
```

> The response looks like:

```json
[
   {
    "toaddress":"0x59a5208B32e627891C389EbafC644145224006E8",
    "fromaddress":"0xA12431D0B9dB640034b0CDFcEEF9CCe161e62be4",
    "transactionhash":"0xf24ddce2e5788eda153edf18406e982352fbf017957fcddc7054f4366a53117e",
    "value_usd":"157089.90478515625",
    "value":"1000.0"
   },
...]
```

### URL Parameters

Parameter | Description
--------- | -----------
token |  The token (in this case eth) 
exchange | An exchange from the list 
direction | Either inflow or outflow (in this case inflow)
format | Either json or csv
key | API key

## 24h Top 10 Outflow Large Value Transactions 

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_top10_historical`

```shell
$ curl https://api.tokenanalyst.io/analytics/private/v1/last/exchange_flow_top10_historical
&token=eth
&exchange=binance
&direction=outflow
&format=json
&key=API_KEY
```


```json
[
  {
    "toaddress": "0xA0e56f656c89e4819909d921a880329Bc9BC8E38",
    "fromaddress": "0x876EabF441B2EE5B5b0554Fd502a8E0600950cFa",
    "transactionhash": "0x9e4f6ea067bcd617cbd713f78873bb233bcb9b6604f6183b497817c7471f9b51",
    "value_usd": "1571033.6690427142",
    "value": "10009.998650000001"
  },...
]
```

### URL Parameters

Parameter | Description
--------- | -----------
token |  The token (in this case eth) 
exchange | An exchange from the list 
direction | Either inflow or outflow (in this case inflow)
format | Either json or csv
key | API key

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

