TimeSeries.OBeu
================
Kleanthis Koupidis, Charalampos Bratsas

[TimeSeries.OBeu](https://okgreece.github.io/TimeSeries.OBeu/)
==============================================================

Εstimate and return the necessary parameters for time series visualizations, used in [OpenBudgets.eu](http://openbudgets.eu/). It includes functions to test stationarity (with ACF, PACF, Phillips Perron test, Augmented Dickey Fuller (ADF) test, Kwiatkowski-Phillips-Schmidt-Shin (KPSS) test, Mann Kendall Test For Monotonic Trend and Cox and Stuart trend test), decompose, model and forecast Budget time series data of municipalities across Europe, according to the [OpenBudgets.eu data model](https://github.com/openbudgets/data-model).

This package can generally be used to extract visualization parameters convert them to JSON format and use them as input in a different graphical interface. Most functions can have general use out of the [OpenBudgets.eu data model](https://github.com/openbudgets/data-model). You can see detailed information [here](https://okgreece.github.io/TimeSeries.OBeu/).

``` r
# install TimeSeries.OBeu- cran stable version
install.packages(TimeSeries.OBeu) 
# or
# alternatively install the development version from github
devtools::install_github("okgreece/TimeSeries.OBeu")
```

Load library `TimeSeries.OBeu`

``` r
library(TimeSeries.OBeu)
```

Time Series analysis in a call
==============================

`ts.analysis` is used to estimate *autocorrelation and partial autocorrelation* of input time series data, *autocorrelation and partial autocorrelation* of the model residuals, *trend*, *seasonal* (if exists) and *remainder* components, model parameters such as arima order, arima coefficients etc. and the desired *forecasts* with their corresponding confidence intervals.

`ts.analysis` returns by default a json object, if `tojson` parameter is `FALSE` returns a list object and the default forecast step is set to 1.

``` r
results = ts.analysis(Athens_executed_ts, prediction.steps = 2, tojson=TRUE) # json string format
jsonlite::prettify(results) # use prettify of jsonlite library to add indentation to the returned JSON string
```

    ## {
    ##     "acf.param": {
    ##         "acf.parameters": {
    ##             "acf": [
    ##                 1,
    ##                 0.5302,
    ##                 0.2018,
    ##                 -0.1397,
    ##                 -0.4059,
    ##                 -0.3556,
    ##                 -0.3939,
    ##                 -0.073,
    ##                 0.071,
    ##                 0.0676,
    ##                 0.0285
    ##             ],
    ##             "acf.lag": [
    ##                 0,
    ##                 1,
    ##                 2,
    ##                 3,
    ##                 4,
    ##                 5,
    ##                 6,
    ##                 7,
    ##                 8,
    ##                 9,
    ##                 10
    ##             ],
    ##             "confidence.interval.up": [
    ##                 0.5658
    ##             ],
    ##             "confidence.interval.low": [
    ##                 -0.5658
    ##             ]
    ##         },
    ##         "pacf.parameters": {
    ##             "pacf": [
    ##                 0.5302,
    ##                 -0.1102,
    ##                 -0.2817,
    ##                 -0.2903,
    ##                 0.0427,
    ##                 -0.2781,
    ##                 0.2318,
    ##                 -0.1163,
    ##                 -0.1829,
    ##                 -0.209
    ##             ],
    ##             "pacf.lag": [
    ##                 1,
    ##                 2,
    ##                 3,
    ##                 4,
    ##                 5,
    ##                 6,
    ##                 7,
    ##                 8,
    ##                 9,
    ##                 10
    ##             ],
    ##             "confidence.interval.up": [
    ##                 0.5658
    ##             ],
    ##             "confidence.interval.low": [
    ##                 -0.5658
    ##             ]
    ##         },
    ##         "acf.residuals.parameters": {
    ##             "acf.residuals": [
    ##                 1,
    ##                 0.8646,
    ##                 0.7284,
    ##                 0.6039,
    ##                 0.4589,
    ##                 0.3295,
    ##                 0.154,
    ##                 -0.0016,
    ##                 -0.1241,
    ##                 -0.2595,
    ##                 -0.3802,
    ##                 -0.5098,
    ##                 -0.6276,
    ##                 -0.5885,
    ##                 -0.5207,
    ##                 -0.4629
    ##             ],
    ##             "acf.residuals.lag": [
    ##                 0,
    ##                 1,
    ##                 2,
    ##                 3,
    ##                 4,
    ##                 5,
    ##                 6,
    ##                 7,
    ##                 8,
    ##                 9,
    ##                 10,
    ##                 11,
    ##                 12,
    ##                 13,
    ##                 14,
    ##                 15
    ##             ],
    ##             "confidence.interval.up": [
    ##                 0.5658
    ##             ],
    ##             "confidence.interval.low": [
    ##                 -0.5658
    ##             ]
    ##         },
    ##         "pacf.residuals.parameters": {
    ##             "pacf.residuals": [
    ##                 0.8646,
    ##                 -0.0756,
    ##                 -0.0325,
    ##                 -0.1597,
    ##                 -0.0335,
    ##                 -0.2937,
    ##                 -0.0528,
    ##                 -0.046,
    ##                 -0.162,
    ##                 -0.1372,
    ##                 -0.2201,
    ##                 -0.2078,
    ##                 0.4336,
    ##                 0.1187,
    ##                 -0.0519
    ##             ],
    ##             "pacf.residuals.lag": [
    ##                 1,
    ##                 2,
    ##                 3,
    ##                 4,
    ##                 5,
    ##                 6,
    ##                 7,
    ##                 8,
    ##                 9,
    ##                 10,
    ##                 11,
    ##                 12,
    ##                 13,
    ##                 14,
    ##                 15
    ##             ],
    ##             "confidence.interval.up": [
    ##                 0.5658
    ##             ],
    ##             "confidence.interval.low": [
    ##                 -0.5658
    ##             ]
    ##         }
    ##     },
    ##     "decomposition": {
    ##         "stl.plot": {
    ##             "trend": [
    ##                 488397393.1091,
    ##                 472512470.2805,
    ##                 473063423.4839,
    ##                 487284165.8281,
    ##                 519914575.4486,
    ##                 549044538.1581,
    ##                 546747322.3717,
    ##                 517885722.186,
    ##                 482561749.2963,
    ##                 453474237.5689,
    ##                 423909077.9758,
    ##                 393617768.3187
    ##             ],
    ##             "conf.interval.up": [
    ##                 525849686.8842,
    ##                 495462596.0604,
    ##                 495888427.6281,
    ##                 512171768.3925,
    ##                 545880538.4876,
    ##                 575706534.5412,
    ##                 573409318.7548,
    ##                 543851685.225,
    ##                 507449351.8607,
    ##                 476299241.7132,
    ##                 446859203.7557,
    ##                 431070062.0938
    ##             ],
    ##             "conf.interval.low": [
    ##                 450945099.334,
    ##                 449562344.5005,
    ##                 450238419.3396,
    ##                 462396563.2637,
    ##                 493948612.4097,
    ##                 522382541.7751,
    ##                 520085325.9887,
    ##                 491919759.147,
    ##                 457674146.7319,
    ##                 430649233.4247,
    ##                 400958952.1958,
    ##                 356165474.5436
    ##             ],
    ##             "seasonal": {
    ## 
    ##             },
    ##             "remainder": [
    ##                 3494473.6909,
    ##                 -6782427.4905,
    ##                 -360030.3839,
    ##                 -20859217.1881,
    ##                 8715868.0414,
    ##                 20321961.4419,
    ##                 -24805255.8217,
    ##                 12476896.984,
    ##                 -25628827.4663,
    ##                 18714394.8611,
    ##                 -9197723.8358,
    ##                 1891498.5713
    ##             ],
    ##             "time": [
    ##                 2004,
    ##                 2005,
    ##                 2006,
    ##                 2007,
    ##                 2008,
    ##                 2009,
    ##                 2010,
    ##                 2011,
    ##                 2012,
    ##                 2013,
    ##                 2014,
    ##                 2015
    ##             ]
    ##         },
    ##         "stl.general": {
    ##             "degfr": [
    ##                 5.4179
    ##             ],
    ##             "degfr.fitted": [
    ##                 5.1011
    ##             ],
    ##             "stl.degree": [
    ##                 2
    ##             ]
    ##         },
    ##         "residuals_fitted": {
    ##             "residuals": [
    ##                 3494473.6909,
    ##                 -6782427.4905,
    ##                 -360030.3839,
    ##                 -20859217.1881,
    ##                 8715868.0414,
    ##                 20321961.4419,
    ##                 -24805255.8217,
    ##                 12476896.984,
    ##                 -25628827.4663,
    ##                 18714394.8611,
    ##                 -9197723.8358,
    ##                 1891498.5713
    ##             ],
    ##             "fitted": [
    ##                 488397393.1091,
    ##                 472512470.2805,
    ##                 473063423.4839,
    ##                 487284165.8281,
    ##                 519914575.4486,
    ##                 549044538.1581,
    ##                 546747322.3717,
    ##                 517885722.186,
    ##                 482561749.2963,
    ##                 453474237.5689,
    ##                 423909077.9758,
    ##                 393617768.3187
    ##             ],
    ##             "time": [
    ##                 2004,
    ##                 2005,
    ##                 2006,
    ##                 2007,
    ##                 2008,
    ##                 2009,
    ##                 2010,
    ##                 2011,
    ##                 2012,
    ##                 2013,
    ##                 2014,
    ##                 2015
    ##             ],
    ##             "line": [
    ##                 0
    ##             ]
    ##         },
    ##         "compare": {
    ##             "resid.variance": [
    ##                 258964785711184
    ##             ],
    ##             "used.obs": [
    ##                 2004,
    ##                 2015,
    ##                 2009.5,
    ##                 2006.75,
    ##                 2012.25
    ##             ],
    ##             "loglik": [
    ##                 -1.42430632141151e+015
    ##             ],
    ##             "aic": [
    ##                 2.84861264282304e+015
    ##             ],
    ##             "bic": [
    ##                 2.84861264282304e+015
    ##             ],
    ##             "gcv": [
    ##                 789007326652162
    ##             ]
    ##         }
    ##     },
    ##     "model.param": {
    ##         "model": {
    ##             "arima.order": [
    ##                 2,
    ##                 1,
    ##                 0,
    ##                 0,
    ##                 1,
    ##                 1,
    ##                 0
    ##             ],
    ##             "arima.coef": [
    ##                 -0.2,
    ##                 0.304,
    ##                 0.1684
    ##             ],
    ##             "arima.coef.se": [
    ##                 0.5484,
    ##                 0.3034,
    ##                 0.5345
    ##             ]
    ##         },
    ##         "residuals_fitted": {
    ##             "residuals": [
    ##                 491891.5916,
    ##                 -24734053.8013,
    ##                 4848198.2869,
    ##                 2291242.4698,
    ##                 58442566.8183,
    ##                 45241384.4941,
    ##                 -65806529.3585,
    ##                 -2362504.0059,
    ##                 -56932278.3288,
    ##                 7600701.3147,
    ##                 -33386168.6854,
    ##                 -29710365.2918
    ##             ],
    ##             "fitted": [
    ##                 491399975.2084,
    ##                 490464096.5913,
    ##                 467855194.8131,
    ##                 464133706.1702,
    ##                 470187876.6717,
    ##                 524125115.1059,
    ##                 587748595.9085,
    ##                 532725123.1759,
    ##                 513865200.1588,
    ##                 464587931.1153,
    ##                 448097522.8254,
    ##                 425219632.1818
    ##             ],
    ##             "time": [
    ##                 2004,
    ##                 2005,
    ##                 2006,
    ##                 2007,
    ##                 2008,
    ##                 2009,
    ##                 2010,
    ##                 2011,
    ##                 2012,
    ##                 2013,
    ##                 2014,
    ##                 2015
    ##             ],
    ##             "line": [
    ##                 0
    ##             ]
    ##         },
    ##         "compare": {
    ##             "resid.variance": [
    ##                 1.96694555669531e+015
    ##             ],
    ##             "variance.coef": [
    ##                 [
    ##                     0.3007,
    ##                     0.0586,
    ##                     -0.2532
    ##                 ],
    ##                 [
    ##                     0.0586,
    ##                     0.0921,
    ##                     -0.029
    ##                 ],
    ##                 [
    ##                     -0.2532,
    ##                     -0.029,
    ##                     0.2857
    ##                 ]
    ##             ],
    ##             "not.used.obs": [
    ##                 0
    ##             ],
    ##             "used.obs": [
    ##                 11
    ##             ],
    ##             "loglik": [
    ##                 -207.6519
    ##             ],
    ##             "aic": [
    ##                 423.3037
    ##             ],
    ##             "bic": [
    ##                 424.8953
    ##             ],
    ##             "aicc": [
    ##                 429.9704
    ##             ]
    ##         }
    ##     },
    ##     "forecasts": {
    ##         "ts.model": [
    ##             "ARIMA(2,1,1)"
    ##         ],
    ##         "data_year": [
    ##             2004,
    ##             2005,
    ##             2006,
    ##             2007,
    ##             2008,
    ##             2009,
    ##             2010,
    ##             2011,
    ##             2012,
    ##             2013,
    ##             2014,
    ##             2015
    ##         ],
    ##         "data": [
    ##             491891866.8,
    ##             465730042.79,
    ##             472703393.1,
    ##             466424948.64,
    ##             528630443.49,
    ##             569366499.6,
    ##             521942066.55,
    ##             530362619.17,
    ##             456932921.83,
    ##             472188632.43,
    ##             414711354.14,
    ##             395509266.89
    ##         ],
    ##         "predict_time": [
    ##             2016,
    ##             2017
    ##         ],
    ##         "predict_values": [
    ##             376873927.6929,
    ##             374763602.0226
    ##         ],
    ##         "up80": [
    ##             433711072.7506,
    ##             453885516.7716
    ##         ],
    ##         "low80": [
    ##             320036782.6353,
    ##             295641687.2737
    ##         ],
    ##         "up95": [
    ##             463798839.8792,
    ##             495770128.3811
    ##         ],
    ##         "low95": [
    ##             289949015.5067,
    ##             253757075.6642
    ##         ]
    ##     }
    ## }
    ## 

`ts.analysis` uses internally the functions `ts.stationary.test`,`ts.acf`,`ts.non.seas.decomp`,`ts.seasonal.decomp`, `ts.seasonal.model`, `ts.non.seas.model` and `ts.forecast`. However, these functions can be used independently and depends on the user requirements (see package manual or vignettes).

Time series analysis on OpenBudgets.eu platform
===============================================

`open_spending.ts` is designed to estimate and return the autocorrelation parameters, time series model parameters and the forecast parameters of [OpenBudgets.eu](http://openbudgets.eu/) time series datasets.

The input data must be a JSON link according to the [OpenBudgets.eu data model](https://github.com/openbudgets/data-model). The user should specify the amount and time variables, future steps to be predicted (default is 1 step forward) and the arima order (if not specified the most appropriate model will be selected according to AIC value).

`open_spending.ts` estimates and returns the json data (that are described with the [OpenBudgets.eu data model](https://github.com/openbudgets/data-model)), using `ts.analysis` function.

``` r
#example openbudgets.eu time series data
sample.ts.data = 
'{"page":0,
"page_size": 30,
"total_cell_count": 15,
"cell": [],
"status": "ok",
"cells": [{
        "global__fiscalPeriod__28951.notation": "2002",
        "global__amount__0397f.sum": 290501420.64,
        "global__amount__0397f__CZK.sum": 9210928544.2325,
        "_count": 4805
    },
    {
        "global__fiscalPeriod__28951.notation": "2003",
        "global__amount__0397f.sum": 311242291.07,
        "global__amount__0397f__CZK.sum": 9832143974.9013,
        "_count": 4988
    },
    {
        "global__fiscalPeriod__28951.notation": "2004",
        "global__amount__0397f.sum": 5268500701.1,
        "global__amount__0397f__CZK.sum": 170688885714.24,
        "_count": 10055
    },
    {
        "global__fiscalPeriod__28951.notation": "2005",
        "global__amount__0397f.sum": 2542887761.01,
        "global__amount__0397f__CZK.sum": 77204615312.025,
        "_count": 2032
    },
    {
        "global__fiscalPeriod__28951.notation": "2006",
        "global__amount__0397f.sum": 14803951786.68,
        "global__amount__0397f__CZK.sum": 429758720367.32,
        "_count": 13632
    },
    {
        "global__fiscalPeriod__28951.notation": "2007",
        "global__amount__0397f.sum": 16188514346.44,
        "global__amount__0397f__CZK.sum": 445588857385.76,
        "_count": 22798
    },
    {
        "global__fiscalPeriod__28951.notation": "2008",
        "global__amount__0397f.sum": 18231035815.89,
        "global__amount__0397f__CZK.sum": 480643028250.12,
        "_count": 24176
    },
    {
        "global__fiscalPeriod__28951.notation": "2009",
        "global__amount__0397f.sum": 19079541164.68,
        "global__amount__0397f__CZK.sum": 511808691742.54,
        "_count": 26250
    },
    {
        "global__fiscalPeriod__28951.notation": "2010",
        "global__amount__0397f.sum": 22738650575.01,
        "global__amount__0397f__CZK.sum": 597685430364.14,
        "_count": 87667
    },
    {
        "global__fiscalPeriod__28951.notation": "2011",
        "global__amount__0397f.sum": 24961375670.57,
        "global__amount__0397f__CZK.sum": 626230992823.26,
        "_count": 134352
    },
    {
        "global__fiscalPeriod__28951.notation": "2012",
        "global__amount__0397f.sum": 261513607691.41,
        "global__amount__0397f__CZK.sum": 7030666436872.5,
        "_count": 147556
    },
    {
        "global__fiscalPeriod__28951.notation": "2013",
        "global__amount__0397f.sum": 268946402299.09,
        "global__amount__0397f__CZK.sum": 7226220232913.8,
        "_count": 150079
    },
    {
        "global__fiscalPeriod__28951.notation": "2014",
        "global__amount__0397f.sum": 255222816704.9,
        "global__amount__0397f__CZK.sum": 6907598086283.4,
        "_count": 176019
    },
    {
        "global__fiscalPeriod__28951.notation": "2015",
        "global__amount__0397f.sum": 22976062973.62,
        "global__amount__0397f__CZK.sum": 636276111928.46,
        "_count": 213777
    },
    {
        "global__fiscalPeriod__28951.notation": "2016",
        "global__amount__0397f.sum": 12051686541.16,
        "global__amount__0397f__CZK.sum": 325672725401.77,
        "_count": 161797
    }
],
"order": [
    ["global__fiscalPeriod__28951.fiscalPeriod", "asc"]
],
"aggregates": ["", "_count"],
"summary": {
    "global__amount__0397f.sum": 945126777743.27,
    "global__amount__0397f__CZK.sum": 25485085887878
},
"attributes": [""]
}'

result = open_spending.ts(
  json_data =  sample.ts.data, 
  time ="global__fiscalPeriod__28951.notation",
  amount = "global__amount__0397f.sum"
  )
# Pretty output using prettify of jsonlite library
jsonlite::prettify(result,indent = 2)
```

    ## {
    ##   "acf.param": {
    ##     "acf.parameters": {
    ##       "acf": [
    ##         1,
    ##         0.6083,
    ##         0.1674,
    ##         -0.1663,
    ##         -0.1295,
    ##         -0.0727,
    ##         -0.0925,
    ##         -0.1301,
    ##         -0.1615,
    ##         -0.1959,
    ##         -0.2115,
    ##         -0.1311
    ##       ],
    ##       "acf.lag": [
    ##         0,
    ##         1,
    ##         2,
    ##         3,
    ##         4,
    ##         5,
    ##         6,
    ##         7,
    ##         8,
    ##         9,
    ##         10,
    ##         11
    ##       ],
    ##       "confidence.interval.up": [
    ##         0.5061
    ##       ],
    ##       "confidence.interval.low": [
    ##         -0.5061
    ##       ]
    ##     },
    ##     "pacf.parameters": {
    ##       "pacf": [
    ##         0.6083,
    ##         -0.3215,
    ##         -0.1865,
    ##         0.25,
    ##         -0.1593,
    ##         -0.1764,
    ##         0.0869,
    ##         -0.1346,
    ##         -0.2117,
    ##         -0.0036,
    ##         0.0508
    ##       ],
    ##       "pacf.lag": [
    ##         1,
    ##         2,
    ##         3,
    ##         4,
    ##         5,
    ##         6,
    ##         7,
    ##         8,
    ##         9,
    ##         10,
    ##         11
    ##       ],
    ##       "confidence.interval.up": [
    ##         0.5061
    ##       ],
    ##       "confidence.interval.low": [
    ##         -0.5061
    ##       ]
    ##     },
    ##     "acf.residuals.parameters": {
    ##       "acf.residuals": [
    ##         1,
    ##         0.3097,
    ##         0.2296,
    ##         -0.2346,
    ##         -0.0115,
    ##         -0.069,
    ##         -0.0524,
    ##         -0.0981,
    ##         -0.0842,
    ##         -0.1215,
    ##         -0.0934,
    ##         -0.0868,
    ##         -0.0484,
    ##         -0.2128,
    ##         -0.115,
    ##         -0.1051,
    ##         0.2946
    ##       ],
    ##       "acf.residuals.lag": [
    ##         0,
    ##         1,
    ##         2,
    ##         3,
    ##         4,
    ##         5,
    ##         6,
    ##         7,
    ##         8,
    ##         9,
    ##         10,
    ##         11,
    ##         12,
    ##         13,
    ##         14,
    ##         15,
    ##         16
    ##       ],
    ##       "confidence.interval.up": [
    ##         0.5061
    ##       ],
    ##       "confidence.interval.low": [
    ##         -0.5061
    ##       ]
    ##     },
    ##     "pacf.residuals.parameters": {
    ##       "pacf.residuals": [
    ##         0.3097,
    ##         0.1479,
    ##         -0.3857,
    ##         0.1673,
    ##         0.0455,
    ##         -0.2432,
    ##         0.0379,
    ##         0.0137,
    ##         -0.2159,
    ##         0.0048,
    ##         0.0175,
    ##         -0.1445,
    ##         -0.2757,
    ##         0.0882,
    ##         -0.0175,
    ##         0.2238
    ##       ],
    ##       "pacf.residuals.lag": [
    ##         1,
    ##         2,
    ##         3,
    ##         4,
    ##         5,
    ##         6,
    ##         7,
    ##         8,
    ##         9,
    ##         10,
    ##         11,
    ##         12,
    ##         13,
    ##         14,
    ##         15,
    ##         16
    ##       ],
    ##       "confidence.interval.up": [
    ##         0.5061
    ##       ],
    ##       "confidence.interval.low": [
    ##         -0.5061
    ##       ]
    ##     }
    ##   },
    ##   "decomposition": {
    ##     "stl.plot": {
    ##       "trend": [
    ##         -823419544.04,
    ##         1661560665.9804,
    ##         4624784833.2485,
    ##         7878983909.6147,
    ##         9164365784.5264,
    ##         1249040776.0474,
    ##         -4351015666.9835,
    ##         6551641382.3009,
    ##         57664029716.5692,
    ##         135646130024.628,
    ##         199114831577.553,
    ##         212547970266.68,
    ##         183231679540.212,
    ##         110152904453.676,
    ##         -12061960507.0426
    ##       ],
    ##       "conf.interval.up": [
    ##         100039247758.34,
    ##         66576136730.9101,
    ##         60840745923.6514,
    ##         68328241465.8754,
    ##         72409579665.7543,
    ##         65432105297.0944,
    ##         59676059487.2765,
    ##         70171989437.8921,
    ##         121691104870.829,
    ##         199829194545.675,
    ##         262360045458.781,
    ##         272997227822.941,
    ##         239447640630.614,
    ##         175067480518.606,
    ##         88800706795.3375
    ##       ],
    ##       "conf.interval.low": [
    ##         -101686086846.42,
    ##         -63253015398.9493,
    ##         -51591176257.1543,
    ##         -52570273646.646,
    ##         -54080848096.7016,
    ##         -62934023744.9996,
    ##         -68378090821.2435,
    ##         -57068706673.2904,
    ##         -6363045437.6908,
    ##         71463065503.5815,
    ##         135869617696.325,
    ##         152098712710.42,
    ##         127015718449.809,
    ##         45238328388.7462,
    ##         -112924627809.423
    ##       ],
    ##       "seasonal": {
    ## 
    ##       },
    ##       "remainder": [
    ##         1113920964.68,
    ##         -1350318374.9104,
    ##         643715867.8515,
    ##         -5336096148.6047,
    ##         5639586002.1536,
    ##         14939473570.3926,
    ##         22582051482.8735,
    ##         12527899782.3791,
    ##         -34925379141.5592,
    ##         -110684754354.058,
    ##         62398776113.8568,
    ##         56398432032.4096,
    ##         71991137164.6884,
    ##         -87176841480.0559,
    ##         24113647048.2026
    ##       ],
    ##       "time": [
    ##         2002,
    ##         2003,
    ##         2004,
    ##         2005,
    ##         2006,
    ##         2007,
    ##         2008,
    ##         2009,
    ##         2010,
    ##         2011,
    ##         2012,
    ##         2013,
    ##         2014,
    ##         2015,
    ##         2016
    ##       ]
    ##     },
    ##     "stl.general": {
    ##       "degfr": [
    ##         5.288
    ##       ],
    ##       "degfr.fitted": [
    ##         4.9747
    ##       ],
    ##       "stl.degree": [
    ##         2
    ##       ]
    ##     },
    ##     "residuals_fitted": {
    ##       "residuals": [
    ##         1113920964.68,
    ##         -1350318374.9104,
    ##         643715867.8515,
    ##         -5336096148.6047,
    ##         5639586002.1536,
    ##         14939473570.3926,
    ##         22582051482.8735,
    ##         12527899782.3791,
    ##         -34925379141.5592,
    ##         -110684754354.058,
    ##         62398776113.8568,
    ##         56398432032.4096,
    ##         71991137164.6884,
    ##         -87176841480.0559,
    ##         24113647048.2026
    ##       ],
    ##       "fitted": [
    ##         -823419544.04,
    ##         1661560665.9804,
    ##         4624784833.2485,
    ##         7878983909.6147,
    ##         9164365784.5264,
    ##         1249040776.0474,
    ##         -4351015666.9835,
    ##         6551641382.3009,
    ##         57664029716.5692,
    ##         135646130024.628,
    ##         199114831577.553,
    ##         212547970266.68,
    ##         183231679540.212,
    ##         110152904453.676,
    ##         -12061960507.0426
    ##       ],
    ##       "time": [
    ##         2002,
    ##         2003,
    ##         2004,
    ##         2005,
    ##         2006,
    ##         2007,
    ##         2008,
    ##         2009,
    ##         2010,
    ##         2011,
    ##         2012,
    ##         2013,
    ##         2014,
    ##         2015,
    ##         2016
    ##       ],
    ##       "line": [
    ##         0
    ##       ]
    ##     },
    ##     "compare": {
    ##       "resid.variance": [
    ##         2.49022310287957e+021
    ##       ],
    ##       "used.obs": [
    ##         2002,
    ##         2016,
    ##         2009,
    ##         2005.5,
    ##         2012.5
    ##       ],
    ##       "loglik": [
    ##         -1.7431561720157e+022
    ##       ],
    ##       "aic": [
    ##         3.4863123440314e+022
    ##       ],
    ##       "bic": [
    ##         3.4863123440314e+022
    ##       ],
    ##       "gcv": [
    ##         5.54416871376474e+021
    ##       ]
    ##     }
    ##   },
    ##   "model.param": {
    ##     "model": {
    ##       "arima.order": [
    ##         2,
    ##         1,
    ##         0,
    ##         0,
    ##         1,
    ##         1,
    ##         0
    ##       ],
    ##       "arima.coef": [
    ##         0.8348,
    ##         -0.249,
    ##         -0.9999
    ##       ],
    ##       "arima.coef.se": [
    ##         0.2524,
    ##         0.2482,
    ##         0.5954
    ##       ]
    ##     },
    ##     "residuals_fitted": {
    ##       "residuals": [
    ##         290501.235,
    ##         18348491.5673,
    ##         4388546947.1005,
    ##         -2696772503.6529,
    ##         12279728064.2191,
    ##         1663580465.5181,
    ##         5162045935.6711,
    ##         4109968756.8555,
    ##         6995758466.0538,
    ##         5772141452.1428,
    ##         231395392466.55,
    ##         31316282096.0982,
    ##         66705686505.6137,
    ##         -149540611131.324,
    ##         33819214996.6006
    ##       ],
    ##       "fitted": [
    ##         290210919.405,
    ##         292893799.5027,
    ##         879953753.9995,
    ##         5239660264.6629,
    ##         2524223722.4609,
    ##         14524933880.9219,
    ##         13068989880.2189,
    ##         14969572407.8245,
    ##         15742892108.9562,
    ##         19189234218.4272,
    ##         30118215224.8599,
    ##         237630120202.992,
    ##         188517130199.286,
    ##         172516674104.944,
    ##         -21767528455.4406
    ##       ],
    ##       "time": [
    ##         2002,
    ##         2003,
    ##         2004,
    ##         2005,
    ##         2006,
    ##         2007,
    ##         2008,
    ##         2009,
    ##         2010,
    ##         2011,
    ##         2012,
    ##         2013,
    ##         2014,
    ##         2015,
    ##         2016
    ##       ],
    ##       "line": [
    ##         0
    ##       ]
    ##     },
    ##     "compare": {
    ##       "resid.variance": [
    ##         7.52601888826793e+021
    ##       ],
    ##       "variance.coef": [
    ##         [
    ##           0.0637,
    ##           -0.034,
    ##           -0.0003
    ##         ],
    ##         [
    ##           -0.034,
    ##           0.0616,
    ##           -0.0002
    ##         ],
    ##         [
    ##           -0.0003,
    ##           -0.0002,
    ##           0.3545
    ##         ]
    ##       ],
    ##       "not.used.obs": [
    ##         0
    ##       ],
    ##       "used.obs": [
    ##         14
    ##       ],
    ##       "loglik": [
    ##         -371.6686
    ##       ],
    ##       "aic": [
    ##         751.3372
    ##       ],
    ##       "bic": [
    ##         753.8934
    ##       ],
    ##       "aicc": [
    ##         755.7816
    ##       ]
    ##     }
    ##   },
    ##   "forecasts": {
    ##     "ts.model": [
    ##       "ARIMA(2,1,1)"
    ##     ],
    ##     "data_year": [
    ##       2002,
    ##       2003,
    ##       2004,
    ##       2005,
    ##       2006,
    ##       2007,
    ##       2008,
    ##       2009,
    ##       2010,
    ##       2011,
    ##       2012,
    ##       2013,
    ##       2014,
    ##       2015,
    ##       2016
    ##     ],
    ##     "data": [
    ##       290501420.64,
    ##       311242291.07,
    ##       5268500701.1,
    ##       2542887761.01,
    ##       14803951786.68,
    ##       16188514346.44,
    ##       18231035815.89,
    ##       19079541164.68,
    ##       22738650575.01,
    ##       24961375670.57,
    ##       261513607691.41,
    ##       268946402299.09,
    ##       255222816704.9,
    ##       22976062973.62,
    ##       12051686541.16
    ##     ],
    ##     "predict_time": [
    ##       2017
    ##     ],
    ##     "predict_values": [
    ##       27966100694.5231
    ##     ],
    ##     "up80": [
    ##       142431305172.611
    ##     ],
    ##     "low80": [
    ##       -86499103783.5649
    ##     ],
    ##     "up95": [
    ##       203025524202.564
    ##     ],
    ##     "low95": [
    ##       -147093322813.518
    ##     ]
    ##   }
    ## }
    ##
