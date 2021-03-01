## Introduction & Background

Our goal for this project is to investigate the socioeconomic relationship between Uber rides and crime rates in Atlanta. Machine learning has also played a role in crime investigation. It is a challenge to parse large amounts of data to find relevant information for investigation purposes (Nath, 2006). Weber (2019) investigated 18 cities, finding that the introduction of Uber rides led to an overall 5% reduction in crime. The cause for this phenomenon is still speculative. We want to investigate the following questions:

1. How does an increase in crime in one area affect the frequency of Uber rides in that area?
2. How do crime and Uber ride frequencies change with time and is there a correlation?

### Problem Definition

Crime occurs frequently in Atlanta. This project will address the safety concerns that may arise for Uber drivers in terms of accepting unknown riders. By analyzing crime data and Uber ride frequencies in Atlanta, we aim to provide a threat assessment for drivers as they provide services in different areas around the city. Both Atlanta Police Department and Uber publish data sets related to this problem, see references.

### Methods

For our project, we will be using K-means for unsupervised learning and linear regression and decision trees for supervised learning.  K-means has been used before to analyze crime by clustering possibly dependent crimes (Nath, 2006). We will also utilize PCA to reduce feature dimensionality as needed. For supervised learning, both regression (Weber, 2019) and decision trees (Iqbal, 2013) have been used to investigate crime data. With linear regression, we can plot crime and Uber ride frequencies over time and analyze for similar trends.

### Potential Results

One of the potential results that we would like to show is the correlation between crime frequency in various areas around Atlanta and the number of Uber rides that occur. Additionally, by analyzing different time frames, we could also note the change in crime frequencies over the years and understand if and how Uber and its drivers have adapted to this change.

### Discussion

Our research will provide a useful tool for Uber drivers and individuals to gain insight into the crime patterns around Atlanta. This could help keep Uber employees safe as they navigate the city. The future for this project could include expansion into other cities, as we would simply need to feed data into our algorithm to obtain results.

Potential difficulties we envision facing are discerning the difference in frequency of Uber rides in a particular area. The frequency of Uber rides in an area may be completely unrelated to crime, and may have to do with other factors, such as geographic proximity, cars per capita in an area, and other various variables. Discerning these factors will be a key aspect of our goal of correlating crime dispersion with Uber traffic.

### References

Atlanta Police Department “Crime Data Downloads.” Atlanta Police Department,  2021, www.atlantapd.org/i-want-to/crime-data-downloads.

Iqbal, Rizwan, et al. "An experimental study of classification algorithms for crime prediction." Indian Journal of Science and Technology 6.3 (2013): 4219-4225.

Nath, Shyam Varan. "Crime pattern detection using data mining." 2006 IEEE/WIC/ACM International Conference on Web Intelligence and Intelligent Agent Technology Workshops. IEEE, 2006.

Uber. “Movement Cities.” Uber Movement, 2021, movement.uber.com/cities?lang=en-US.

Weber, Bryan S. "Uber and urban crime." Transportation research part A: policy and practice 130 (2019): 496-506.
