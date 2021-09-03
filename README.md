# Calgary's Single Family Permits - Exploratory Data Analysis and Cost Prediction Modeling

## Project Overview

For this project I wanted to take a dive into some single family housing permit data in the City of Calgary. This project consisted of three parts:

**Part 1)** Data cleaning, wrangling, handling missing values, and removing outliers. 

**Part 2)** Exploring the data, uncovering and analyzing the trends taking place in Calgary's single family housing market.

**Part 3)** Building a cost prediction model to predict the project cost of a single family house where the user specifies the attributes.

## The Data

The data that I used came from the Building Permits dataset located in the City of Calgary Open Data portal. Each row in this dataset represents a building permit with a unique identifier. Every single building permit that has been applied for in the City of Calgary as of 1996 is in this dataset. A link to this dataset can be found [here](https://data.calgary.ca/Business-and-Economic-Activity/Building-Permits/c2es-76ed). 

## A Few Notes

* The project cost of a permit does not equal the overall cost of the house. We can think of project cost as the construction cost, not the sale price.

* I only looked at permits that were applied for after January 2010.

* I only looked at permits that are deemed complete (the house has been built).

* Given that there are a lot of contractors and builders that operate in Calgary, I decided to only look at the top 10 builders by value count. This still provides a good overview of Calgary's single family housing activity, since the top 10 builders make up the vast majority of the permit applications. This also reduced the number of dimensions and the likelihood of overfitting the prediction model.

## Data Cleaning

After gathering the data, I needed to clean it up so that I could analyze it, and make it usable for the prediction model. I made the following changes and created the following variables:

* Cast the various date columns into datetime data types.

* Filtered the dataframe down so it only shows permits that were applied for on or after January 1st 2010.

* Filtered the dataframe down so it only shows permits that are completed.

* Filtered the dataframe down to the top 10 builders by value count.

* Renamed the existing columns to more understandable conventions.

* Renamed the builders from their legal names to their marketing names.

* Added a cost per sqaure foot column.

* Added a construction duration column (the number of days between when a permit was issued and when it is deemed complete).

* Added a column to identify which quadrant the permit is located in (North West, North East, South West, South East) 

* Droped all of the unnecessary columns.

* Removed rows where there were missing values (less than 1% of values were missing).

* Removed the outliers that appeared in the sqaure footage vs project cost scatter plot.

## Exploratory Data Analysis

Here are just some of the highlights that I found while exploring the data:

Not surprisingly, square footage and project cost have a strong linear relationship with eachother. While there were some points that deviated from the linear trend, I decided to leave them in to see how well the prediction model held up.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/SquareFootageVSProjectCosts.png)

Calgary is very much a sprawling city with the vast majority of single family permits being located in communities on the boundaries of the city. Only a handful of single family permits are located near the downtown area of Calgary. Additionally, the South East quadrant makes up the bulk of the single family permit activity since 2010. Lastly, some communities have only one, or very few, permits located in them. It was later discovered that 60% of all the single family permit completions are located in the top 10 communities by value count. Since it is not practical to predict the cost of something that appears only once, and the fact that communities can be consolidated into quadrants, I opted to not use community as a feature in the prediction model and go with qaudrant instead.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/map.png)

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/QuadrantBreakdown.png)

However, when you look at the permit applications on a yearly basis you find that as of 2016 the North East qaudrant has been the more favoured quadrant amongst the top 10 builders. 

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/PermitApplicationsByQaudrant.png)
