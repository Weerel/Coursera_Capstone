# Developing neighbourhood rating system by example of the city of Toronto
#### Applied Data Science Capstone by IBM/Coursera
## Table of contents
* [Introduction](#introduction)
* [Data](#data)
* [Methodology](#methodology)
* [Results](#results)
* [Discussion](#discussion)
* [Conclusion](#conclusion)
## Introduction <a name="introduction"></a>
It is very important to find a good place where to live, where to do business. Computer science definitely can help it. This research investigates how to build recommendations systems, that can be applied to any large city and provide information about most suitable areas to do the activities for it's users. The city of Toronto is an example how to do it. The key feature is capturing all available venues data around the city. Foursquare location data is a good opportunity fastly collect all the data. The problem to be solved is to find districts with the most advanced infrastructure. All needed places must be close with good variety. Then districts can be clustered for areas with life quality and business value above average. After all customer can explore the map with areas highlighted for their requirements. So the target audience both as small business as ordinary citizens. One can explore the map to find best places for renting. Also it is suitable for helping to establish new public plase to do business.
## Data <a name="data"></a>
First of all, public data for Toronto neighbourhoods are loaded. Then not assigned data are excluded. Then uses Foursquare API to load all venues for the entire city. It cannot be done instantly with single request due to lage amount of data and API limitations. Thus special approach is designed to collect the data needed. For neighbourhood its max radius is estimated. Then requests API for all venues within radius. It's not a single request - it's a series of paged requests. Not all points belongs to current neighbourhood. Then venue points are filtered by the neighbourhood's estimated polygon. Then venues stats are calculated such as count, distinct category count and assigned to current neighbourhood in neighbourhoods dataset. After all, neighbourhoods dataset with venues stats and venues dataset with refs to neighbourhood are available.

![Map of Toronto](/map_polygons.jpg)
In the figure above all neighbourhoods are shown as circles. For each neighbourhood there is a shape estimation. Shown as polygon with red borders. If the shape is poorly estimated then it is not shown and neighbourhood is green. Otherwise neighbourhood is blue. Black dots are all available venues. Venues dataset is marked with neighbourhoods they belongs to based on its shape estimation. This is primary geodata ready for further analysis.
## Methodology <a name="methodology"></a>
First of all let's check dependency for venues total count and venues categories count within neighbourhoods.

![Map of Toronto](/fig_count_cat.jpg)
Figure above demonstrates it. One can see it's higly correlated. The more places available, the more it's variety. It's dependend values. Let's take into consideration only total venues count for neighbourhood.

![Map of Toronto](/fig_count_cat_cluster.jpg)

![Map of Toronto](/fig_count_volume_cluster.jpg)

![Map of Toronto](/fig_volume_density_cluster.jpg)

## Results <a name="results"></a>
section where you discuss the results.

![Map of Toronto](/map_venues_count.jpg)
![Map of Toronto](/map_density.jpg)
![Map of Toronto](/map_cluster.jpg)
![Map of Toronto](/map_cluster_detailed.jpg)

## Discussion <a name="discussion"></a>
section where you discuss any observations you noted and any recommendations you can make based on the results.
## Conclusion <a name="conclusion"></a>
section where you conclude the report.
