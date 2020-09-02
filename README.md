# Forecasting Uber Travel Times

#####    by <b>[Bobby Williams](https://github.com/bobbyiestofjos)</b>

---

## Repo Contents

- <b>data</b> - Various datasets used for modeling and reference.
- <b>images</b> - Various plots and images used in the documents found in this repo.
- <b>notebooks</b> - Jupyter Notebooks created for this project.
    - <b>[01_data_prep.ipynb](notebooks/01_data_prep.ipynb)</b> - Data prep...
    - <b>[02_eda.ipynb](notebooks/02_eda.ipynb)</b> - Jupyter Notebook containing Exploratory Data Analysis.
    - <b>[03_model_01_base.ipynb](notebooks/03_model_01_base.ipynb)</b> - Jupyter Notebook containing the process for creating a base model.
    - <b>[03_model_02_all.ipynb](notebooks/03_model_02_all.ipynb)</b> - Jupyter Notebook containing the process for creating all models.
- <b>[executive.ipynb](executive.ipynb)</b> - The main Jupyter Notebook containing the models and analysis for this project.
- <b>[presentation](presentation.pdf)</b> - The presentation for this project.
- <b>[README.md](README.md)</b> - A description of the project goals, process, and results.

---

## Uber Movement

![uber_movement](images/uber_movement.png)

In January of 2017 Uber introduced a website tool for urban planners to access and download their anonymized and aggregated trip data. Their intent was to help inform decisions about how to adapt existing infrastructure and invest in future solutions to make cities more efficient.

---

## Goal

Uber Movement allows site visitors to map trips between census tracts across select cities to view historical mean travel times between those tracts. Currently Uber Movement only provides historical information.

The goal of this project is to predict future travel times across Washington DC, via time series modeling, for urban planners utilizing Uber Movement, or a similar web app, for city planning.

---

## Data

Over 17 million data points across 32 csv files were pulled from the Uber Movement website. These were combined to form a single dataset which included a monthly average for Mean Travel Times from the year 2016 thru 2019 between census tract locations across Washington DC.

For this date range the granularity was limited to monthly averages broken down by weekday and weekend trips.

---

## Modeling

SARIMA modeling is a time series forecasting method that includes a component for data with underlying seasonality.

Due to the uniqueness of each trip across DC: trip distance, multiple route options, speed limits, etc, a separate model is needed for every trip. Over 31,000 optimized SARIMA models are available for deployment to forecast travel times.

There was a trade-off between model complexity and runtime due to processing power.

### Performance

![predicted](images/predicted.png)

This plot is for a weekday trip with the observed travel times along with the forecasted travel times from the model for 2019.

Multiple model iterations are produced for each trip using different parameters to minimize Root Mean Square Error, the metric used to determine model performance.

Here the Root Mean Square Error is a measure of the differences between values forecasted by the model and the observed values. (9.31)

### Predictions

![forecast](images/forecast.png)

After determining the optimum parameters for each model, forecasts are created for the year 2020.

These forecasts will allow urban planners to quickly look at what the next year or period of time will look like across specific areas of the city.

---

## Conclusion

Implement the process for model development from this project into the Uber Movement interface, or a similar web application, to allow urban planners to determine the potential impact of future city projects on forecasted travel times.

---

## Future Work

Road Construction  
To assist with this I’ve pulled occupancy permit data for Washington DC to determine the effects certain types of planned roadway construction/congestion such as Construction Staging Areas, Parades, and City Events have on travel times.

Wider Implementation  
The process in this project is easily scalable to additional cities for wider implementation.

Improve Modeling  
As mentioned, the models were simplified due to processing power constraints. Addressing this will allow for more complex models providing improved forecasting.



---
---
---



## Conclusions

• For every 1,000 images:

   • At a 90% prediction probability cutoff, we only have to manually check 140 images. (86% reduction of work.)
   
   • At a 95% prediction probability cutoff, we only have to manually check 200 images. (80% reduction of work.)
   
   • At a 99% prediction probability cutoff, we only have to manually check 310 images. (69% reduction of work.)
   
Given that the model was only able to correctly identify "cracked" images 2 out of every 3 times, I would hesitate to put this model in production at the moment. Automated deficiency detection potentially poses a safety issue if very serious cracking is missed by the algorithm. So before implementing this tool, it would be prudent to gather a larger set of images and spend more time tweaking the CNN architecture to produce more reliable results. I think the model should be correctly identifying 9 out of every 10 "cracked" images before considering putting the model to use in the real-world. 

Another variable to consider is the prediction probability "cutoff" point. How much uncertainty from the model's decision-making are we willing to tolerate? There is an strong positive correlation between the model's prediction probability cutoff percentage and the number of images to be manually checked. As the prediction probability cutoff increases, so do the number of images to be manually checked. So an important question is this: are we more willing to do more manual checking to ensure the safety of building users? Or, are we willing to miss a few cracks observed on the construction site to save more time and money? This should be debated with other practicing professionals to arrive at a consensus.

## Future Work

To improve this project, I would use images with even more “visual noise” to train on. Furthermore, I would consider more types of materials, such as plastics, wood, composites, or even rammed earth. Finally, I would spend more time training and tuning various layers of the CNNs to improve training metrics and reduce the loss function.
   
In the future, I would build more CNNs to detect other types of deficiencies besides cracking. Then we could combine these models to build a tool that can detect all types of construction deficiencies. In the further future, instead of people, maybe drones could take photos of construction sites! Using a more robust version of this tool, drones could auto-identify deficient work! This would save an even more tremendous amount of time and money for architecture, engineering, and construction firms.