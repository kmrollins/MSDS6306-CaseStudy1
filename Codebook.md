# Codebook for Beer and Brewery Data

# K n A Marketing Consultants, 12 Wall street, NY

Beers and Breweries data analysis for Anheuser Busch ltd.

# Introduction

Now this study is conducted to help one of our clients on their marketing campaign. This analysis will help answer certain important questions on the Beer and Breweries information for a calculated and appropriate decision on go to market strategy. The analysis will study Alcoholic content and IBU (international bitterness unit) to position the product with competition from other beer manufacturers including craft beer industry. Enough sample data is provided to conduct the study and analysis.

# Background

Our client Anheuser Busch limited and its CEO Mr. Michel Doukeris is eager to introduce a new beer with optimum alcoholic content (ABV) and international bitterness units (IBU), so that they can compete with other breweries and position itself in the market to regain its top performance slot. This will be an important feature in their marketing campaign and advertisement for the product in the upcoming NFL commercial with enhanced visual effects.

Launching on this project required some quick but a deeper research of the industry and understanding of the competition involved. 
Marketing survey analysis were researched to see what level of ABV and IBU were preferred by its consumers to come up with the best tasting beer.

IBU--International bitterness unit:
IBU is a popular use of measurement of bitterness in beer. The IBU calculations are made using complex formula based on certain variables such as hops used, how long the hops are boiled in the wort, wort density, volume of wort etc. To obscure the bitterness more malt is added.

Alcoholic content (Alcohol by volume-ABV):
Alcohol by volume, or ABV, is used to measure the alcohol content of any drink with alcohol. Beers typically will have in the range of 3.0-13.0%.

<!--https://www.thespruceeats.com/alcohol-by-volume-353204
-->
*Reading/reference materials : 

1. craftbeeracademy.com / beer-characteristics.
2. efficientdrinker.com
3. https://www.thespruceeats.com/alcohol-by-volume-353204

Alternatives/Extensibility: The study can also be used to set up new breweries in various locations to have them locally to satisfy the market demands. The study can also be conducted on pricing the product appropriately to ward off competition at the same time reduce the cost by positioning breweries nearer to the raw material available areas so the transportation is minimal.

Since the CEO was specific on his request on the research study, no new alternatives were considered for the study though they may be weighed in on a future date for an indepth analysis.

# Solution

We have come up with some salient information on the data to present to the CEO for his decision:

1.	State wise number of Breweries present to gauge the competition. 

2.	Merge beer data with the breweries data. Print the first 6 observations and the last six observations to check the merged file.

3.	Report the number of NA's in each column.

4.	Compute the median alcohol content and international bitterness unit for each state. Plot a bar chart to compare.

6.	Summary statistics for the ABV variable.

7.	Is there an apparent relationship between the bitterness of the beer and its alcoholic content? Draw a scatter plot.

####Version of R studio used:

platform       x86_64-w64-mingw32          
arch           x86_64                      
os             mingw32                     
system         x86_64, mingw32             
status                                     
major          3                           
minor          5.1                         
year           2018                        
month          07                          
day            02                          
svn rev        74947                       
language       R                           
version.string R version 3.5.1 (2018-07-02)
nickname       Feather Spray      

#### Input files for the study.
Two input files were used for the study.
1. Beers.csv
This file contains the following columns.
Beer Name,
Beer_ID,
ABV(alcohol by volume),
IBU(International Bitterness Unit),
Brewery_id,
Style,
Ounces
From this file we had to eliminate records that did not have enough data available for ABV and IBU.

2. Breweries.csv
This file contains the following attributes
Brew_Id (identifier for brewery - numeric),
Name(Name of the brewery),
City,
State

For this analysis we mostly used a merged data set that contained all the fields on the key value from both the files (Brew_id and Brewery_id).

The merged frame had the following columns:
Brew_ID,	Brewery_Name,	City,	State,	Beer_Name,	Beer_ID,	ABV,	IBU,	Style,	Ounces

####Libraries loaded:

library(ggplot2)
library(dplyr)
library(DT)
library(knitr)
library(kableExtra)

#### Read in beer and brewery data files
The data files used are 
1. DataFiles/beers.csv
2. DataFiles/breweries.csv
The two files have common identifier in brewery id which can be used to 
identify the records between the two files for merging operation.
The relationship cardinality between breweries to beers is one to many.

#### Count number of breweries in each state
* Create table with state and number of breweries (using kable) Table 1.
* Define color gradient gg plot geom bar for statewise number of breweries (Figure 1)
The table shows the number of breweries, categorized by states in the U.S. (plus District of Columbia) in descending order from highest to lowest.
Figure 1 - shows number of breweries by state.
#### Merge beer and breweries data

The two datasets were merged into one composite dataset. They can be combined because each beer is brewed at,or at least associated with, a particular brewery.Since they have a common id in brewery id that acts as a link between the two datasets.

#### Display beginning of merged data frame 
Table 2a: shows beginning few rows of Merged Data Frame

#### Display tail end of merged data frame 
Table 2b: shows few rows from the end of Merged Data Frame

#### Report column NA's - table 3
Table 3: shows the columns with counts of number of occurance of NA i.e. missing values, in each column.
From this table, we see that there are 62 NA values in the ABV column, and 1005 NA's in the IBU column.
Figure 2 - shows missing values in ABV and IBU

#### Median ABV and IBU by state - Summary statistics.
*Get median values for each state, convert to data frames
*Remove South Dakota since no IBU data was available

####Create a ggplot using geom bar plotting the graph on median ABV.
Figure 3: Median Alcohol Content of Beers by State

####Create a ggplot using geom bar plotting the graph on median IBU.
Figure 4: Median Bitterness of Beers by State

#### States with Maximum ABV and IBU
Determine the state that has the beer with the largest alcohol content, as well as the state where the most bitter beer is brewed.

####We will see the summary statistics of alcohol by volume for all the beers in the United States.
This shows the mean, median , minimum and maximum values of ABV across the beers.
Figure 5: Alcohol content summary.
#### 7. IBU and ABV relationship
This shows the linear relationship of the Bitterness of beer to the alcohol content by volume in each beer category.
Figure 6: Scatter plot on Alcohol content and Bitterness of beers

# Recommendations:

Considering the information given and the market trends thus analyzed so far, the conclusion is that the CEO can take a decision on launching a new product in collaboration with the craft beer breweries.

