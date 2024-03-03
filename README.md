# Predicting the climate based on the concentration of carbon dioxide
<p align="center">
  <img src="https://github.com/Jko0425/Phase_5_project/blob/main/Images/Mauna%20Loa.jpg" width="1000" />
</p>

By: Joshua Ko
<br>Email: joshuawko@gmail.com
## Table of Contents
* [The dangers of climate change](https://github.com/Jko0425/Phase_5_project?tab=readme-ov-file#the-dangers-of-climate-change)
* [About the data](https://github.com/Jko0425/Phase_5_project?tab=readme-ov-file#about-the-data)
* [Finding the best predictive model](https://github.com/Jko0425/Phase_5_project?tab=readme-ov-file#finding-the-best-predictive-model)
* [Comparing the metrics of both models](https://github.com/Jko0425/Phase_5_project?tab=readme-ov-file#comparing-the-metrics-of-both-models)
* [Conclusion](https://github.com/Jko0425/Phase_5_project?tab=readme-ov-file#conclusion)
## The dangers of climate change
Climate change is a natural process that is responsible for developing the life that exists on Earth. However, there has been an acceleration of climate change due to human activity. As technology advances so does our need for electricity. Currently, most of our energy is sourced from burning fossil fuels; as a result, carbon emissions continue to rise and so does the surface temperature of the Earth. This problem is very expensive to solve, and according to the [Environmental Protection Agency](https://www.epa.gov/planandbudget/budget), their budget is around ten billion dollars with a workforce of 15000 employees. The EPA needs to allocate their budget accordingly. With the implementation of a predictive model, the EPA can use their budget efficiently and focus on areas that are more susceptible to climate change due to the cities' carbon emissions. This project aims to develop a model for the EPA that will predict the temperature and precipitation of the area depending on their greenhouse gas concentration.
## About the data
The data used to model the model was provided by the National Oceanic and Atmospheric Administration.
- [Climate data](https://www.ncei.noaa.gov/access/search/data-search/global-summary-of-the-month?pageNum=1)
- [Greenhouse gas emission data](https://gml.noaa.gov/dv/site/index.php?stacode=none)

These are time series data that may contain noise. [Mauna Loa Observatory](https://gml.noaa.gov/obop/mlo/aboutus/aboutus.html), which provided the carbon emission data for Hilo International Airport, is located near an active volcano. This may lead to spiked levels of carbon dioxide concentration. We can reduce the noise for both climate and carbon emission data by calculating the rolling mean.

The climate data contains many variables in the form of acronyms listed below. Some sites do not contain any values for some of these variables. Therefore we only focus on "Average Monthly Temperature" and "Total Monthly Precipitation".
Some variables are listed below:
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
<br>*Emission data for Hilo International Airport is taken from Mauna Loa Observatory
<br>*Emission data for Temple is taken from Moody, TX

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

The XGBoost performed the best when predicting both temperature and precipitation. However, precipitation may be more challenging to predict than temperature. According to [this article](https://www.downtoearth.org.in/news/climate-change/rising-co2-can-lead-to-drier-amazon-and-bring-more-rain-in-african-and-pacific-forests-60682#:~:text=Scientists%20have%20discovered%20another%20factor,in%20African%20and%20Indonesian%20forests.), the rise of carbon dioxide in the Amazon leads to more rainfall in African and Pacific forests due to trade winds. This may explain the higher mean squared error for both linear and XGBoost models.

## Conclusion
We recommend that the EPA use the XGBoost model to predict the temperature and precipitation. They can mainly focus on these cities:
- Hilo Internation Airport
- Cape Florida
- Vestmannaeyjar
- Boulder (rise in precipitation)

With the EPA's limited budget, they can use the model to focus on cities that are vulnerable to climate change.
__Limitations__
- Weak operating system. A powerful computer may be able to handle more parameters for the grid search
- Lack of data. Some sites/cities are missing values, limiting our sample size

__Next steps__
- Repeat the process with other greenhouse gases (Use XGBoost feature importance to determine which greenhouse gas is most influencial)
- Consider other elements of climate (cloud coverage, relative humidity)
- Look at how climate change is affecting certain ecosystems (marine, forests)
## Repository Structure
```bash
Phase_5_project/
├─ CH4_data/
│  ├─ Boulder Methane.csv
│  ├─ Hohenpeissenberg Methane.csv
│  ├─ Iceland Methane.csv
│  ├─ Key Methane.csv
│  ├─ Los Angeles Methane.csv
│  ├─ Moody Methane.csv
│  ├─ Mouna Loa Methane.csv
│  ├─ San Francisco Methane.csv
├─ CO2_data/
│  ├─ Boulder.csv
│  ├─ Hohenpeissenberg.csv
│  ├─ Iceland.csv
│  ├─ Key Biscayne.csv
│  ├─ Los Angeles.csv
│  ├─ Moody.csv
│  ├─ Mouna Loa.csv
│  ├─ San Francisco.csv
├─ Climate_data/
│  ├─ boulder.csv
│  ├─ hilo.csv
│  ├─ hohenpeissenberg.csv
│  ├─ iceland.csv
│  ├─ key_biscayne.csv
│  ├─ los_angeles.csv
│  ├─ san_francisco.csv
│  ├─ temple.csv
├─ Images/
│  ├─ Linear regression of average monthly temperature.png
│  ├─ Linear regression of total monthly precipitation.png
│  ├─ Mauna Loa.png
│  ├─ XGBoost precipitation prediction.png
│  ├─ XGBoost temperature prediction.png
├─ N2O_data/
│  ├─ Boulder N2O.csv
│  ├─ Hohenpeissenberg N2O.csv
│  ├─ Iceland N2O.csv
│  ├─ Key N2O.csv
│  ├─ Los Angeles N2O.csv
│  ├─ Moody N2O.csv
│  ├─ Mouna Loa N2O.csv
│  ├─ San Francisco N2O.csv
├─ SF6_data/
│  ├─ Boulder SF6.csv
│  ├─ Hohenpeissenberg SF6.csv
│  ├─ Iceland SF6.csv
│  ├─ Key SF6.csv
│  ├─ Los Angeles SF6.csv
│  ├─ Moody SF6.csv
│  ├─ Mouna Loa SF6.csv
│  ├─ San Francisco SF6.csv
├─ .gitignore
├─ EDA.ipynb
├─ Final.ipynb
├─ Models.ipynb
├─ README.md
├─ presentation.pdf
```
