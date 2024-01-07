# Predicting the climate based on the concentration of carbon dioxide
<p align="center">
  <img src="https://github.com/Jko0425/Phase_5_project/blob/main/Images/Mauna%20Loa.jpg" width="1000" />
</p>

By: Joshua Ko
<br>Email: joshuawko@gmail.com
## The dangers of climate change
Climate change is a natural process that is responsible for developing the life that exists on Earth. However, there has been an acceleration of climate change due to human activity. As technology advances so does our need for electricity. Currently, most of our energy is sourced from burning fossil fuels; as a result, carbon emissions continue to rise and so does the surface temperature of the Earth. This problem is very expensive to solve, and according to the [Environmental Protection Agency](https://www.epa.gov/planandbudget/budget), their budget is around ten billion dollars with a workforce of 15000 employees. The EPA needs to allocate their budget accordingly. With the implementation of a predictive model, the EPA can use their budget efficiently and focus on areas that are more susceptible to climate change due to the cities' carbon emissions. This project aims to develop a model for the EPA that will predict the temperature and precipitation of the area depending on their carbon dioxide concentration.
## About the data
The data used to model the model was provided by the National Oceanic and Atmospheric Administration.
- [Climate data](https://www.ncei.noaa.gov/access/search/data-search/global-summary-of-the-month?pageNum=1)
- [Carbon emission data](https://gml.noaa.gov/dv/site/index.php?stacode=none)

The climate data contains many variables in the form of acronyms. 
Some are listed below:
- ADPT: Average Dew Point Temperature (celsius)
- AWND: Average Wind Speed (meters per second)
- PRCP: Total Monthly Precipitation (millimeters)
- PSUN: Monthly Average of the daily percents of possible sunshine
- TAVG: Average Monthly Temperature (celsius)
- TMAX: Monthly Maximum Temperature (celsius)
- TMIN: Monthly Minimum Temperature (celsius)
- RHAV: Relative Humidity

The carbon emission data contains the concentration of carbon dioxide in parts per million (ppm). The method of extraction involves capturing a sample of air several meters above the surface.

We will develop climate predictive models for these 8 cities/sites:
- BOULDER, CO US
- HILO INTERNATIONAL AIRPORT 87, HI US
- HOHENPEISSENBERG, GM
- CAPE FLORIDA, FL US
- LOS ANGELES DOWNTOWN USC, CA US
- SAN FRANCISCO DOWNTOWN, CA US
- VESTMANNAEYJAR, IC
- TEMPLE DRAUGHTON MIL, TX US
<br>*Carbon emission data for Hilo International Airport is taken from Mauna Loa Observatory
<br>*Carbon emission data for Temple is taken from Moody, TX

## Finding the best predictive model
We have developed two models (linear and XGBoost). A linear regression model is created by simply fitting the data after noise reduction.
<p align="center">
  <img src="https://github.com/Jko0425/Phase_5_project/blob/main/Images/Linear%20regression%20of%20average%20monthly%20temperature.png" width="600" />
</p>
<p align="center">
  <img src="https://github.com/Jko0425/Phase_5_project/blob/main/Images/Linear%20regression%20of%20total%20monthly%20precipitation.png" width="600" />
</p>
The best XGBoost algorithm, on the other hand, is found by running a GridSearchCV. The parameters include:

- objective: linear, squarederror
- learning_rate: 0.1, 0.05, 0.01, 0.005, 0.001
- alpha: 0, 1, 2
- max_depth: 5, 6, 7
- n_estimators: 500, 1000
<p align="center">
  <img src="https://github.com/Jko0425/Phase_5_project/blob/main/Images/XGBoost%20temperature%20prediction.png" width="600" />
</p>
<p align="center">
  <img src="https://github.com/Jko0425/Phase_5_project/blob/main/Images/XGBoost%20precipitation%20prediction.png" width="600" />
</p>

## Comparing the metrics of both models
<br> __Temperature__
|Site|Linear MSE|XGBoost MSE|
|----:|------------|-------|
|Boulder, CO | 0.0884 | 0.0939 |
|Hilo International, HI | 0.0168 | 0.0124 |
|Hohenpeissenberg, GM | 0.0642 | 0.0624|
|Cape Florida, FL | 0.0316 |0.0297|
|Los Angeles, CA | 0.0364 |0.0424|
|San Francisco, CA |	0.0249 |	0.0254|
|Vestmannaeyjar, IC |	0.0359 |	0.04|
|Temple, TX | 0.0742 | 0.0894|

<br> __Precipitation__
|Site|Linear MSE|XGBoost MSE|
|----:|------------|-------|
|Boulder, CO	|0.7101	|0.6511|
|Hilo International, HI	|1.8941|	1.4465|
|Hohenpeissenberg, GM	|0.898|	0.875|
|Cape Florida, FL	|1.3351	|1.2637|
|Los Angeles, CA	|1.173	|1.1681|
|San Francisco, CA	|1.4654	|1.3976|
|Vestmannaeyjar, IC	|0.678	|0.6798|
|Temple, TX	|1.0595	|0.8553|

The XGBoost performed the best when predicting both temperature and precipitation. 
