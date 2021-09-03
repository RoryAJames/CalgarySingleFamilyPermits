# Calgary's Single Family Permits - Exploratory Data Analysis and Cost Prediction Modeling

## Project Overview

For this project I wanted to take a dive into some single family housing permit data in the City of Calgary. This project consisted of three parts:

**Part 1)** Data cleaning, wrangling, handling missing values, and removing outliers. 

**Part 2)** Exploring the data, uncovering and analyzing the trends taking place in Calgary's single family housing market.

**Part 3)** Building a cost prediction model to predict the project cost of a single family house where the user specifies the attributes.

## The Data

The data that I used came from the Building Permits dataset located in the City of Calgary Open Data portal. Each row in this dataset represents a building permit with a unique identifier and the permits attributes. Every single building permit that has been applied for in the City of Calgary as of 1996 is represented. At the time of writing, this amounts to nearly 383,000 building permits. A link to this dataset can be found [here](https://data.calgary.ca/Business-and-Economic-Activity/Building-Permits/c2es-76ed). 

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

All the exploratory data analysis steps I took can be found in the full notebook. Here are just some of the highlights that I found while exploring the data:

Not surprisingly, square footage and project cost have a strong linear relationship with eachother. While there are some points that deviate from the linear trend, I decided to leave them in to see how well the prediction model held up.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/SquareFootageVSProjectCosts.png)

Calgary is very much a sprawling city with the vast majority of single family permits being located in communities on the boundaries of the city. Only a handful of single family permits are located near the downtown area. Additionally, the South East quadrant makes up the bulk of the single family permit activity since 2010. Lastly, some communities have only one, or very few, permits located in them. It was later discovered that 60% of all the single family permit completions are located in the top 10 communities by value count. Since it is not practical to predict the cost of something that appears only once, along with the knowledge that communities can be consolidated into quadrants, I opted to not use community as a feature in the prediction model and go with the qaudrant feature instead.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/map.png)

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/QuadrantBreakdown.png)

However, the South East quadrant hasn't been the most favoured quadrant every year. When you look at the permit applications over time, you find that as of 2016 the North East qaudrant has been the more favoured quadrant amongst the top 10 builders. It also appears that the trend line for yearly permit applications has been downward as of 2014. At the time of working on this project, very few permits were completed in the current year. This explains why there is a drastic drop off at the end of the graph.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/PermitApplicationsByQuadrant.png)

The average cost per square foot increased across all of the quadrants from the period between 2010 and 2016. From 2016 onward the average cost per square foot plateaued, and as of this year, appears to be heading downwards. There doesn't appear to be much deviation in terms of the order as well. For example, the North East has maintained the lowest average cost per sqaure foot for basically the entire dataframe.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/AverageCostPerSquareFootQuadrant.png)

All of the builders are in excess of a thousand single family permit applications that have been completed since 2010. The lion's share goes to Jayman having built nearly 3,500 in this timeframe.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/Top10Builders.png)

All of the builders have either maintained or decreased their number of yearly permit applications since 2010. The most dramatic builder is Cardel, which shows a strong downward trend in their permit application volume as of 2010. In fact, at the time of working on this project, they have not completed a single permit for the year while all of the other builders have. There is no clear uptrend in permit applications for any of the builders. It is worth noting that Mattamy did not enter the Calgary market until 2013 which is explained by their plot starting that year.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/download.png)

The median construction cost per square foot is fairly consistent across the builders. They all appear to be around the $150 value, with the exception of Mattamy whose median value is above $160.

In terms of the spread, Morrison and Brookfield appear to have fairly large construction cost spreads ranging from $90 per square foot to above $200 per square foot. Mattamy on the other hand has a much tighter spread in comparison to the rest of the builders.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/CostPerSqaureFootBuilder.png)

With the exception of Cedarglen, Shane Homes, and Mattamy, all of the builders are showing a reduction in their average cost per square foot as of this year. I think it is too early to say whether this trend is indicative of something. The reason for this is that these builders have only completed a handful of permits at the time of working on this project.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/AverageCostPerSquareFootBuilder.png)

The duration between when a permit is issued and when a permit is completed does not appear to be an accurate representation of construction duration. The average construction duration for a single family home was found to be 185 days (roughly six months). However, when plotting construction duration and square footage on a scatter plot it shows that a large portion of permits are well in excess of the 185 day average. Additionally, it appears that there is no clear linear relationship between these two variables.

What I think is happening here is that the builders are getting their permits sorted out in advance of a home being sold to a buyer. This way the builder can begin the construction of the house without delay after it has been sold.

Without having definitive data for the construction start date, it isn't really practicle to analyze the construction duration.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/SquareFootageVSConstructionDuration.png)

December appears to be the month with largest number of housing completions. This seems logical. Not only is December the fiscal year end for many companies, but it is also the point in the year where the building conditions become really unfavourable due to the weather. Assuming that a single family house in Calgary takes an average of six months to build, this means that the construction typically begins in the summer months of June/July when the weather is more favourable.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/PermitCompletionsMonth.png)

However, when checking for seasonality it is apparent that in one year the builders completed far more permits in the month of December than any other. With this in mind, it is not reasonable to say that most permits are completed in the month of December since one year has skewed the data making it appear this way. Additionally, it does not appear that there is any clear seasonality as to when permits are completed.

![](https://github.com/RoryAJames/CalgarySingleFamilyPermits/blob/main/images/PermitCompletionsYear.png)

## Cost Prediction Model Building

## Model Performance

## Predicting The Project Cost of A House
