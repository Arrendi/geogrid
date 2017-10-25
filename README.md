<!-- README.md is generated from README.Rmd. Please edit that file -->
hexmapr
=======

Using geospatial polygons to portray geographical information can be a challenge when polygons are of different sizes. For example, it can be difficult to ensure that larger polygons do not skew how readers retain or absorb information. As a result, many opt to generate maps that use consistent shapes (i.e. regular grids) to ensure that no specific geography is emphasised unfairly. Generally there are four reasons that one might transform geospatial polygons to a different grid (or geospatial representation):

1.  We may use cartograms to represent the number of people (or any value) within a particular geography. For more information and examples see (here)\[<https://www.wired.com/2016/10/electoral-maps-look-little-different-heres/>\] and (here)\[<http://www.nytimes.com/interactive/2013/04/08/business/global/asia-map.html>\]. This cartogram approach changes the size of a particular geography in-line with the values that one seeks to visualise.
2.  We may use grids to bin data and typically visualise the spatial density of a particular variable. For an example see (here)\[<https://bl.ocks.org/mbostock/4330486>\]. 3.We may use grids to segment a geographical region. For example tesselation can be used in (biological sampling) \[<https://www.arcgis.com/home/item.html?id=03388990d3274160afe240ac54763e57>\] or even in generating (game environments)\[<https://www.redblobgames.com/grids/hexagons/>\]. 4.We may use grids to equally represent existing geographical entities (such as US states, UK local authorities, or even countries in Europe). For an example of representing US states as both regular and hexagonal grids see (here)\[<http://blog.apps.npr.org/2015/05/11/hex-tile-maps.html>\].

If you follow the link in bullet 4 you will see that both the hexagonal and regular grids were implemented by hand through discussion. Recent functionality for representing US states, European countries and World countries in a grid has been made available for ggplot2 (here) \[<https://hafen.github.io/geofacet/>\] and there are many other examples of hand specified or bespoke grids.

What I wanted to do with hexmapr is make it easier to generate these grids in ways that might be visually appealing. Using an input of geospatial polgyons hexmapr will generate either a regular or hexagonal grid, and then assign each of the polygons in your original file to that new grid.

There are three ways to assign the locations to new points on the grid (this is the contentious bit):

1.  Begin from the south, easterly most coordinate and assign each shape to its closest available grid space. Move northward in a row-wise fastion. I.e. assign the bottom row of the grid first, then the next row up...
2.  Assign grids based on their size. Smallest geographies get assigned first. In the first approach, smaller geographies tend to get 'squeezed' to the outside of the whole shape. Assigning smaller geographies first helps to mitigate this (slightly).
3.  Use the hungarian algortithm to efficiently calculate the assignments which involves the minimum distance travelled from the centroid of every geography to its new centroid on the grid. For this I have included an implementation of the Munkres algorithm kindly made available (here)\[<https://github.com/RcppCore/rcpp-gallery/blob/gh-pages/src/2013-09-24-minimal-assignment.cpp>\].

Example
-------

This is a basic example which shows how the assignment of London boroughs could work.

``` r
## basic example code
```

Notes
-----

This is my first attempt at a package and it is not correctly documented. I am in the process of doing so. Hopefully the package is small enough and the functions are simple enough that critiquing them is not too challenging.
