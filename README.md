---
# **TempCast: A Machine Learning Approach to Weather Prediction in Flint Michigan**
---
## **Table of Contents**
---


- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning](#data-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [References](#references)


---
### Project Overview
---


This project explores time series forecasting by leveraging machine learning to predict the next day’s maximum temperature from historical weather data. The project begins by ingesting a multi-decade dataset and performing thorough cleaning, including handling missing values through forward filling and column-specific imputation, and converting date indices into proper datetime objects to enable effective time-based analyses. This foundational work ensures that the dataset is robust and reliable for subsequent modeling.

Once the data is cleaned, the focus shifts to feature engineering and model development. In addition to including standard meteorological variables such as precipitation, snowfall, snow depth, and daily maximum and minimum temperatures, the project creates advanced features like a 30-day rolling average of maximum temperature and derived ratios that encapsulate seasonal trends. These engineered features capture both short-term and longer-term weather patterns, providing the model with a richer context. A Ridge Regression model, known for its ability to mitigate multicollinearity through L2 regularization, is then trained on this enhanced dataset using a thoughtful time-based train-test split.

Model evaluation is conducted using both numerical metrics and visualizations. The model achieves an R² score of approximately 0.845, indicating that over 84% of the variance in maximum temperature is explained by the predictors, alongside an RMSE of around 7.42, which quantifies the typical prediction error. Comprehensive plots, including actual versus predicted temperature graphs and detailed residual analyses, offer insightful diagnostics into model behavior and pinpoint opportunities for further improvement. Overall, the project not only exemplifies a complete end-to-end machine learning workflow—from data cleaning and feature engineering to model training and evaluation—but also lays a solid foundation for future explorations in weather prediction.

![Line Graph](https://github.com/user-attachments/assets/1fa6dc6d-f1db-49ed-9bcc-04534f3d3dc9)

![Histogram Graph](https://github.com/user-attachments/assets/6bad0e5f-ff6e-4c00-a1c1-0465fcb3a3c0)

![Scatter Plot Graph](https://github.com/user-attachments/assets/5c545b83-23a8-4293-ad70-4a863ca15b45)


---
### Data Sources
---


All the weather data used in the Flint Weather Predictor project was sourced directly from NOAA’s National Centers for Environmental Information (NCEI). NOAA’s NCEI is a premier repository for historical weather records in the United States, and its comprehensive datasets have been instrumental in various research and forecasting applications.

**Dataset Details:**
- ***Source***: NOAA’s National Centers for Environmental Information (NCEI Website)

- ***Data Coverage***: Historical records spanning from 1960 to the present

- ***Location Focus***: Measurements and observations specific to Flint, Michigan

- ***Data Format***: CSV files following standardized formats (similar to those used in the Global Historical Climatology Network or Integrated Surface Data datasets)

- ***Key Variables***: The dataset includes various meteorological variables such as temperature, wind speed, precipitation, and other weather-related metrics that are critical for building predictive models.

**Rationale for Data Selection:**

The decision to utilize NOAA’s NCEI data was driven by its credibility, consistency, and long-term record-keeping. By leveraging over six decades of weather data, the project is able to analyze seasonal patterns and long-term climate trends, providing a robust foundation for accurate weather predictions in Flint, MI.

**Usage Considerations:**
- ***Data Quality***: NOAA’s rigorous data collection and quality control processes ensure that the records are both reliable and precise.

- ***Licensing***: The data is publicly available, making it ideal for academic and research purposes. Users are encouraged to review NOAA’s terms of use on the NCEI website.

- ***Integration***: The standardized format of the dataset allows for seamless integration with Python libraries such as pandas, numpy, and scikit-learn, which were extensively used throughout this project.

The dataset is publicly available under NOAA's NCEI open data policy, promoting widespread use and dissemination for educational and research purposes. Users can access, download, and employ the data freely.

For more detailed information, metadata definitions, and to explore additional resources, please visit the official dataset page: [***NOAA's NCEI***](https://www.ncei.noaa.gov/?form=MG0AV3).


---
### Tools
---


- ***Visual Studio Code*** – The IDE where you ran your Jupyter Notebooks.

- ***Jupyter Notebook*** – Interactive development environment for exploratory analysis.
    
- ***Python*** – The primary programming language.

- ***Pandas*** – For data ingestion, manipulation, and cleaning.

- ***NumPy*** – For numerical computations.

- ***Scikit-learn*** – For building, training, and evaluating the Ridge Regression model.

- ***Matplotlib*** – For data visualization and plotting.


---
### Data Cleaning
---


The data cleaning process begins with importing the raw weather dataset from a CSV file, where the DATE column serves as the index. The initial step involves an exploratory analysis to understand data quality. We use Pandas to compute the fraction of missing values across each feature, which revealed only very small proportions of missing data. Recognizing the significance of ensuring data consistency, especially in a time series context, we immediately address these gaps—specifically filling the missing values in the snow and precip columns with 0, which reflects the assumption that missing entries in those columns likely indicate no measurable snowfall or precipitation.

After addressing the major missing values, additional cleaning is performed by applying forward filling (ffill) across the dataset. This technique propagates the last valid observation forward to fill any remaining gaps, thereby preserving the temporal structure of the data while ensuring that no NaN values remain. In tandem with these steps, the index is converted into a datetime format. This conversion not only assures a consistent time series format but also enables efficient time-based slicing and aggregation for further analysis. A further inspection is made to count occurrences of sentinel values (such as 9999), often used to denote erroneous or missing data, ensuring that such anomalies do not interfere with downstream processing.

By rigorously handling missing values and converting date indices appropriately, the dataset is transformed into a robust foundation for both feature engineering and model training. This meticulous cleaning process ensures that subsequent processes—such as generating rolling averages, engineered ratio features, and model fitting—proceed with a dataset that is both reliable and optimally structured for accurate time series forecasting.


---
### Exploratory Data Analysis
---


Once the data was cleaned and prepared, the next step was to perform exploratory data analysis to better understand the underlying patterns, trends, and relationships within the dataset. Initially, descriptive statistics and summary methods were employed to gain insights into the distribution of key weather variables such as precipitation, snowfall, snow depth, and temperature extremes. This phase allowed us to identify any anomalies or outliers in the data and assess its overall quality, setting the stage for more focused analyses.

Visualization was a cornerstone of the EDA process. Time series plots were generated for the maximum and minimum temperatures to capture seasonal trends and variations over multiple decades. A dedicated plot for precipitation was also created, both as a continuous time series and aggregated on a yearly basis to observe long-term patterns in rainfall. These visualizations not only offered a clear picture of the temporal dynamics present in the data but also highlighted periodic fluctuations and potential shifts in weather patterns—insights that were essential for informed feature engineering.

Beyond simple plots, the exploratory phase included a deep dive into the relationships between variables. By overlaying multiple variables, such as plotting actual versus predicted temperatures and examining their residuals, the analysis revealed important cues about the performance of preliminary models and the need for advanced feature engineering. The identification of these relationships, along with patterns uncovered through visualization, directly informed the subsequent steps in model development and calibration, ensuring a well-rounded approach to forecasting future temperatures.


---
### Data Analysis
---

![ML - Flint - Weather Code Snip 1](https://github.com/user-attachments/assets/887371e1-af3c-493b-a4f4-e7d18636f2b1)

![ML- Flint - Weather Code Snip 2](https://github.com/user-attachments/assets/85040a16-e230-48e8-9d58-150824c504a6)

![ML- Flint - Weather Code Snip 3](https://github.com/user-attachments/assets/27072fbd-fb7b-4ee9-b260-0b456268620d)


---
### Results
---


The project yielded promising outcomes in forecasting the next-day maximum temperature using a robust Ridge Regression model enhanced with both raw and engineered features. The model achieved an R² score of approximately 0.8454, meaning that about 84.5% of the variance in maximum temperature is explained by the predictors. Additionally, the RMSE of roughly 7.42 indicates that the average deviation of the model's predictions from the actual temperatures is 7.42 units. These metrics reflect a strong predictive capability given the inherent variability in weather data, underscoring the effectiveness of the data cleaning, feature engineering, and modeling approach employed.

Visual diagnostic tools further confirm these findings. Time series plots comparing actual versus predicted maximum temperatures display a close tracking of the overall trend and seasonal patterns present in the historical data. Moreover, the residual analysis reveals that the differences between predicted and actual values are approximately symmetrically distributed around zero, with no obvious systematic bias over time. This behavior suggests that the model's errors are random rather than influenced by specific time periods or external factors, which lends additional credibility to the model's reliability.

Overall, the results demonstrate that the integrated workflow—from rigorous data preparation and innovative feature engineering to model training and comprehensive evaluation—provides a compelling solution for short-term weather prediction. While the current performance is strong, these findings also lay the groundwork for additional refinements, such as incorporating further lag-based or cyclic features and experimenting with alternative model architectures, to push the predictive boundaries even further.


---
### Recommendations
---

While the current model demonstrates strong performance, there are several opportunities for further improvement. One key recommendation is to enhance feature engineering by incorporating additional lag-based features, cyclical components (such as sinusoidal transformations of time variables), and external meteorological data. These improvements could capture underlying seasonal patterns and temporal dependencies more effectively. Moreover, exploring interactions between features or applying transformations to better normalize skewed distributions may further boost predictive accuracy.

Another area for advancement involves model tuning and experimentation with alternative approaches. Although Ridge Regression has delivered promising results, future work should consider conducting a thorough hyperparameter optimization, perhaps using techniques like GridSearchCV in combination with time series cross-validation. Additionally, experimenting with non-linear models—such as Random Forests, Gradient Boosting Machines, or even deep learning architectures like LSTM networks—might capture complex patterns not fully addressed by linear methods, ultimately leading to improved forecast precision.

Finally, it is advisable to integrate more rigorous evaluation and monitoring frameworks. This includes not only leveraging additional error metrics and diagnostic plots but also establishing a systematic backtesting pipeline to assess model stability over different time windows. Engaging with domain experts to validate model insights and ensuring the reproducibility of experiments will help maintain and enhance the quality of the predictions as new data becomes available. Each of these recommendations forms a pathway for iteratively improving the model and advancing the project toward more sophisticated and reliable weather forecasting.


---
### Limitations
---


While this project employs a robust workflow for forecasting, several limitations remain that warrant consideration. First, the model's performance is inherently tied to the quality of the historical weather data. Measurement errors, biases, or residual missing values—even after thorough cleaning and imputation—can propagate through the analysis, subtly affecting both the predictive accuracy and the reliability of the forecasts.

Another significant limitation is the assumption of linearity and stationarity within the weather dynamics. Although the use of Ridge Regression with engineered features (such as rolling averages and ratio calculations) captures many underlying trends, linear models may not fully account for the non-linear and evolving nature of weather patterns. Seasonal variations, sudden climatic shifts, and complex interactions between variables could be better addressed by more sophisticated, non-linear approaches or models specifically tailored for time series data.

Finally, the evaluation of the model is based on a single train-test split, which might not fully capture variability across different time periods. The reliance on a fixed temporal split limits the ability to assess how the model might perform under different conditions or over longer forecasting horizons. Future work incorporating more rigorous, time series-specific cross-validation methods would provide a more comprehensive understanding of the model's stability and predictive power over time.


---
### References
---


- [***Visual Studio Code (VS Code):***](https://code.visualstudio.com/) IDE used with the Jupyter Notebook extensions for interactive analysis.

- [***Jupyter Notebook:***](https://jupyter.org/) Interactive computing environment that facilitated exploratory data analysis.

- [***Python:***](https://www.python.org/) The programming language used for this project.

- [***Yahoo Finance:***](https://finance.yahoo.com/) Data source for historical market data.

- [***yfinance:***](https://github.com/ranaroussi/yfinance) Python library for retrieving Yahoo Finance data.

- [***pandas:***](https://pandas.pydata.org/) Library for data manipulation and analysis.

- [***numpy:***](https://numpy.org/) Library for numerical computations.

- [***scikit-learn:***](https://scikit-learn.org/) Machine learning library used for building the models and evaluating performance.

- [***NOAA's NCEI***](https://www.ncei.noaa.gov/?form=MG0AV3)

