This readme contains the following steps that were required to complete this Data Science project:
1.	Problem statement
2.	Data Collection
3.	Data Preprocessing
4.	Machine Learning
5.	Visualization
6.	Result


# Problem Statement

The Birmingham metropolitan area as of 2018 in the largest city in Alabama and is also ranked in it the top 50 of metropolitan statistical areas in the United States [5]. Also, with the University of Alabama at Birmingham being established in the 1970s, it helped spark a growth of diversity in Birmingham. As a result, today Birmingham is the most racially and ethnically diverse city in Alabama [8]. As of 2018, the Birmingham metropolitan area population (corresponding to Greater Birmingham) was estimated at 1,151,801, which is the most populous of any city in Alabama and accounts for 25% of the state’s population [6]. The city of Birmingham itself, is the largest urban area in Alabama with 210,710 inhabitants as of 2018. The population density is 1,453/sq mi. [7]. 
 	Birmingham is a city with a high population and population density. From the perspective of a Real Estate investor we want to invest in such places where the housing prices are low and the facilities i.e. shops, restaurants, parks, hotels, etc. and social venues are nearby. Keeping the things mentioned previously in mind it is very difficult for an individual to find such a place in such a big city and to gather this much information.
	When we consider all these problems, we can create a map and information chart where the real estate index is placed on the Birmingham metropolitan area as a whole and clustered those inner cities according to the venue density.


# Data Collection

To consider the above problem the data is collected as following:
* I found a list inner cities and zip codes as they relate to the Birmingham metropolitan area from BestPlaces.net which is a website created to offer information about cities and zip codes in the United States [1].
* For housing prices, I searched and found a great local real estate website where latest Birmingham metropolitan area house prices were available with zip codes [2].
* I used Forsquare API to get the most common venues of given Birmingham metropolitan area [3].
* For choropleth maps I used .geojson file of Birmingham zrea zip code boundaries [4].


# Data Preprocessing

First of all, the data scraped from Bestplaces.net with the use of Gazpacho which is a web scraping library and then have the data clean from its raw data format.

![Alt text](https://github.com/FrederickWilliams/MSDS692-Data-Science-Practicum/blob/master/MSDS692%20Data%20Science%20Practicum/data_pics/pic1.png)

Then, I removed all the hyperlinks and there are more than one zip code for some locations (mainly Birmingham itself) so I decided to keep them to ensure fairness because like in all major metropolitan areas, there are good and bad parts of it

![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic2.png)

The next source of data the I retrieved was that of the housing prices and that the data initially looked like this:

![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic3.png)

Again, after some data processing, I was able to convert this raw json data into a readable data frame.

![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic4.png)

However, this data frame needs to be cleaned and to do that I removed all null values and then get rid of unwanted columns and only kept columns consisting of  the “City”, “Zip_Code” and “Price” which I later named these columns. In addition, the “Price” column data type was a string, so I converted it to a numeric.

![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic5.png)

After cleaning two tables I performed inner join and merge two tables on their zip codes and from resulting table, it produced double cities. So, I dropped “City_x” column and renamed and made “City_y” the main city column.

Before | After
--- | --- |
![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic6a.png) | ![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic6b.png) |

Then by using geocoder library I find the longitudes and latitudes of the inner-city locations and added each as a column to my data frame.

![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic7.png)

I used python Folium library to visualize geographic details of the Birmingham metropolitan area and I created a map of the Greater Birmingham superimposed on top. I used latitude and longitude values to get the visual as below:

![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic8.png)

Next, I utilized the Foursquare API to explore the inner cities of Greater Birmingham and segment them. I designed the limit as 100 venue and the radius 500 meter for each city from their given latitude and longitude information. Here is a head of the list venues name, category, latitude and longitude information from Foursquare API.

![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic9.png)

I repeat the process for all location and venue count of each locations etc. are: 

![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic10.png)

Finally, by using the Foursquare API in conjunction with the created datasets, a table of most common visited venues of the Greater Birmingham inner cities is generated.

![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic11.png)

# Machine Learning 

We have some common venue categories in boroughs. In this reason I used unsupervised learning K-means algorithm to cluster the boroughs. K-Means algorithm is one of the most common cluster method of unsupervised learning.
First, I will run K-Means to cluster the inner cities into 5 clusters because the county (Jefferson county) which Greater Birmingham resides in has five county commissioners. As a result, when I analyze the K-Means with elbow method it ensured me the 5 degree for optimum k of the K-Means.


![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic12.png)

Then I merged table with cluster labels for each inner city and after examining each cluster I label each cluster as follows:
1.	Mixed Social Venues
2.	Hotels and Social Venues
3.	Stores and Plazas
4.	Parks and Historic places
5.	Sports and Recreations
6.	Restaurants and Bars 

I also visualize house prices of each location:


![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic13.png)

As it seems in above histogram, we can define the ranges as below:

*	(>)730000 : 'Low level'
*	730000 - 1460000 : 'Average level'
*	1460000 – 2180000 : 'Above Average'
*	2180000 – 2910000 : 'High level 1'
*	(<)2910000 : 'High level 2'

Resulting table:


![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic14.png)

# Visualization

First, I visualize the cluster and you can see the clustered map below:

![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic15.png)

1.	Red (cluster 0)
2.	Purple (cluster 1)
3.	Blue (cluster 2)
4.	Cyan (cluster 3)
5.	Orange (cluster 4)

Next, I visualize the Average house pricing on the map by using Folium choropleth map and clusters on the top.


![Alt text](C:/Users/frede/OneDrive - Regis University/MSDS_692/data_pics/pic16.png)

# Result

I came to the result that the house prices in the southeast and with Hotels and Social venues nearby are very high you can clearly visualize in the map above while in the suburbs and the neighborhoods away from the city center have lower prices but the facilities are also good. Almost all low-price neighborhoods are close to restaurants, bars, sports facilities etc. Some inner cities such as Mountain Brook, and Vestavia Hills and Hoover have very high house prices. Bessemer, Fairfield, and Westside Birmingham have very low house prices but have good venues to visit nearby.

## Conclusion

As people are turning to big cities to start a business or work. For this reason, people can easily interpret where to live with all facilities and cheaply. Not only for investors but also city managers can manage the city more regularly by using similar data analysis types or platforms.

### References

1.	Sperling, Bert. (2020). Birmingham-Hoover Metro Area, Alabama: 119 Zip Codes. Retrieved January 20, 2020, from https://www.bestplaces.net/docs/team.aspx

2.	https://www.findbirminghamproperties.com/

3.	https://developer.foursquare.com/

4.	Williams, B. (2018, April 18). Birmingham Area Zipcode Boundaries. Retrieved February 25, 2020, from https://data.birminghamal.gov/dataset/birmingham-area-zipcode-boundaries

5.	Data Access and Dissemination Systems (DADS). (2010, October 5). American FactFinder - Results. Retrieved February 28, 2020, from https://factfinder.census.gov/faces/tableservices/jsf/pages/productview.xhtml?src=bkmk

6.	Nag, O. S. (2018, December 14). The 10 Largest Cities In Alabama. Retrieved March 1, 2020, from https://www.worldatlas.com/articles/what-are-the-10-largest-cities-in-alabama.html

7.	Birmingham Population. (2020, February 17). Retrieved March 1, 2020, from http://worldpopulationreview.com/us-cities/birmingham/

8.	Birmingham, Alabama. (2020, March 1). Retrieved March 1, 2020, from https://en.wikipedia.org/wiki/Birmingham,_Alabama#Arts_and_culture



```python

```
