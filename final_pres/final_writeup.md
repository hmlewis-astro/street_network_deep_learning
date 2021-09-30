# Project Write-Up
## Classification of Aggressive Driving Behavior from Smartphone Data


### Abstract

The goal of this project was to classify driving behaviors as normal or abnormal (here, meaning either aggressive or drowsy driving), with the ultimate objective of implementing this model in a real-world, semi-autonomous vehicle. I utilized data from the [UAH-DriveSet](http://www.robesafe.uah.es/personal/eduardo.romera/uah-driveset/) to build a Random Forest classifier; the model is tuned to optimize the F2-score (weighting recall more heavily than precision), and attains F2 = 0.9925. After finalizing the model, I built an interactive Jupyter Binder to understand how the model classifications change with each feature from the data set.


### Design

The near-instantaneous analysis of driver behavior is an important part of the function and safety of semi-autonomous vehicles (i.e., vehicles with advanced driver assist systems). For example, many semi-autonomous vehicles are capable of warning/correcting the driver if they are drifting from their lane or if the person ahead of them has suddenly slowed their speed. Therefore, using data from built-in car sensors&mdash;or, in this case, from a smartphone app&mdash;to also quickly classify driving behaviors as aggressive (and to then warn drivers about those behaviors) will further improve the safety of such vehicles, and may lead to increased confidence in high- and fully-autonomous vehicles.

In this project, we seek to determine what aspects of a driver's behavior are most important for identifying aggressive driving behavior.

### Data

The UAH-DriveSet provides scores (i.e., features) for acceleration, braking, turning, weaving (between lanes), drifting (within lane), speeding, and following distance, as well as the driving style that a driver was simulating (normal vs. abnormal; i.e., the target) during each drive. Drives are recorded for a range of driving styles (normal vs. abnormal, including aggressive and drowsy), in a variety of environments (day vs. night, on highways vs. secondary roads).


I have also scraped weather conditions for the date, time, and location of each recorded drive, from Weather Underground. A multitude of weather data are scraped; however, the drives collected in this dataset were recorded only at times when there was no precipitation, when the temperature was above freezing, and when conditions were fair (i.e., low winds, low cloud cover). Therefore, on the whole, weather conditions do not vary significantly between drives. The only parameter scraped from Weather Underground that varies significantly between the various drives in the dataset is whether it is day or night.


### Algorithms

#### EDA & Feature Engineering
EDA and feature engineering are carried out through the entirety of the modeling process.

The pair plot of a subset of the relevant features from the UAH-DriveSet reveal that the scores for normal driving behaviors generally have a higher median and a narrower (near Gaussian) distribution compared to the scores for abnormal driving behaviors, which show very broad, left-skewed distributions (i.e., tail toward very low scores). Based on the pair plot, I selected the acceleration, braking, and speeding scores&mdash;which appear to have distinct distributions in the kde plots&mdash;as the features utilized in the baseline models.

From the change in latitude, longitude of each observation of a given drive, and the time between observations, I calculate the average speed over the interval (in miles per hour). Other features that _could not_ have been engineered from the given data, but may have been important features, might be the age of the driver and the speed limit of the roads driven.

The classes in the dataset are relatively balanced (~40% negative class, ~60% positive class), so no resampling or class weighting techniques are apllied to these data.

#### Modeling
I generate baseline KNN, logistic regression, decision tree, and Random Forest models on a small number of features and a subsample of the data (to improve training time), evaluating each model on the F2-score obtained on the validation set. The F-beta score, with beta > 2 (weighting recall more heavily than precision), is chosen because false negative predictions, where we misidentify abnormal driving behaviors, are potentially very dangerous in practice in an autonomous vehicle. Due to lower validation scores (logit), overfitting (decision tree), and lengthy prediction times (KNN), I ultimately select the Random Forest classifier. Each estimator in the Random Forest is grown deep (i.e., no max depth), and the number of estimators is approximated as the value at which at which the out-of-bag error stabilizes. We find that 150 estimators is sufficient to balance the increased variance due to the over-fitting of individual estimators.

The final model is retrained on the training data (comprised of 80% of the full dataset) and includes features for acceleration, braking, turning, weaving (between lanes), drifting (within lane), speeding, and following distance scores, as well as the speed (in mph), the type of road driven (highway vs. secondary), and whether it was day or night during the drive. The resulting model attains F2 = 0.9925 on the test data. Feature importances (shown below) are extracted and the trained model is pickled for use in an interactive notebook.

<p align="center">
<img src="https://github.com/hmlewis-astro/classify_aggressive_driving/blob/main/figures/feature_importance.png" width="420" />
</p>

#### Visualization
To allow interaction with the model (and to simulate how the model might behave if implemented in a semi-autonomous vehicle), I have created a publicly available Jupyter Binder: [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/hmlewis-astro/classify_aggressive_driving/HEAD?filepath=final_class_model.ipynb)

The video below uses that Binder to  simulate what it might look like if someone is drowsy driving, and starts to drift within their lane. As the driver's drifting score decreases (such that the predicted class probability falls below the threshold), the model classifies the driving behavior as abnormal, and at that point the vehicle might flash a red warning light to notify the driver that something about their driving appears to be abnormal.

https://user-images.githubusercontent.com/21116401/131949959-997e2c33-460a-4391-935d-35f6980834a9.mov

### Tools
- Selenium, and BeautifulSoup for web scraping
- Pandas and Numpy for data analysis and exploration
- Scikit-learn for building, tuning, training, and testing the various baseline and final models
- Matplotlib and Seaborn for plotting and visualizations
- IPywidgets and Binder for publicly available, interactive visualizations

### Communication

In addition to the slides and visuals presented here, the interactive Binder notebook will be included in a forthcoming blog post.
