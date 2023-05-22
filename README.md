# Forecasting-Project
Methods used: R programming language, fpp2 package, linear regression, exponential smoothing, ARIMA models, and forecasting off a training set
## Introduction
This project is composed of two parts, one where we are working with a non-seasonal time series and one when we are working with a seasonal time series. My main adjective was to find a forecasting method that has good accuracy in predicting future trends. The steps I used to do this is as follows:
1. Use decomposition to better understand the time series
2. Create different linear regression methods and checking residuals to see which one worked the best
3. Create different exponential smoothing methods and checking residuals to see which one worked the best
4. Create different ARIMA models and find whichever model has the lowest AICc value to select the best
5. Split the time series into training and test sets. We then fit the best of each method to the training set and check the accuracy on the test set to find the best overall method

## Non-Seasonal Time Series
This time series is of birthrates per 1000 adults over through 1960-2020. 

The first step is to use linear regression in fitting a model. We created a 1st degree polynomial to a 4th degree polynomial as well as creating a smoothing spline. We then plot them side by side and check the residuals. We find that the smoothing spline is by the far the best due to its residuals being the lowest.

Next we want to create an exponential smoothing algorithm. Since we are working with non seasonal data, we use simple exponential smoothing (SES) to forecast the time series. We got a alpha value of .999 meaning there is no trend to pick up on, so the most recent observation is the best estimate.

Lastly we create ARIMA models. We use the ndiffs() function and find there is 1 level of seasonal differencing. After fitting all of the models and checking the AICc values, model 4 did the best which is ARIMA(1, 1, 0).

Now that we have the 3 best models, we then fit them to the training set for the time series. After forecasting these alongside the test set, we find that the ARIMA model performed the best based on it having the lowest RMSE, MAE, MAPE, and MASE values.

![image](https://github.com/SamWeller3/Forecasting-Project/assets/123184681/c871e1b8-3140-4aff-87b4-df02304afb19)

![image](https://github.com/SamWeller3/Forecasting-Project/assets/123184681/b6fc0698-68b2-4661-aaad-b713b17830f2)

## Seasonal Data
This time series is of U.S. GPP through 1990-2022

The first thing I did was to use multiplicative decomposition (due to the seasonal differences over time) to look at the trend, seasonality, and remainder of the time series. I used a lag value of 24 and for the most part, didn't find any large residuals.

I then created 4 different polynomial models, as well as a smoothing spline and fourier fits. After checking the residuals on all of these models I found that the 4th degree polynomial was the best predictor.

After that I moved onto exponential smoothing methods. I created a simple exponential smoothing (SES), Holt method, Holt-Winters additive method, and Holt-Winters multiplicative method. After checking the residuals, Holt-Winters multiplicative method worked the best which makes sense because the time series has clear trend and seasonality, and the magnitude of the seasonality fluctuates over time.

For ARIMA models, I found that there is 1 level of normal differencing and 1 level of seasonal differencing needed. I checked the ACF and PACF plots and found that (0, 1, 1)(0, 1, 1) and (1, 1, 0)(3, 1, 0) would be the best combinations. I created variances of those and had 27 different ARIMA models. I checked the AICc values and model 9 or (0,1,0)(1,1,2) was the best overall ARIMA model.

I then fit these four methods based on the training set and compared it to the test set. I found that the 4th degree polynomial did the best forecast because it had the lowest RMSE, MAE, MAPE, and MASE values.

![image](https://github.com/SamWeller3/Forecasting-Project/assets/123184681/69fe2ab8-3552-4031-97ec-912b11baca89)

![image](https://github.com/SamWeller3/Forecasting-Project/assets/123184681/c42c02de-f30b-4223-8ddf-4c24b1814e02)

