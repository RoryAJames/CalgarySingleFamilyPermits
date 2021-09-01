# Calgary's Single Family Permits - Exploratory Data Analysis and Cost Prediction Modeling

## Project Overview:

For this project I wanted to take a dive into some single family housing permit data in the City of Calgary.  This project consists of three parts:

**Part 1)** Data cleaning, wrangling, handling missing values, and removing outliers. 

**Part 2)** Exploring the data, uncovering and analyzing trends, and gaining insights into the single family housing market.

**Part 3)** Build a cost prediction model to predict the project cost of a single family house where the user specifies the variables.

## The Data:

The data that I used came from the Build Permits dataset located in the City of Calgary Open Data portal. A link to this dataset can be found [here](https://data.calgary.ca/Business-and-Economic-Activity/Building-Permits/c2es-76ed).

## A Few Notes:

* The project cost of a permit does not equal the overall cost of a home. We can think of project cost as the construction cost of a house, not the sale price.

* I only looked at permits that were applied for after January 2010.

* I only looked at applications that are deemed complete, meaning that the house was actually built.

* Since there are a lot of contractors and builders that operate in Calgary, I only looked at the top 10 builders by value count. This still provided a good overview of the trends in Calgary's single family real estate market as the top 10 builders make up the vast majority of the permit applications. This also reduced the number of dimensions and the likelihood of overfitting the prediction model.

Still needs work...
