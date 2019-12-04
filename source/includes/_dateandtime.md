# Date & Time Conventions

Throughout this API a `window` parameter is used to indicate the time intervals for which the data is aggregated. We currently offer daily (denoted by `window=1d`) and hourly (denoted by `window=1h`) endpoints. 

<aside class="success">
We use a 3 block confirmation methodology in all our calculations, therefore, the latest hour data may change when the following hour is calculated due to these block lags. Due to this, if you want the data for a full day (1 day bar), the safe time to query the endpoint would be 2 hours after the day (i.e 2 AM UTC the following day if you want data for 12:00 AM - 11:59 PM UTC).
</aside>


| Window | Description     | 
| --------- | -------- | 
| `1d`       | Data returned per day for every day historically for which data exists for the endpoint in question. The latest day returned is the last full day of data. Each day runs from 0:00:00 UTC to 23:59:59 UTC. | 
| `1h`    | Data returned per hour for every hour for which data exists for the endpoint in question. All times are in UTC. The displayed hour in the data is the start of the hour for which the data is aggregated. For example if `"hour":"22:00:00"`, it represents data from 22:00:00 to 22:59:59 UTC. | 


<aside class="warning">
Note: Not all endpoints support hourly data yet. See the specific docs below to see if the `window=1h` param is supported for your desired endpoint
</aside>