# Codebook for Beer and Brewery Data

# K n A Marketing Consultants, 12 Wall street, NY

Beers and Breweries data analysis for Anheuser-Busch Ltd.

# Introduction

This study is conducted to help one of our clients on a marketing campaign. This analysis will determine important questions regarding beer and breweries information for a calculated and appropriate decision on go-to-market strategy. The analysis will also examine alcoholic content and bitterness measurements to position the product against competition from other beer manufacturers, including the craft beer industry. Sufficient sample data is available to conduct the study.

# Background

Our client Anheuser-Busch Limited and its CEO Mr. Michel Doukeris are eager to introduce a new beer with optimum alcoholic content (ABV) and international bitterness units (IBU), so that they can compete with other breweries and position itself in the market to regain its top performance slot. This will be an important feature in their marketing campaign and advertisement for the product in an upcoming NFL commercial with enhanced visual effects.

# Research

Launching this project required some quick but deep research of the industry and understanding of the competition involved. 
Marketing survey analyses were researched to see what level of ABV and IBU were preferred by its consumers to come up with the best tasting beer.

**IBU - International Bitterness Unit**:
IBU is a popular use of measurement of bitterness in beer. The IBU calculations are made using complex formula based on certain variables such as hops used, how long the hops are boiled in the wort, wort density, volume of wort etc. To obscure bitterness more malt is added.

**ABV - Alcohol by Volume**:
Alcohol by volume, or ABV, is used to measure the alcohol content of any drink with alcohol. Beers typically fall in the range of 3.0-10.0% ABV.

*Reading/reference materials*: 

1. craftbeeracademy.com/beer-characteristics
2. www.efficientdrinker.com
3. https://www.thespruceeats.com/alcohol-by-volume-353204

*Alternatives/Extensibility*: The study can also be used to set up new breweries in various locations to have them satisfy local market demands. The study can also be conducted on pricing the product appropriately to ward off competition, while reducing cost by positioning breweries nearer to areas with raw material available so transportation is minimal.

Since the CEO was specific in his requests for the research study, no new alternatives were considered for the study. However, they may be weighed in on a future date for further in-depth analysis.

# Solution

We have come up with some salient information on the data to present to the CEO for his decision:

1.	How many breweries are present in each state?

2.	Merge beer data with the breweries data. Print the first 6 observations and the last six observations to check the merged file.

3.	Report the number of NA's in each column.

4.	Compute the median alcohol content and international bitterness unit for each state. Plot a bar chart to compare.

5.	Which state has the maximum alcoholic (ABV) beer? Which state has the most bitter (IBU) beer?

6.	Summary statistics for the ABV variable.

7.	Is there an apparent relationship between the bitterness of the beer and its alcoholic content? Draw a scatter plot.

# Software

We used the R programming language to code solutions to these questions. We also used the RStudio IDE as an environment to write-up our analyses along with our code.

#### R version:

|                |                              |
|----------------|------------------------------|
| platform       | x86_64-w64-mingw32           |         
| arch           | x86_64                       |           
| os             | mingw32                      |         
| system         | x86_64, mingw32              |         
| status         |                              |         
| major          | 3                            |         
| minor          | 5.1                          | 
| year           | 2018                         | 
| month          | 07                           | 
| day            | 02                           | 
| svn rev        | 74947                        | 
| language       | R                            | 
| version.string | R version 3.5.1 (2018-07-02) | 
| nickname       | Feather Spray                | 

#### Session info:

R version 3.5.1 (2018-07-02)

Platform: x86_64-apple-darwin15.6.0 (64-bit)

Running under: macOS High Sierra 10.13.6

#### R packages used:

* ggplot2
* dplyr
* knitr
* kableExtra

# Analysis

#### Original data

Two input files were provided by our client and used for the study.

1. Beers.csv

This file contains the following columns.

| Column            | Description                                | Type        | Example Values/Range           |
|-------------------|--------------------------------------------|-------------|--------------------------------|
| Name              | Name of the beer                           | String      | "Ginja Ninja", "Back in Black" |
| Beer_ID           | Unique identifier of the beer              | Int         | 1 - 2692                       |
| ABV               | Alcohol by volume of the beer              | Decimal     | 0.001 - 0.128                  |
| IBU               | International Bitterness Units of the beer | Int         | 4 - 138                        |
| Brewery_id        | Brewery ID associated with the beer        | Int         | 1 - 558                        |
| Style             | Style of the beer                          | Factor      | American IPA, Light Lager      |
| Ounces            | Ounces of beer                             | Decimal     | 8.4 - 32                       |

2. Breweries.csv

This file contains the following attributes.

| Column            | Description                                | Type        | Example Values/Range                             |
|-------------------|--------------------------------------------|-------------|--------------------------------------------------|
| Brew_ID           | Unique identifier of the brewery           | Int         | 1 - 558                                          |
| Name              | Name of the brewery                        | String      | "NorthGate Brewing", "Against The Grain Brewery" |
| City              | City where the brewery is located          | Factor      | Portland, Chicago                                |
| State             | U.S. state where the brewery is located    | Factor      | CO, FL, TX                                       |

Now we will detail the R code we used in each section to perform data analysis for our client.

#### Read in beer and brewery data files

The data files used are 
1. DataFiles/beers.csv
2. DataFiles/breweries.csv

We used the R code below to load in these data files in order to proceed with the analysis.

```r
beers <- read.csv("DataFiles/beers.csv")
breweries <- read.csv("DataFiles/breweries.csv")
```

#### Count number of breweries in each state

First, we created a data frame with the brewery counts for each state, using the plyr package (included in the dplyr package).

```r
cdf <- plyr::count(breweries, 'State')
names(cdf)<- c("State", "NumBreweries")
```

We also defined a color gradient to apply to the 51 state categories, and created a ggplot barchart for the statewise number of breweries using the ggplot2 package.

```r
grad <- scales::seq_gradient_pal("brown", "yellow")(seq(0,1,length.out=51))

ggplot(cdf, aes(x=reorder(State, -NumBreweries), y=NumBreweries, fill=State)) +
  geom_bar(stat='identity', position='dodge') +
  labs(title="Figure 1: Number of Breweries per State", x="State", y="Number of Breweries") +
  theme(plot.title = element_text(hjust=0.5), axis.text.x=element_text(angle=90, size=7), 
        legend.position="none") +     
  scale_fill_manual(values=grad)
```

This code generated Figure 1, which shows number of breweries by states in the U.S. (plus District of Columbia) in descending order from highest to lowest.

#### Merge beer and breweries data

For the remaining analysis we primarily used a merged dataset that contains all the fields from both of the data files. The two files have a common identifier of brewery ID, which we used to identify the records between the two files for merging.

After merging the data using the brewery ID number, note that we also chose to modify column names since both the beers and breweries datasets had a "Name" column. Thus we distinguished between those variables.

```
beer_data <- merge(breweries, beers, by.x='Brew_ID', by.y='Brewery_id', all=TRUE)
names(beer_data)[c(2, 5)] <- c("Brewery_Name", "Beer_Name")
```

The resulting composite dataset, stored in an object named *beer_data*, has the following columns.


| Column            | Description                                | Type        | Example Values/Range                             |
|-------------------|--------------------------------------------|-------------|--------------------------------------------------|
| Brew_ID           | Unique identifier of the brewery           | Int         | 1 - 558                                          |
| Brewery_Name      | Name of the brewery                        | String      | "NorthGate Brewing", "Against The Grain Brewery" |
| City              | City where the brewery is located          | Factor      | Portland, Chicago                                |
| State             | U.S. state where the brewery is located    | Factor      | CO, FL, TX                                       |
| Beer_Name         | Name of the beer                           | String      | "Ginja Ninja", "Back in Black"                   |
| Beer_ID           | Unique identifier of the beer              | Int         | 1 - 2692                                         |
| ABV               | Alcohol by volume of the beer              | Decimal     | 0.001 - 0.128                                    |
| IBU               | International Bitterness Units of the beer | Int         | 4 - 138                                          |
| Style             | Style of the beer                          | Factor      | American IPA, Light Lager                        |
| Ounces            | Ounces of beer                             | Decimal     | 8.4 - 32                                         |

Note that the relationship cardinality between breweries and beers is one to many, since breweries may make multiple beers. 

#### Display beginning of merged data frame 

To show that the merge was a success, we displayed the first few rows of the composite dataset. We chose to omit the ID fields from the display because they were not necessary for the client to see. This code requires the knitr package to use the "kable" function, as well as the kableExtra package for the kable_styling function that improves the table's formatting.

```r
hd <- select(head(beer_data), -Brew_ID, -Beer_ID)
kable(hd, row.names=FALSE, caption="Table 1: Beginning of Merged Data Frame") %>% kable_styling(bootstrap_options="bordered")
```

This code generated Table 1, showing the beginning few rows of the merged data frame.

#### Display tail end of merged data frame 

Similarly, we also displayed the last few rows of the composite dataset. We again chose to omit the ID fields from the display. This code also requires the knitr and kableExtra packages.

```r
tl <- select(tail(beer_data), -Brew_ID, -Beer_ID) # Hide ID fields
kable(tl, row.names=FALSE, caption="Table 2: End of Merged Data Frame") %>% kable_styling(bootstrap_options="bordered")
```

This code generated Table 2, which shows a few rows from the end of the merged data frame.

#### Report column NA's

We first created a data structure from applying a count of NA values to each column in the composite data set. We also converted this to a data frame, so it could be utilized by a ggplot in the future.

```r
na_table <- sapply(beer_data, function(x) sum(is.na(x)))
na_df <- as.data.frame(na_table)
```

Next we visualized the information by creating both a table and a barchart. This code requires the knitr, kableExtra, and ggplot2 packages.

```r
kbl <- kable(na_table, col.names="Number of NAs", caption="Table 3: NA Counts")
kable_styling(kbl, full_width=FALSE, bootstrap_options="bordered")

ggplot(na_df, aes(x=reorder(rownames(na_df), na_table), y=na_table)) + 
  geom_bar(stat='identity', position='dodge', fill="darkred", color="darkred") +
  coord_flip() +
  labs(title="Figure 2: Missing Values", x="Variable", y="Number of NAs") +
  theme(plot.title = element_text(hjust=0.5), legend.position="none") 
```

The code creates Table 3, which shows the columns with counts of number of occurance of NA i.e. missing values, in each column.
From the table, we saw that there are 62 NA values in the ABV column, and 1005 NA's in the IBU column. Figure 2 also visualizes the proportion of missing values in ABV and IBU.

#### Median ABV and IBU by state

Next, we obtained median values for both ABV and IBU for each state, then converted those structures to data frames. We also removed South Dakota from the median_IBU data frame since no IBU data was available for that state.

```r
median_ABV <- tapply(beer_data$ABV, beer_data$State, median, na.rm=TRUE)
median_IBU <- tapply(beer_data$IBU, beer_data$State, median, na.rm=TRUE)
median_ABV <- as.data.frame(median_ABV); median_ABV$State <- rownames(median_ABV)
median_IBU <- as.data.frame(median_IBU); median_IBU$State <- rownames(median_IBU)

median_IBU <- subset(median_IBU, State!=" SD")
```

We also used ggplot2 to create a barchart for median ABV by state (Figure 3), specifiying many options for the formatting of the graph. First we defined a color gradient to be applied to the 51 state values.

```r
grad <- scales::seq_gradient_pal("brown", "yellow")(seq(0,1,length.out=51))

ggplot(median_ABV, aes(x=reorder(State, -median_ABV), y=median_ABV, fill=State)) +
  geom_bar(stat='identity', position='dodge') +
  labs(title="Figure 3: Median Alcohol Content of Beers by State", x="State", y="Median ABV") +
  theme(plot.title = element_text(hjust=0.5), axis.text.x=element_text(angle=90, size=7), 
        legend.position="none") +     
  scale_fill_manual(values=grad)
```

Similarly, using the same color gradient we created a ggplot barchart for median IBU by state (Figure 4).

```r
ggplot(median_IBU, aes(x=reorder(State, -median_IBU), y=median_IBU, fill=State)) +
  geom_bar(stat='identity', position='dodge', na.rm=TRUE) +
  labs(title="Figure 4: Median Bitterness of Beers by State", x="State", y="Median IBU") +
  theme(plot.title = element_text(hjust=0.5), axis.text.x=element_text(angle=90, size=7), 
        legend.position="none") +     
  scale_fill_manual(values=grad)
```

#### States with maximum ABV and IBU

To determine the state that has the beer with the largest alcohol content, we wrote code to find the top three alcoholic beers and display a few of their attributes in a table (Table 4).

```r
max_ABV <- beer_data[order(beer_data$ABV, decreasing=TRUE), c("State", "Beer_Name", "ABV", "Brewery_Name")] %>% head(n=3)
kbl <- kable(max_ABV, row.names=FALSE, caption="Table 4: Highest ABV")
kable_styling(kbl, full_width=FALSE, bootstrap_options="bordered")
```

In addition, we found the top 3 IBU values to determine the state that has the most bitter beer.

```r
max_IBU <- beer_data[order(beer_data$IBU, decreasing=TRUE), c("State", "Beer_Name", "IBU", "Brewery_Name")] %>% head(n=3)
kbl <- kable(max_IBU, row.names=FALSE, caption="Table 5: Highest IBU")
kable_styling(kbl, full_width=FALSE, bootstrap_options="bordered")
```

#### ABV summary statistics

We also found the summary statistics of alcohol by volume for all the beers in the United States. We first made a data structure with these summary values, then displayed a table from them (Table 6). This includes the mean, median, minimum and maximum values of ABV across the beers.

```r
sum <- as.array(summary(beer_data$ABV)) %>% round(3)

kbl <- kable(sum, col.names=c("Statistic", "ABV Value"), caption="Table 6: ABV Summary Statistics") 
kable_styling(kbl, full_width=FALSE, bootstrap_options="bordered") %>% column_spec(1:2, width="2.75cm")
```

To graphically show the ABV summary statistics as well, we used ggplot2 to create a boxplot of the values (Figure 5).

```r
ggplot(beer_data, aes(y=ABV, x="")) + 
  geom_boxplot(na.rm=TRUE, width=0.4, color="#31394d") +
  stat_summary(fun.y=mean , na.rm=TRUE, geom="point", colour="darkred") + 
  coord_flip() + 
  labs(title="Figure 5: Alcohol Content Summary", x="", y="Alcohol by Volume (ABV)") +
  theme(plot.title = element_text(hjust=0.5))
```

#### IBU and ABV relationship

To determine whether ABV and IBU have an apparent relationship, we used ggplot2 to create a scatterplot of the paired values. The geom_smooth portion of the code plots a line through the scatterplot, which shows the linear relationship of the bitterness of beer to its alcohol content by volume.

```r
ggplot(beer_data, aes(x=IBU, y=ABV, color=IBU)) + 
  geom_point(size=1.3, na.rm=TRUE) + 
  geom_smooth(method=lm, na.rm=TRUE, se=FALSE, color="brown") +
  labs(title="Figure 6: Alcohol Content vs. Bitterness of Beers", x="International Bitterness Units (IBU)", y="Alcohol by Volume (ABV)") +
  theme(plot.title = element_text(hjust=0.5), legend.position="none") +
  scale_color_gradient(low = "#ffbf00", high = "brown")
```

After creating the Figure 6 scatterplot for alcohol content and bitterness of beers, we ran a hypothesis test to determine whether the linear relationship was significant.

```r
with(beer_data, cor.test(IBU, ABV))
```

This code provided output for calculating Pearson's product-moment correlation, with the result of 0.67 and a p-value < 0.0001. From the output we determined that the ABV and IBU linear relationship was significant.

# Conclusion

By cleaning, structuring, and manipulating the beer and brewery data as detailed above, we were able to perform analyses and provide insights to the CEO of Anheuser-Busch. A full write-up of this analysis is found in [CaseStudy1.html](http://htmlpreview.github.io/?https://github.com/mccraryk/MSDS6306-CaseStudy1/blob/master/CaseStudy1.html). 
