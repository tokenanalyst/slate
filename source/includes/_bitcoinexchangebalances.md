# Bitcoin Exchange Balance 

## BTC Full Historical Balance

<img src="https://img.shields.io/badge/Tier-Professional-black.svg"/>

This endpoint returns the full historical on-chain balance of Bitcoin for as far back as we can track.

```shell
# Make sure you substitute API_KEY for your unique API key.

curl "https://api.tokenanalyst.io/analytics/private/v1/exchange_balance_window_historical/last?key=API_KEY&limit=2&format=json&exchange=binance&token=btc&window=1h"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2019-10-04",
    "hour": "12:00:00", // not available when window 1d
    "datetime": "2019-10-04 12:00:00", // not available when window 1d
    "balance": 242107.08456132,
    "balance_usd": 1976383805.44
  },
  {
    "date": "2019-10-04",
    "hour": "13:00:00", // not available when window 1d
    "datetime": "2019-10-04 13:00:00", // not available when window 1d
    "balance": 242107.08456132,
    "balance_usd": 0
  }
]
```

### HTTP Request

`GET https://api.tokenanalyst.io/analytics/private/v1/exchange_balance_window_historical/last`

### Query Parameters

| Parameter    | Type      | Description                                                                               |
| ------------ | --------- | ----------------------------------------------------------------------------------------- |
| key          | _string_  | Your unique API key                                                                       |
| format       | _string_  | What format you want your data in (`json` or `csv`)                                       |
| token        | _string_  | `btc`                                                                                     |                                    |
| exchange     | _string_  | An exchange from the list of ones we support                                              |
| window       | _string_  | `1h` or `1d`                                                                              |
| from_date \* | _string_  | Start date of returned data specified as YYYY-MM-DD (ISO date format)                     |
| to_date \*   | _string_  | End date of returned data specified as YYYY-MM-DD (ISO date format)                       |
| limit \*     | _integer_ | The number of entries returned before the latest data point (or the to_date if specified) |

Note: All params with a \* are optional and `limit` is only available in the JSON return format

### Data Overview

| Field                                   | Type      | Description                                                                                                                                                                                                               |
| --------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| balance                                 | _decimal_ | The amount of BTC on a given exchange on this date.                                                                                                                                |
| balance_usd                             | _decimal_ | The USD value of the amount of BTC on a given exchange on this date.                                                                                                            |
| date                                    | _string_  | The date in _YYYY-MM-DD_                                                                                                                                                                                                  |
| datetime *                              | _string_  | The hour of the day in datetime format YYYY-MM-DD HH:MM:SS (UTC time zone). This is an optional field field and appears when window is `1h`                                                                               |
| hour *                                  | _string_  | The hour of the day in _HH:MM:SS_ (UTC time zone). This is an optional field field and appears when window is `1h`                                                                                                        |
