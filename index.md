## Introduction & Background

Our goal for this project is to investigate the relationship between crime and other socio-economic factors. We initially proposed studying how uber traffic affects crime. Due to data collection difficulties, we switched to a different problem setting. We are now investigating the relationship between crime and housing prices. It is a challenge to parse large amounts of data to find relevant information for investigation purposes with machine learning techniques being a possible solution (Nath, 2006). We want to investigate the following questions:

1. How does an increase in crime in one area affect the price of real estate in that area?
2. How do crime patterns and housing availability change over time?

## Problem Definition

Crime occurs frequently in Atlanta. As students, we must balance safety and affordability in terms of our housing options. By analyzing crime and housing data in Atlanta, we aim to provide a threat and price assessment for students as they choose where to live. Both Atlanta Police Department and Atlanta Regional Commission publish data sets related to this problem, see references.

## Data Collection

We obtained crime data from Atlanta Police Department’s website. This data ranges between the years 2009 and 2019. We also obtained home sales price data from the Atlanta Regional Commission (ARC). By cleaning the crime data, we can remove the irrelevant columns that would not be useful in K-Means or Linear Regression. We kept the longitude and latitude values of all the crime data since we plan to use those values to group the crimes by neighborhoods. We also kept the UC2_Literal column in the crime data, this labels the crime type.  

For the housing price data, we will be keeping the columns with the home sale price per sq ft in 2013 and 2018. We plan to incorporate the data with the crime score from NSA, neighborhood statistical areas, for our Linear Regression model. These NSA were created by ARC to provide natural groupings for neighborhoods. In the scope of this project, we will be ignoring the other columns since we are mainly interested in the relationship between housing and crime.   

Initially, housing data was filtered down to remove attributes that have no purpose for our problem statement. This includes features such as gross housing prices, time of crime reports, and miscellaneous identification numbers. 

## Methods

### Unsupervised Learning - K-Means

After cleaning the crime data set, we are left with only the relevant features for analysis. We will first perform is K-Means clustering. Using the longitude and latitude values of the crime data, we will group crimes that occur in close proximities. By doing so, we can extract information regarding the frequency of the types of crimes that occur with the different clusters. Since the crime data also includes an UC2_Literal column, a crime type identifier, we can label each data point with the corresponding crime.

We first tried to utilize the elbow method using the within the sum of square value to identify the optimal number of clusters. We also calculated the silhouette coefficients to validate our optimal number of clusters. Using sci-kit-learn, we were able to determine the silhouette score for each K-Means run ranging from 3 to 12 clusters. The optimal number of clusters is associated with the highest silhouette scores. Although each year prescribes a different optimal number of clusters, the mode number of clusters was 8. Finally, we ran K-Means for each year from 2009 to 2020 and plotted the K-Means graph for each year.

### Supervised Learning - Linear Regression

We have two datasets to compare: crime data provided by the Atlanta Police Department (APD) and housing price data provided by the Atlanta Regional Commission (ARC). The housing data has housing sales prices from 2013, 2017, and 2018 for City of Atlanta Neighborhood Statistical Areas (NSAs – or neighborhood clusters designed for statistical analysis). We have chosen to focus our testing on the year 2018.

The Linear Regression model will be based on sets of input/labels, where the inputs will be a "crime score" per NSA, and the labels will be home sale price per sq ft. The crime score will be tailored to different crime statistics in an NSA, such as types of crimes, number of crimes, etc. The idea of the model is:

1. Find any correlation between a crime and average housing prices. 
2. Predict average pricing of houses given a neighborhood’s rate of low and severe crimes.

Measuring crime is a difficult problem. We initially tried to assign crimes a score based on their severity. The statistical model will be based on input/output pairs of neighborhoods' "crime scores" and home sale prices per sq ft. The crime scores will range from 1 – 3, will average from the addition of individual crime categories:

1. Auto Theft, Larceny, Burglary
2. Aggravated Assault, Robbery
3. Rape, Criminal Homicide

Each neighborhood will be given a score, which will be averaged over the number of occurrences of the crime category reported.

## Results

#### K-Means Elbow Method:

![Elbow Graph](https://github.com/IvanJLeung/Housing-Crime-Analysis/blob/main/images/elbowPlot.png?raw=true)

#### Silhouette Scores:

![Silhouette Scores](https://github.com/IvanJLeung/Housing-Crime-Analysis/blob/main/images/silhouetteScore.PNG?raw=true)

#### K-Means Graph

![K-Means Graph](https://github.com/IvanJLeung/Housing-Crime-Analysis/blob/main/images/KMeansGraph.png?raw=true)

The clusters for every year are similar and thus we only provide 2020 as a reference.

#### Linear Regression Results

**Analysis on all crime scores:**

![Linear Regression Graph All](https://github.com/IvanJLeung/Housing-Crime-Analysis/blob/main/images/LRGraph.png?raw=true)

**Coefficient of # of crimes reported feature**: ~-0.132

**MSE**: 10749.80

**Analysis on crimes scored as 1:**

![Linear Regression Graph Crimes 1](https://github.com/IvanJLeung/Housing-Crime-Analysis/blob/main/images/LRGraph.png?raw=true)

**Coefficient of # of crimes reported feature**: ~0.0286

**MSE**: 7625.54

**Analysis on crimes scored as 2 or 3:**

![Linear Regression Graph Crimes 2, 3](https://github.com/IvanJLeung/Housing-Crime-Analysis/blob/main/images/LRGraph.png?raw=true)

**Coefficient of # of crimes reported feature**: ~-0.473

**MSE**: 7383.36

## Discussion

Our K-Means analysis helped us identify crime clusters based on proximity. We found a total of 8 clusters for Atlanta optimally describes crime “neighborhoods”. The elbow method gave us an initial estimate for the optimal number of clusters, and then we implemented silhouette coefficient analysis to further validate our results. The SC coefficient was highest for 8 clusters at a value of 0.4317. We performed K-Means clustering per year and we have shown the year 2020 as a reference image. We also found that time has minimal effect on our clustering.   

Some important observations were made from this analysis. Larceny is by far the most common crime, comprising about 50-80% of all the crimes for each year. The aggregated percentage of different types of crime over the years is as below:

* Larceny from Vehicle = 30.8%
* Larceny Non-Vehicle = 23.9%
* Home Burglary = 14.46%
* Auto Theft = 13.73%
* Aggravated Assault = 7.3%
* Pedestrian Robbery = 5.01%
* Non-Residential Burglary = 3.19%
* Commercial Robbery = 0.68%
* Residential Robbery = 0.65%
* Homicide = 0.29%
* Manslaughter = 0.0%

We also see a drop in home burglary over the last 10 years in clusters 2, 4, 5, and 7.

From 2009 to 2019:

* Cluster 2’s crime distribution for home burglary dropped from 29.5% to 10.43%.
* Cluster 4’s crime distribution for home burglary dropped from 26.39% to 12.58%.
* Cluster 5’s crime distribution for home burglary dropped from 28.51% to 15.47%.
* Cluster 7’s crime distribution for home burglary dropped from 27.44% to 13.44%.

This can be due to many reasons. We conjecture increased home security, advanced security systems, or police patrolling possibly decreased burglary. A total of 245 neighborhoods were sampled in this analysis and are distributed as follows:

* 22 in cluster 0
* 38 in cluster 1
* 34 in cluster 2
* 29 in cluster 3
* 34 in cluster 4
* 38 in cluster 5
* 18 in cluster 6
* 32 in cluster 7

Most of cluster 6 includes areas closer to the Georgia Tech campus.

For the preliminary Linear Regression model testing, the model was fitted on the total number of crimes per neighborhood. This was just to get a feel for how crime may indeed model housing price trends. The initial testing showed a very weak negative correlation between the number of crimes reported per neighborhood and the average housing price per square foot of that neighborhood. The hypothesis presented by the team was that the more accounted crime reports would result in lower housing prices. While these initial results appear to lean towards that assertion, the testing was naïve and did not consider appropriate feature extraction methodology. Additionally, the metric of considering the number of crimes committed may be too broad, as more crimes may not necessarily translate to the level of danger awareness in a neighborhood. For example, an area that has fewer crimes, but most of those crimes are homicides or other forms of physical assault could be less desirable than an area that has more crimes but is comprised mostly of lesser offenses such as larceny.

For the final and follow-up Linear Regression, we decided to specific the trends. We wanted to observe if the severity of the crimes committed would have any effect on housing prices. Two separate linear regressions were run: one to observe trends related to crimes scored as ‘1’ (i.e. auto theft, larceny, burglary) and another to observe trends related to crimes scored as ‘2’ or ‘3’ (i.e. aggravated assault, rape, criminal homicide, robbery). The trends observed were interesting. There was a negative correlation between housing prices and low-ranked crimes, and a positive correlation between housing prices and high-ranked crimes. This leads one to surmise that more desirable areas, even if they have a high rate of theft, are still well-priced. It should be noted that included in these locations were the neighborhoods of Buckhead and Midtown, areas which are highly affluent, but can be subject to more petty crimes. On the opposite coin, the most severe crimes did lead to a downward trend in house prices, which is more on par with what our hypothesis expected.

## Conclusion

For the crime data, we assumed that the clusters would change over the years, but it was surprising to see similar trends throughout the timeline. It was also surprising to note that only certain clusters experienced a reduction in home burglary crimes over the 10 years. This raises an interesting question and prompts further analysis to discover why areas within those clusters had reduced burglary crime and not others. We only took housing data from two years. It would be interesting to compare the housing data for the same timeline as we did for the crime data. Overall, this is a nice exploratory analysis to build future work upon. For future works, we would like to tie in the results of our K-Means analysis to our linear regression analysis and to see how housing prices impact crime types and frequencies within the different clusters. 

## Team Contributions

We planned weekly meetings from the start. Each of the team members was present in all meetings and we recorded some for later references. We all came up with ideas to discuss and settled down on the current one. We delegated work in every meeting and all members did their part. Overall, it was an effective team collaboration, and we are happy to present our work. The individual contributions are listed below:

* **Ivan**: Performed K-Means analysis on crime data, managed GitHub pages, report writing, contributions in proposal video. 
* **Eunseo**: Data cleaning on crime data, video editing for presentations, report writing. 
* **Pierre**: Performed Linear Regression on crime and housing data to observe trends, proposal (initial and midterm) report contributions. 
* **Sakshi**: Idea conception and building. Report and presentation writing, discussions with the team, research for references.
* **Michael**: Read and communicated research papers on what has been done with crime data, performed the data collection, report writing and proofreading. 

## References

Atlanta Police Department "Crime Data Downloads." Atlanta Police Department,  2021, www.atlantapd.org/i-want-to/crime-data-downloads.

Iqbal, Rizwan, et al. "An experimental study of classification algorithms for crime prediction." Indian Journal of Science and Technology 6.3 (2013): 4219-4225.

Nath, Shyam Varan. "Crime pattern detection using data mining." 2006 IEEE/WIC/ACM International Conference on Web Intelligence and Intelligent Agent Technology Workshops. IEEE, 2006.

ARC Open Data & Mapping Hub, "City of Atlanta Neighborhood Home Sales Prices & Sq Footage 2013 – 2018", Atlanta Regional Commission's Research and Analytics Group, 26 Mar. 	2020, opendata.atlantaregional.com/datasets/dd66bf7d57404a54941d7d7d835b3658.
