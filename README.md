# Impact of Weather Conditions on Household Electricity Consumption
## Overview

This repository contains the code and models developed for my dissertation on the "Impact of Weather Conditions on Household Electricity Consumption." The project leverages a Gated Recurrent Unit (GRU) neural network to predict household electricity consumption based on various weather conditions, such as temperature, humidity, and wind speed.

## Tools

Ensure you have Python 3.x and the following packages installed:

TensorFlow/Keras

NumPy

Pandas

Scikit-learn

Matplotlib

Seaborn

## Data Collection and Preprocessing

The dataset used in this study comprises of The London Smart Meter dataset, collected by the UK Power Networks for the Low Carbon London project, Weather data was  from the European Climate Assessment (ECA) and Meteostat online portals. The London Heathrow airport station data obtained from ECA contained daily temperature, humidity, cloud cover, precipitation, sea-level pressure, global radiation, sunshine hours, and snow depth information from 1979 to 2012 while the data from Meteostat weather contained daily minimum/maximum temperature, wind speed, wind direction, and air pressure from 2012 to 2014.
Additionally, Holiday data was collected from the UK Debt Management Office, covering holiday days from 1998 to 2110.

Key preprocessing steps include:

**Handling missing data**: All datapoints in the dataset was clean except wind speed and wind direction. Linear interpolation was used for wind speed on the assumption that wind speed is expected to change smoothly over time. while forward fill and back fill was used for wind direction assuming that wind direction remains relatively constant over time.

**Feature scaling**: Min-Max scaling was used to normalize the data for better model performance.

**Sequence creation**: The data was segmented into sequences to capture temporal dependencies, essential for GRU modeling.

## Exploratory Data Analysis (EDA)

The relationship between all features in the dataset was investigated as seen in Fig IV. Just as observed in previous studies, across the years, Temperature’s U-shaped and inverse relationship with energy consumption is quite conspicuous which the degree days detrends in Fig. V. This is as result of households utilising heating and cooling systems to maintain a comfortable temperature (Emenekwe and Emodi, 2022). Cloud Cover, Air Pressure (sea level), Sunshine (hours), Wind speed, Wind direction and Global Radiation shows similar trend across the years but not so obvious. This is an indication of their multicollinearity with Temperature since they seem to be intertwined.  However, Humidity shows a direct relationship while Precipitation shows no visible relationship with household energy consumption. These relationships will be empirically proven with correlation analysis and multicollinearity tests to select features for forecasting.

**Correlation Analysis**
A correlation matrix was computed to identify the relationships between weather variables and electricity consumption. This analysis helped in understanding which weather factors have the strongest influence on electricity usage.

**Multicollinearity Checks**
Multicollinearity among features was assessed using the Variance Inflation Factor (VIF) to ensure that the input features were not highly correlated, which could adversely affect the model's performance.

**Autocorrelation Analysis**
The appropriate sequence length for the GRU model was determined by ACF plots.

## Modeling with GRU
**Model Architecture**
The GRU model was designed using the Keras Sequential API. It consists of a single layer configured to accept the input shape, allowing the model to process sequences of weather data to predict the electricity consumption. This approach was taken due to the size of the dataset used, to avoid it being too complex for the task which may likely lead to poor results. 

The tanh activation function was applied within the GRU units to help the model adapt to non-linear relationships that may likely exist between the features and the target variable.

To prevent overfitting, a Dropout layer with a rate of 0.1 was added after the GRU layer. 

A single Dense layer was used as the output layer, producing a scalar value representing the predicted electricity consumption.

**Training and Evaluation**
The model was trained using a time series dataset split into training, validation and testing sets over three different time horizons. Evaluation metrics such as MMean Squared Error (MSE), Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), Mean Absolute Percentage Error (MAPE) and Coefficient of Determination (R²) were used to assess the model's performance.

**Feature Importance**
Saliency Maps was used to determine feature importance across time sets

## Results and Discussion
The GRU model demonstrated a strong ability to predict household electricity consumption based on weather conditions. The results showed that temperature have the most significant impact on electricity usage. The model's predictions were evaluated against actual consumption data, and the findings were discussed in the context of potential applications in energy management and policy-making.

## Conclusion
This study successfully demonstrated the utility of GRU models in forecasting electricity consumption based on weather conditions. The findings highlight the importance of considering weather variables in electricity demand forecasting and provide a foundation for future research in this area.
