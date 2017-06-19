---
layout: post
title:  Forecasting Greece's GDP for 2017
Categories: Technical
comments: true
tags: [Time Series Analysis, Forecasting, Machine Learning]
---

During this semester I took a class on Forecasting to get a better understanding of how to do time series analysis and better grasp forecasting methodologies. For the final project the goal was to pick a country and forecast its GDP for 2017. I picked Greece because it seemed an interesting country for this type of project given its recent history. The reasons behind it are beyond the scope of this post and the project, but it will suffice to say that Greece hasn't exactly been the most stable of economies, and that lack of stability was what drew me to choose it. 

# Data

The data used in this project was retrieved from the *GDP and main components (output, expenditure and income)* dataset available from EUROSTAT. The dataset created includes data related to Greece's Real GDP, measured in *Chain Linked Volumes (2010), million euro* and isn't seasonally or calendar adjusted. Data related to government expenditure, household expenditure, imports, exports, and investment levels was also extracted. 

# Graphical Exploratory Analysis

We'll start by looking at the data that we got:

![realgdp]({{site.url}}/assets/forecastgreece/realgdp.png)

It's obvious that by around 2009 Greece's Real GDP started experiencing a downfall that seems to have petered out by 2012 and has largely stayed constant since. We could decompose this time series into a trend and a seasonal component using STL decomposition, or even applying a Hodrick-Prescott filter, but I don't think it would give us more information that we already get by just looking at the plot above.

A good starting point for a forecasting project is to transform the data by applying a Box-Cox transformation to stabilize the seasonal variation. A Box-Cox transformation is a class of transformations that is defined by:

$$
\left\{\begin{matrix}
w_t = \ln\left(y_t \right )  &  \text{if}\;  \lambda = 0\\ 
w_t = \frac{y_t^\lambda - 1}{\lambda} & \text{otherwise}
\end{matrix}\right.
$$

where lambda is a parameter that needs to be estimated. We use the function already provided by the *forecast* package for this purpose:

```{r}
lambda <- BoxCox.lambda(realgdp)
gdp_boxcox <- BoxCox(realgdp,lambda) 
```

After transforming the data, we get the following:

![realgdp]({{site.url}}/assets/forecastgreece/realgdp_boxcox.png)

The very thing that made Greece such an enticing target for this project also makes it challenging for our forecast process. Because Greece's recent economic history is so tumultuous, it we were to use a method that includes all the temporal data that we have we would be fitting a model to information that is no longer relevant to us. This means we need to select a time interval that provides only the information that is relevant and exclude that which isn't, not only because Greece's economic fundamentals have changed but because including that information might actually damage the model's performace. 

A way to go about selecting which data to maintain and which to throw away would just to look at the plot of Greece's Real GDP and eyeball it. I don't have anything against that in this particular case because it seems to me you can identify the three phases the Real GDP goes through by just looking at it. However, because my main goal with this project is for me to **learn**, so I decided to use an R package that provides functions that identify structural breaks in the data programatically.

To go about estimating where the stuctural breaks happen I used the *breakpoints* function provided by the *strucchange* package, available from CRAN, which implements the algorithm detailed in <cite paper here>. Again, I am not sure whether this approach is superior to just eyeballing it, but at least now I know how to use this package.

![realgdp]({{site.url}}/assets/forecastgreece/structural.png)

Okay so now we know the time interval we will be using: 2011Q3 onwards. Before I proceed to throwing some models onto the data however, I still need to make one last transfomation to the data because my goal is to forecast *growth rates*, not the actual Real GDP. This is fairly simple.

![realgdp]({{site.url}}/assets/forecastgreece/realgdp_growthrate.png)

# Model Evaluation

There are plenty of different models we could use but how do we go about selecting the *best* model? We need a way to select the best model from all models that we'll be using, and this selection needs to be based on the goals of the project. I am not quite confident my approach here is 100% valid, but for pragmatic purposes I don't think it's that bad. The idea is that we'll will be calculating the RMSE and MAE of each model's out of sample performace, and then select that which minimizes both variables. It seems to me that it would be hard for a model to not minimize both variables but perform consistently better than one who does. 

# Methods

## Exponential Smoothing

Exponential Smoothing methods are fairly standard forecasting tools. If we consider different combinations of the trend and seasonal components of a time series, we can work out fifteen exponential smoothing models that we can use. If we take into account that each of these can be further subdivided between a version with an additive error component and another with a multiplicative one, we end up with 30 models in total to consider.

To calculate the out of sample RMSE and MAE for each model I use a cross validation setting with a forecasting horizon of h=4, or 4 quarters, and this setting will be used for all models that allow for a cross validation calculation of error measures.

The six models with the best performance, given by how low their RMSE and MAE values are, are as follows:

 |Model   |RMSE     |MAE|
 |-------| --------| --------|
  |ANA     |0.0480   |0.0275|
  |AAA     |0.0531   |0.0322|
  |ANN     |0.0707   |0.0611|
  |AAN     |0.0712   |0.0580|
  |ANM     |0.0838   |0.0599|
  |AAM     |0.038    |0.0599|
  

From this table we can see that a Holt's Linear Method, correponding to an additive trend component, no seasonal component, and an additive error component (hence ANA), provides us with the lowest RMSE and MAE of the bunch.

### Bagged ETS

Bagged ETS is an approach detailed in <<paper>>. The idea is to decompose the time series into a trend, seasonal, and error component, bootstrapping the error component, adding back in the trend, seasonal, and the bunch of artificial error components you get from the bootstrap, and applying an ETS model to each individual time series. After getting the forecast for all of them, you calculate its mean and that's the end forecast result of the algorithm. One issue from this approach is that I can't use cross validation to calculate the RMSE and MAE that I want, so I ended up restricting the dataset to include 8 pseudo-out of sample periods to calculate the RMSE and MAE on those.

![realgdp]({{site.url}}/assets/forecastgreece/bagged_outofsample.png)

|RMSE     |MAE|
|-------| --------|
|0.0122 |0.0141|
 
While the MAE and RMSE error measures differ in how they're computed, we can see that this approach has a good forecasting performace. 

## ARIMA

ARIMA models are one other class of standard models known to everyone who's done time series analysis. The idea is the same from the exponential smoothing section: I'll calculate the out of sample, cross validated, out of sample RMSE and MAE for a bunch of models and select the one that minimizes both.

Because we're dealing with data with seasonal variation, I'll be using a seasonal ARIMA model. These models are specificed using 6 parameters, so I need to decide the range of values these can take. In the end I ended up restricting the non-seasonal parameters to [0,3] and the seasonal parameters to [0,2] for entirely pragmatic reasons. These intervals provided a good sample of possible ARIMA models, 1728 of them, while not being too time consuming to calculate.

The four models with the best performance are as follows:


 | Model                | MAE     | RMSE    |
 | ---------------------| --------| --------|
 | ARIMA(3,0,0)(2,1,1)  | 0,0022  |0,0022   |
 | ARIMA(3,3,3)(1,1,0)  | 0,0038  | 0,0036  |
 | ARIMA(2,1,0)(2,1,1)  | 0,0050  | 0,0050  |


As is easily seen, the model (3,0,0)(2,1,1) is the best performant of the bunch. Its residual diagnostics also seem very good, with the residuals not being autocorrelated nor biased (and following a normal distribution thus passing the Ljung-Box test).

![realgdp]({{site.url}}/assets/forecastgreece/arima_diagnostics.png)

# Regression Analysis

Let's say we're at time \\(t\\). If we're forecasting something, it means we're trying to estimate some future values, at time \\(t+1\\). In the context of regression analysis, this means that we won't have the values for the independent variables for time \\(t+q\\) at time \\(t\\), that is, future values are only available in the future, which means we need to use the lag of the independent variables. I decided to use a lag of 1, which basically means that I will be estimating the Real GDP at time \\(t+1\\) using the value of the variables at time \\(t\\). 

I'll cut to the chase: I tried using multiple linear regression, along with ridge and lasso regression just to see if their out of sample performance would be better than the ARIMA one. It wasn't, by a long shot. I'll abstain from going through the results here because they're not that interesting.

# Forecast

So, it seems the \\(ARIMA(3,0,0)(2,1,1)\\) wins as it obtains the lowest RMSE and MAE of all models here used. Now our task is to use it to forecast the Real GDP values for all 4 quarters of 2017.

![realgdp]({{site.url}}/assets/forecastgreece/arima.png)

The image above is what applying the ARIMA model to the data and setting the forecast horizon for \\(h=4\\) gets you, the estimated values and their corresponding confidence intervals. Because we're forecasting growth rates, that's what the model gives you back, but it would be interesting to see what it translates to in actual Real GDP values. To do this its just a matter of transforming the growth rates back into actual values, and, since the growth rates come from a time series that's been transformed with a Box-Cox transformation, we need to do the reverse of that transformation. This is what we get in the end:

![realgdp]({{site.url}}/assets/forecastgreece/gdp_forecast.png)

With the following predicted values:


  |           | Real GDP|
  |---------  |----------|
  |  2017 Q1  | 42827.88|
  |  2017 Q2  | 46027.45|
  |  2017 Q3  | 48243.45|
  |  2017 Q4  | 44920.62|


Since the provisional data for the 1st quarter of 2017 is 42827.3, we can be optimistic that our model actually does provide us with good forecasts for Greece's Real GDP. It is entirely possible that this is a fluke, or good fortune, so I will update it further as data for the following quarters are released to see if the model's good performance holds up.
# Conclusion

This was my first foray into time series analysis/forecasting, and I enjoyed it more than I thought I would. To be sure, there's bound to be some errors here that I didn't catch, some intricacie of the forecasting process that I have yet to learn. If you know what that is, please do tell as I want to get better at this.

Still, given the results I got, I would say this project was a success. 

