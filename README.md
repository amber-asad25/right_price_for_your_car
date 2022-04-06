# Right Price to Sell your Used Car
## Introduction 
* Develop a project that predicts best price to sell your used car according to market value. It can help sellers better negotiate on price to get maximum profit.
* Scraped over 451 car selling advertisment using chrome web scraper extension.
* Engineered features from the text of each title of add to quantify the which car is VXR or VXL and what effect does it have on car price.
* Optimized Linear, Lasso, and Random Forest Regressors using GridsearchCV to get more accurate result. 
* Deploy model using Flask API. 

## Credit to youtube channel
[Ken Jee](https://www.youtube.com/playlist?list=PL2zq7klxX5ASFejJj80ob9ZAnBHdz5O1t)

## Web Scraping
I make use of chrome web scraper extention to scrape data from following car selling websites
*	[PakWheels](https://www.pakwheels.com/)
*	[CarFirst](https://www.carfirst.com/)

With scraping we are able to collect information about following:
* title
* model 
* make
* trim
* year
*	price
*	automatic or manual
*	bodytype
*	assembly
*	enginecapacity
*	color
*	registeredcity
*	fueltype
*	registeryear
*	location
*	mileage

## Data Cleaning
After web scrapping the required data, I have to clean it up to make it in the form I can use for my machine learning model. I did the following steps:

*	Deleted the unnecessary columns that come with a register year chrome extension.
*	Correctly label the columns so that it does not have space in their name.
*	Remove works from all the rows like cc in the engine capacity column and PKR in the price column.
*	Also deleted every comma and full stop.
*	Merge data from both websites into a single CSV and xlsx file.
*	Correct the data type of columns.
*	For PakWheels data there was no separate column for make, model, trim, and year so I make them by using the title column.
![alt text](https://github.com/amber-asad25/right_price_for_your_car/blob/master/Images/datacleaning1.PNG "Column making")
*	Fill NaN values of different columns.
*	There was inconsistency in some categorical value spelling like Automatic and automatic so I make it correct.
*	Made columns for more features from the title of the car add like:
    * VXL
    * VXR

## EDA
I observed different categorical variable value counts and created histograms to study distributions. I also observed the correlation between variables and gain some insights. Bar charts, box plots, and pivot tables also help a lot. Below are some pictures for you:

![alt text](https://github.com/amber-asad25/right_price_for_your_car/blob/master/Images/eda1.PNG "histogram")
![alt text](https://github.com/amber-asad25/right_price_for_your_car/blob/master/Images/eda2.PNG "Box plot")
![alt text](https://github.com/amber-asad25/right_price_for_your_car/blob/master/Images/eda3.PNG "Heat map")
![alt text](https://github.com/amber-asad25/right_price_for_your_car/blob/master/Images/eda4.PNG "Bar chart1")
![alt text](https://github.com/amber-asad25/right_price_for_your_car/blob/master/Images/eda5.PNG "Bar chart2")
![alt text](https://github.com/amber-asad25/right_price_for_your_car/blob/master/Images/eda6.PNG "pivot table")

## Model Building 

First, I transformed the categorical variables into dummy variables. I also split the data into train and tests sets with a test size of 20%.   

I tried three different models and evaluated them using Mean Absolute Error. I chose MAE because it is relatively easy to interpret and outliers aren’t particularly bad fo in the type of model.   

I tried three different models:
*	**Multiple Linear Regression** – Baseline for the model, to have a better understanding.
*	**Lasso Regression** – I thought a normalized regression like lasso would be effective because of the sparse data from the many categorical variables.
*	**Random Forest** – Due to our data, it fits nicely. 

## Model performance
The Random Forest model far outperformed the other test and validation sets approaches. But all three of them did not give the remarkable result the reason being small data with lots of missing values.

## Model Deployment
In this step, I built a flask API endpoint that was hosted on a local webserver. The API endpoint takes in a request with a list of values from a job listing and returns an estimate. 
![alt text](https://github.com/amber-asad25/right_price_for_your_car/blob/master/Images/dep1.PNG "Output1")
![alt text](https://github.com/amber-asad25/right_price_for_your_car/blob/master/Images/dep2.PNG "Output2")
