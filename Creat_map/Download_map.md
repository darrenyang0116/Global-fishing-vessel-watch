We need a vector file to create an interactive map. [Shapefile](https://en.wikipedia.org/wiki/Shapefile) format can spatially describe vector features: points, lines, and polygons, representing. Each item usually has attributes that describe it, such as country or capital city.
.
## Sourcing shapefiles

You can easily search online for shapefiles and there are many free resources for pulling down high quality ones, we use [Natural Earth Data](http://www.naturalearthdata.com) to find the worldmap we want. You can also preview the shapefile you downloaded in [mapshaper](http://mapshaper.org)


The binary shapefile we downloaded can be previewed at mapshaper, which is a fast way to see the data inside of a shapefile without needing to go through the lengthy geojson conversion process.

Drag in the .shp file to view the contents of the shapefile. You should see the UN-recognized countries rendered in black lines, with some scattered red lines indicating intersecting vectors.

Please move the entire downloaded ne_50m_admin_0_sovereignty file to your Desktop.

####Matching Plottable Dataset Download this comma-separated-value file. It contains historical data sourced from the UNHCR on Refugee countries-of-origin from 2006 to 2014, the most recent study available.

Please move the refugee.csv downloaded file inside of the ne_50m_admin_0_sovereignty directory of your Desktop.

####Code for Visualization This code will come from D3's excellent geospatial code library. We will use code similar to this example by Mike Bostock, the author of D3.
