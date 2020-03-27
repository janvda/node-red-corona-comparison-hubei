node-red-corona-comparison-hubei
================================

# Description

This node-red flow is creating a dashboard showing the historical statistics of the corona deaths and corona confirmed cases for the selected country or province/state.

The statistics are retrieved from [github.com/CSSEGISandData/COVID-19](https://github.com/CSSEGISandData/COVID-19).  More precisely it is based on the following 2 files from this github repository:
 - [time_series_covid19_deaths_global.csv](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_deaths_global.csv)
 - [time_series_covid19_confirmed_global.csv](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)

It also puts in the same charts the statistics for the province Hubei (China) were the outbreak began.  To make comparison easy I have scaled and shifted the chart for Hubei.

The time shift (`"hubei date shift"`) is determined by the `"lock down date"` that you can specify.  So the Hubei charts will be shifted so that the lock down date of Hubei (= 23rd of January 2020) falls together with the `"lock down date"` you have specified.

The `"hubei factor"` is the factor used to scale the Hubei deaths and Hubei confirmed cases in the charts.  The `"hubei factor"` is calculated as the ratio of the current total number of deaths for the selected country or province over the total number of deaths in Hubei at corresponding date relative to the start of lock down.

It is also possible to smooth the Hubei data in the charts by clicking on the `"smooth Hubei charts"` toggle button.  When activated it has the following effect on the Hubei:
1. The new confirmed cases for days 12, 13 and 14 of February 2020 have been replaced by _interpolated_ values.  This is to get rid of the big spike caused due to the new way of testing at that time.
2. furthermore the new confirmed cases andnew deatsh for Hubei have been smoothed by taking a weighted running average of 3 points.  So the smoothed value for point i is calculated as 50% of value of point i + 25% of the values of point i-1 and point i+1.
3. total deaths and total confirmed cases are recalculated based on smoothed new deaths and smoothed new confirmed cases (see points 1 and 2)

Tip: you can also clearly visualize the effect of smoothing by selecting as country "China" and as province/state "Hubei" and then activating the `smooth Hubei charts` toggle button

# Examples

See Node-RED forum thread: [Corona country comparison with Hubei (China)](https://discourse.nodered.org/t/flow-corona-country-comparison-with-hubei-china/23237)

# Usage
At startup this flow will read the statistics from a local file `"covid.json"`.  The very first time this local file will not exist and an error message is reported in the dashboard (this is normal).
So in that case you must retrieve the data from Github by clicking on the button `retrieve data from github`.
Note that this takes several minutes.  You will even loose your browser connection.  This is expected.  Just be patient and you will be automatically reconnected.  If everything is fine then this data is also stored in the local file.

FYI it is not the retrieving that takes a lot of time but converting the data to proper json structure that is time consuming.

Once the data is retrieved, you can select the `country`, `province/state` and `lock down date` and the charts will automatically be updated.

You can always refresh the data with the latest available data from github by clicking on the button (but as said this takes several minutes).


