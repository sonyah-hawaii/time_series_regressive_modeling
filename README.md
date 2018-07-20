# READ ME
## Data Sources:
- [EnerData Global Statistical Yearbook](https://yearbook.enerdata.net/)
- [World Bank (CO2 Emissions)](https://data.worldbank.org/indicator/EN.CO2.ETOT.ZS)
- [World Bank (GDP Per Capita](https://data.worldbank.org/indicator/NY.GDP.PCAP.CD)
- [World Intellectual Property Organization](http://www.wipo.int/econ_stat/en/economics/research/)


## Table of Contents
1. [Data cleaning & target development](https://github.com/sonyah-hawaii/time_series_regressive_modeling/blob/master/Cleaning%20%26%20Abatement%20Calculations.ipynb)       
_This notebook details the steps to calculate units of CO2 Abated annually. A full list of countries included in the dataset can be found here_
- [Developing profiles with K-Means clustering](https://github.com/sonyah-hawaii/time_series_regressive_modeling/blob/master/clustering.ipynb)  
_This notebook generates yoy change using `.diff` and passes that information through K-Means, using the resulting labels to develop cohorts for modeling._
- [Variance Analysis of Clusters/Cohorts](https://github.com/sonyah-hawaii/time_series_regressive_modeling/blob/master/Variance%20Analysis.ipynb)  
_This notebook takes in results of K-Means to develop tables that summarize variance, and distinguishes differences in patterns between cohorts._
- [Regression Models](https://github.com/sonyah-hawaii/time_series_regressive_modeling/blob/master/time_series.ipynb)

These notebooks includes the following packages and languages:
- `Numpy` and `Pandas`
- `Scikitlearn`
- `pymc3`
- `Seaborn` and `Matplotlib`  
- Python, LaTex, and Markdown

## Executive Summary:  

This project aims to gain understanding of working with a small dataset with high variance. Utilizing metrics of production and emissions trends, the target (abatement in metric tons of CO2) was developed and passed through 3 regressive models to test different approaches to incorporate variance into the modeling process. The dataset is comprised of:

The data spanned 37 countries over 25 years, and each model trained and tested on historical data with 15 lags. The training model aimed to predict abatement from 2005-2013, and the test model predicted 2014. Models tested were traditional autoregressive model, Random Forest Regressor from `scikitlearn` and Bayesian autoregression with `pymc3`. Before the modeling process the data was passed through K-Means to develop cohorts for modeling.   
A primary focus of this is to assess what Bayesian regression can offer us in terms of incorporating distributions into future predictions. Overall, the model performed better than traditional Autoregressive models, but in some cases not as well as Random Forest Regressor. The traditional autoregressive model acted as a baseline, while Random Forest Regressor was included to test the efficacy of an ensemble method on making difficult predictions. The Bayesian model is distinguished from the other regressions by incorporating variance through informed prior distributions.
                           
With the traditional autoregressive model, it often was able to predict increases in abatement, or capture the peaks in trends, but often lost integrity when predicting troughs. The best Bayesian model was built for Cohort 1, which included the largest group of countries (topping off at 25 of the 35 countries). It scored with a 0.8 for train and 0.64 for test (R2), a marked improvement from the traditional regression's score of 1 on train and -1.18 on test. Across all cohorts, Random Forest Regressor and traditional autoregressive model performed the best; however, the two cohorts modeled using Bayesian autoregression had divergent results, proving they are both excellent subsets to explore how Bayes can improve upon traditional regression, as well as how it can be fine-tuned. 

This project entailed building a series of loops that developed lagged train and test dataset, passed cohorts through the modeling process, and output useable markdown tables. For the Bayesian autoregression, this entailed developing informed priors by passing individual countries through MCMC, and ensembling the resulting predictions for individual countries to determine R2. Additionally, it demanded meticulous organization and information tracking within codes. Each notebook stands and runs through independently.   