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

5.	Which state has the maximum alcoholic (ABV) beer? Which state has the most bitter (IBU) beer?

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

# Count number of breweries in each state


# Recommendations:



