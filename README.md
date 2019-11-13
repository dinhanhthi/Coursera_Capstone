# ☕ Capstone project : Setting up a café in Ho Chi Minh City

- This repository is used for the [Capstone project](https://www.coursera.org/learn/applied-data-science-capstone/) on Coursera.
- Full report: https://note.dinhanhthi.com/setting-up-a-cafe-in-hcmc

## Problem's description

If you have a chance to visit Ho Chi Minh City (HCMC), you will see that it’s one of the most active cities in the world. People here love to talk, to chat everywhere. The catering services in this city, therefore, very thriving.

We need to clarify **the differences between *a coffee shop* and *a café***. The coffee shop has no similar connotations. In the United States, a café usually serves meals, while a coffee shop usually just sells snacks (muffins, scones, shortbread). This is not strictly the case, and both usually serve coffee. In this project, we suppose to work only on the café.

Although there are already a lot of cafés in HCMC, their density between districts is not uniform. There are some districts containing too many cafés while there are less in some others. If we have some knowledge about the *population density*, the *housing price* in each district coupling with an overview of *the number of cafés*, we can have a better idea to set up a new business there.

If we think of it by an investor, we expect to choose a place where the population density is high but fewer competitors. If the housing price in that place is low, it’s more attractive to us.

By using Data Science and some geometric factors about the relation between districts in HCMC, we can give good answers of following questions to the investors so that they can have a better vision about not only the café but also about other venues in HCMC.

1. **How many venues in each district?** Answering this question gives us a better understanding of *the dynamic level* of a district.
2. **How many categories in each district?** Answering this question helps us know about *the diversity in the business* of a district.
3. **How many venues in each category?** This question shows the magnitude of a category in a district.
4. **What are the most popular categories in each district?** If investors change their mind to focus on other commercial fields instead of opening a café.
5. **How many clusters we can use to categorize the districts based on the popularity of cafés?**
6. **In which districts, the average housing price is low and the number of cafés is low also?**
7. **Where there are many people but fewer cafés?**
8. Visualize all information on the map so that we can have a better look at what we want to find the answers!

## Data presentation

In order to explore the previous questions, we need to use the following data in the research.

1. [List of Ho Chi Minh City administrative units](http://bit.ly/30r0yU8) from Wikipedia. It gives us a list of all urban districts of HCMC with their area (in $km^2$), population (in 2015) and the density of each district (people/$km^2$).
2. List of the coordinates (latitude, longitude) of all urban districts in HCMC. This list can be generated based on the name of each district and package *geopy.geocoders.Nominatim*.
3. [List of average housing prices](https://mogi.vn/gia-nha-dat) per $m^2$ in HCMC.
4. A `.json` file contains all coordinates where we use it to create a choropleth map of Housing Sales Price Index of HCMC. I create this file by myself using [OpenStreetMap](https://nominatim.openstreetmap.org).

## Methodology

1.  First, we need to collect the data by scraping the table of HCMC units on the Wikipedia page and the average housing price (AHP) on a website. The **BeautifulSoup** package is very useful in this case.
2.  The column **Density** is calculated later based on columns **Population** and **Area** of each district.
3.  Throughout the project, we use **numpy** and **pandas** packages to manipulate data frames.
4.  We use **geopy.geocoders.Nominatim** to get the coordinates of districts and add them to the main data frame.
5.  We use *folium* package to visualize the HCMC map with its districts. The central coordinate of each district will be represented as a small circle on top of the city map.
6.  We use **Foursquare API** to explore the venues in each district and segment the districts based on them.
7.  For clustering the “Café" venues between districts, we use **K-Means Clustering** method and the package **scikit-learn** will help us implement the algorithm on our data. In order to indicate how many K for the method, we try with 10 different values of K from 1 to 10 and use the “elbow" method to choose the most appropriate one.
8.  In order to visualize the charts, we use package **matplotlib**.
9.  We use again the package **folium** to visualize the clusters on the main map and the choropleth map of AHP.
