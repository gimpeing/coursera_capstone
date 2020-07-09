# Capstone Project - The Battle of Neighborhoods
**Capstone Project**: Nursing home coverage in Singapore
*Applied Data Science Capstone by IBM/Coursera
July 2020*


## Problem Statement

Singapore, like many developed countries, is facing the challenge of a rapidly **aging population** and the **increasing need to provide long-term care services for elderly in the community**. Ideally, family members are the first line of support and care for the elderly. However, long term care facilities like nursing home is in demand to care for elderly that required constant medical and/or nursing supervision.   

The **goal** of this project is to understand the nursing home coverage in Singapore. Which are has the most nursing home? Is nursing home roughly distributed to all planning area? Are there any particular subzone in any of the planning area is relatively having lower nursing home coverage, based on demographic trait? If yes, any strategic location to recommand for new nursing home facilities? There are the questions that I would like to find the answer in this project.

**Target audience**
The outcome would be good information for both general public as well as government agencies. MOH, nursing home operator, social service agencies is able to prioritze resources to target neighborhood with low nursing home coverage.


## Executive Summary

1. [Introduction: Business Problem (Week 1)](#Problem-Statement)
2. [Data Collection (Week1)](#Data-Collection)
3. [Methodology (Week2)](#Methodology)
4. [Results and Discussion (Week2)](#Results-and-Discussion)
5. [Recommendation and Conclusion (Week2)](#Recommendations-and-Conclusions)


## Data Collection

In this project, five different datasets were collected and used to solve the problem. They are listed below:
1. List of **planning areas** of Singapore. There are total of 55 planning areas. `Population density` for each planning area will be used. In addition, coordinates for each planning area will be compiled via geocoding.
2. Singapore **demographics**. `Population` for different `age group` from subzone for each planning area will be used.
3. Singapore **boundary**. `Polygon` for each planning area and subzone from each planning area will be used.
4. List of **nursing home**. `Coordinates` for each nursing home will be used to visualize their distribution across Singapore.
5. List of `top popular places` for each planning area to obtain via Foursquare location data. The data will be used to segregate the 55 planning area and groups them into **clusters**.


## Methodology
### Exploratory Analysis and Visualization
Singapore map and its' demographics pattern across different planning areas was plotted using `folium`. Exploratory analyis based on the aggregated demographics trait were used to understand the population trend of Singapore. Nursing home distribution data are added to the analysis to find out the relationship between number of senior age group (>=65 years old) population and number of nursing home per planning area.

### Clustering analysis
Planning areas are goups into cluster by **k-means clustering** using their nearby places scraped from FourSquare API as their X-features. The number of clusters is set using *silhoutte* method. Scope of analysis was narrowing down to the cluster that at least one of its' planning area has nursing home. Linear relationship between number of nursing home and senior age group population was established. Based the data, *outliers* (i.e. the planning area) where it shows relatively lower number of nursing home based on its senior age group population were identified.

### Coverage analysis
Nursing home coverage is defined as **1km radius** from the location of each nursing home. Visualization on the map plus data analysis zooming into the subzones that fall outside the coverage areas, and their demographics trait are used to infer and recommend subzone that need additional nursing home.


## Results and Discussion
Data from earlier section were compiled and plotted in map. It consists of:
- Senior age group (>=65 years old) demographics (for each subzone) on choropleth map
- Marker for each subzone (*dots in orange color*)
- Nursing home, all are added to the map via `MarkerCluster`
- 1km radius coverage area for every nursing home (*circle in blue*)
- 8 clusters from kmeans clustering (*circle in 8 different color*)

**Three** subzones are detected to be potentially have higher demand of nursing home. They are **Bedok North, Hong Kah, and Tampines West**.


## Recommendations and Conclusions
The objective of this project is to understand the current nursing home coverage in Singapore and to find out is there area that is relatively low in nursing home coverage. Results from previous section recommended **three** subzones that are outside the 1km radius coverage and could potentially having high demand for nursing home. They are **Bedok North, Hong Kah, and Tampines West** identified based on:
1. Outside 1km nursing home coverage
2. High senior age group population especially, among those outside the coverage area
3. High medium age group population
Medium age group population is taken into consideration is due to mass majority of them could be the sandwich generation that needs to care for their aging parents. In addition, nursing home model that is closer to community with greater emphasis on fostering home-like environment could enrich the senior residents' quality of life.

However, my analysis does not taken into account the capacity of each nursing home, and the land price for new nursing home, which are deem to be important factors to be considered


## Reference
- [Planning areas of Singapore](https://en.wikipedia.org/wiki/Planning_Areas_of_Singapore)
- [Nursing homes of Singapore](https://www.healthhub.sg/directory/nursing-homes)
- [Department of Statitistics Singapore's website](https://www.singstat.gov.sg/find-data/search-by-theme/population/geographic-distribution/latest-data)
- [News](https://www.straitstimes.com/singapore/sufficient-capacity-to-meet-demand-in-aged-care-says-moh-in-response-to-lien-foundation)
- [Everyting you need to know about nursing homes in Singapore](https://www.income.com.sg/blog/nursing-homes-in-singapore)
- [Woring with Geospatial Data](https://residentmario.github.io/geoplot/user_guide/Working_with_Geospatial_Data.html)
