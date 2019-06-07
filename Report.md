# Developing neighbourhood rating system by example of the city of Toronto

## Introduction/Business Problem

It is very important to find a good place where to live, where to do business. Computer science definitely can help it. This research investigates how to build recommendations systems, that can be applied to any large city and provide information about most suitable areas to do the activities for it's users. The city of Toronto is an example how to do it. The key feature is capturing all available venues data around the city. Foursquare location data is a good opportunity fastly collect all the data. The problem to be solved is to find districts with the most advanced infrastructure. All needed places must be close with good variety. Then districts can be clustered for areas with life quality and business value above average. After all customer can explore the map with areas highlighted for their requirements.

## Data

First of all, public data for Toronto neighbourhoods are loaded. Then not assigned data are excluded. Then uses Foursquare API to load all venues for the entire city. It cannot be done instantly with single request due to lage amount of data and API limitations. Thus special approach is designed to collect the data needed. For neighbourhood its max radius is estimated. Then requests API for all venues within  radius. It's not a single request - it's a series of paged requests. Not all points belongs to current neighbourhood. Then venue points are filtered by the neighbourhood's estimated polygon. Then venues stats are calculated such as count, distinct category count and assigned to current neighbourhood in neighbourhoods dataset. After all, neighbourhoods dataset with venues stats and venues dataset with refs to neighbourhood are available.

![Map of Toronto](/Toronto_map.jpg)

In the figure above all neighbourhoods colored by borough are shown. For each borough there is a shape estimation. Shown as polygon with red borders. Bad estimated shapes are excluded and not shown. Black dots are all available venues. Venues dataset is marked with neighbourhoods they belongs to based on its shape estimation. This is primary geodata ready for further analysis.
