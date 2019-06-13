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

So we use neighbourhood venues count, neighbourhood area value as primary features. Additional useful feature is density = count/area.
Then features are scaled and ready for clusterization. We should choose a set of features to be clustered. The most representative set is volume and density. Let's examine feature clusterization on plot.

![Map of Toronto](/fig_volume_density_cluster.jpg)

In the figure above four clusters are shown. They are good separated and distinguish small neighbourhood with high density and large neighbourhood with low density.

Let's examine clusterization for origin features. First in count, area plot.

![Map of Toronto](/fig_count_volume_cluster.jpg)

As we can see points are coupled and not so good for clusterization. However clusters are notable.

For instance count and venues categories features are not suitable for clustering. And different clusters are not separable.

![Map of Toronto](/fig_count_cat_cluster.jpg)

## Results <a name="results"></a>
After all interactive map to view result is prepared. One can view selected features as heatmap and final clusterization. More over new features can be added as render paramerers and can be automaticly rendered on map.

Here is venues count heatmap:

![Map of Toronto](/map_venues_count.jpg)

Here is venues density heatmap:

![Map of Toronto](/map_density.jpg)

Here is final clusterization map:

![Map of Toronto](/map_cluster.jpg)

Here is the same map on another scale. Venues points are shown to show clusterization quality.

![Map of Toronto](/map_cluster_detailed.jpg)

Data on map can be more transparent. It's just a parameter for the render.

## Discussion <a name="discussion"></a>
As a result we can view all available features rendered on map. One can explore the map and choose neighbourhood to rent apartment or to do the business. One can choose by comparing different features. However the easiest way to choose neighbourhood within good clusters.
* The luxury cluster is yellow. It's right in the center of the city. Its infrastructure is very good. The are a lot of different places. They all are close. Neighbourhoods are small.
* The good cluster is red. It is bigger. Neighbourhoods are larger. But the infrastructure is still good.
* The reasonable cluster is brown. It is the biggest cluster. Neighbourhoods are much larger. But the are not so much places available.
* The oulier is black. This is outskirts of the city. Neighbourhood is the largest. Nevertheless the ase a few places available. It's not enough for good infrastructure.

## Conclusion <a name="conclusion"></a>
Neighbourhood rating system is developed. In this article results are shown by example of the city of Toronto. This work implements key features such as:
* Approach applied to any city
* Neighbourhood's area regions automatically detected
* All features can be viewed over map and switched dynamically
* Additional features can be processed and viewed easily

This work is the beginning. The next step is taking into account additional features provided by Foursquare API.


