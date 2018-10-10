---
title: "MSDS 6306 - Case Study 1"
author: "Anand Rajan & Kristen McCrary"
date: "10/18/2018"
output: 
  html_document:
    keep_md: yes
---


# Introduction

In 2017, 83 percent of all beer was domestically produced, and 17 
percent was imported from more than 100 different countries around 
the world. Based on beer shipment data and U.S. Census population 
statistics, U.S. consumers 21 years and older consumed 26.9 gallons 
of beer and cider per person during 2017. -  
  https://www.nbwa.org/resources/industry-fast-facts

Consumers have many options on the choice of beer they drink today. 
The beer industry is saturated with regards to production and 
consumption over the past 10 years, to ward off competition, and 
position in the market, it is imperative that the brewing companies 
have to come up with new strategies. However, Large breweries still 
are having the majority market share.

Now this study is conducted to help one of our clients on a marketing 
campaign. This analysis would determine certain important questions 
on the Beer and Breweries information for a calculated and appropriate 
decision. The analysis would also include Alcoholic content and IBU 
(international bitterness unit) to position the product with competition 
from other beer manufacturers including craft beer industry. Enough 
sample data is available to conduct the study/analysis.

# Background

Our client Budweiser limited is eager to introduce a new Beer with optimum alcoholic 
content (ABV) and international bitterness units (IBU), so that they can compete 
with other breweries and position itself in the market with regards to pricing. 
This will be an important feature in their marketing campaign and advertisement 
for the product in the upcoming NFL halftime commercial (Most watched) with enhanced 
visual effects.  The strategy would create awareness and curiosity around this new 
beer with their consumers (Budweiser enthusiasts!).

# Analysis


```r
# Read in data files
beers <- read.csv("DataFiles/beers.csv")
breweries <- read.csv("DataFiles/breweries.csv")
```

1. How many breweries are present in each state?


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
plyr::count(breweries, 'State')
```

```
##    State freq
## 1     AK    7
## 2     AL    3
## 3     AR    2
## 4     AZ   11
## 5     CA   39
## 6     CO   47
## 7     CT    8
## 8     DC    1
## 9     DE    2
## 10    FL   15
## 11    GA    7
## 12    HI    4
## 13    IA    5
## 14    ID    5
## 15    IL   18
## 16    IN   22
## 17    KS    3
## 18    KY    4
## 19    LA    5
## 20    MA   23
## 21    MD    7
## 22    ME    9
## 23    MI   32
## 24    MN   12
## 25    MO    9
## 26    MS    2
## 27    MT    9
## 28    NC   19
## 29    ND    1
## 30    NE    5
## 31    NH    3
## 32    NJ    3
## 33    NM    4
## 34    NV    2
## 35    NY   16
## 36    OH   15
## 37    OK    6
## 38    OR   29
## 39    PA   25
## 40    RI    5
## 41    SC    4
## 42    SD    1
## 43    TN    3
## 44    TX   28
## 45    UT    4
## 46    VA   16
## 47    VT   10
## 48    WA   23
## 49    WI   20
## 50    WV    1
## 51    WY    4
```

2. Merge beer and breweries data


```r
beer_data <- merge(breweries, beers, by.x='Brew_ID', by.y='Brewery_id', all=TRUE)
head(beer_data)
```

```
##   Brew_ID             Name.x        City State        Name.y Beer_ID   ABV
## 1       1 NorthGate Brewing  Minneapolis    MN       Pumpion    2689 0.060
## 2       1 NorthGate Brewing  Minneapolis    MN    Stronghold    2688 0.060
## 3       1 NorthGate Brewing  Minneapolis    MN   Parapet ESB    2687 0.056
## 4       1 NorthGate Brewing  Minneapolis    MN  Get Together    2692 0.045
## 5       1 NorthGate Brewing  Minneapolis    MN Maggie's Leap    2691 0.049
## 6       1 NorthGate Brewing  Minneapolis    MN    Wall's End    2690 0.048
##   IBU                               Style Ounces
## 1  38                         Pumpkin Ale     16
## 2  25                     American Porter     16
## 3  47 Extra Special / Strong Bitter (ESB)     16
## 4  50                        American IPA     16
## 5  26                  Milk / Sweet Stout     16
## 6  19                   English Brown Ale     16
```

```r
tail(beer_data)
```

```
##      Brew_ID                        Name.x          City State
## 2405     556         Ukiah Brewing Company         Ukiah    CA
## 2406     557       Butternuts Beer and Ale Garrattsville    NY
## 2407     557       Butternuts Beer and Ale Garrattsville    NY
## 2408     557       Butternuts Beer and Ale Garrattsville    NY
## 2409     557       Butternuts Beer and Ale Garrattsville    NY
## 2410     558 Sleeping Lady Brewing Company     Anchorage    AK
##                         Name.y Beer_ID   ABV IBU                   Style
## 2405             Pilsner Ukiah      98 0.055  NA         German Pilsener
## 2406         Porkslap Pale Ale      49 0.043  NA American Pale Ale (APA)
## 2407           Snapperhead IPA      51 0.068  NA            American IPA
## 2408         Moo Thunder Stout      50 0.049  NA      Milk / Sweet Stout
## 2409  Heinnieweisse Weissebier      52 0.049  NA              Hefeweizen
## 2410 Urban Wilderness Pale Ale      30 0.049  NA        English Pale Ale
##      Ounces
## 2405     12
## 2406     12
## 2407     12
## 2408     12
## 2409     12
## 2410     12
```

3. Report number of NA's in each column


```r
# Get all the NA data from Beer Data
sapply(beer_data, function(x) sum(is.na(x)))
```

```
## Brew_ID  Name.x    City   State  Name.y Beer_ID     ABV     IBU   Style 
##       0       0       0       0       0       0      62    1005       0 
##  Ounces 
##       0
```
* ABVs - 62   NULLS
* IBUs - 1005 NULLS

# Conclusion

TODO
