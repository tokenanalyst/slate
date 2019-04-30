---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href="https://sid296635.typeform.com/to/abg0kL" target="_blank">Get your API key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the TokenAnalyst API. We provide simple and powerful endpoints, which you can use to get information on basic transaction data and aggregate on-chain statistics derived directly from the blockchain. This API reference provides information on available endpoints and how to interact with it.

# Authentication

TokenAnalyst uses API keys to allow access to the API. To obtain your API key contact us <a href="https://sid296635.typeform.com/to/abg0kL" target="_blank">here</a>
.

TokenAnalyst expects for the API key to be included in all API requests to the server. You can simply include the key in the URL parameters like:

`key=API_KEY`

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: API_KEY"
```

<aside class="notice">
You must replace <code>API_KEY</code> with your personal API key.
</aside>

# Bitcoin Stats

## On-chain Volume

```shell
curl "https://ws.tokenanalyst.io/analytics/private/last?job=token_volume_historical&format=json&key=API_KEY&token=btc"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2009-04-13",
    "volume_gross": "50.0",
    "volume_change": "40.0",
    "volume_real": "10.0",
    "price_usd": "",
    "volume_real_usd": "",
    "volume_change_usd": ""
  },
  {
    "date": "2009-04-18",
    "volume_gross": "182.51",
    "volume_change": "17.49",
    "volume_real": "165.01999999999998",
    "price_usd": "",
    "volume_real_usd": "",
    "volume_change_usd": ""
  }
]
```

This endpoint returns the full historical on-chain volume of Bitcoin since it's genesis in 2009. The volume is separated into 'real' volume and 'change' volume.

Our current heuristic for 'change' related volume is for whenever BTC in a transaction is sent back to the same address that sent the BTC. The 'real' volume is simply the remainder left over after subtracting the change.

### HTTP Request

`GET https://ws.tokenanalyst.io/analytics/private/last?job=token_volume_historical`

### Query Parameters

| Parameter | Type   | Description                                                   |
| --------- | ------ | ------------------------------------------------------------- |
| key       | _string_ | Your unique API key                                           |
| format    | _string_ | What format you want your data in (currently we support JSON) |
| token     | _string_ | The token you want the volume for (in this case `btc`)        |




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
const kittn = require("kittn");

let api = kittn.authorize("meowmeowmeow");
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

| Parameter | Description                      |
| --------- | -------------------------------- |
| ID        | The ID of the kitten to retrieve |

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
const kittn = require("kittn");

let api = kittn.authorize("meowmeowmeow");
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted": ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the kitten to delete |
