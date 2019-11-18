# Rendering Topography

In this last project, you will revist the de facto urban areas you defined as well as the transportation infrastructure and health care facilites you spatially located.  Using your combined adm2 or adm3, you will intersect those land use, transport and health care geographies with the topography of your selected adm2 or adm3.  You may recall that we used the `rayshader::` package back in project 1, which we will use again, but this time will focus on its application with rasters rather than starting with a `sf` object.

To start, be certain you have the `raster::`,`sf::` and `tidyverse::` library of functions available for your current R worksession.  Also, install and load the `rayshader::` and `rayrender::` packages.

```text
#install.packages("rayshader", dependencies = TRUE)

library(raster)
library(sf)
library(tidyverse)

library(rayshader)
library(rayrender)
```

Use the `setwd()` command to make certain your working directory is set to the data folder where you saved your raster and shapefiles.  Read your raster file that describes the topography throughout your LMIC into RStudio.  Also read the shapefile of your adm2 or adm3s as a simple features object into RStudio.  Following are my examples for Liberia.

```text
lbr_topo <- raster("lbr_srtm_topo_100m.tif")
lbr_adm2  <- read_sf("gadm36_LBR_2.shp")
```

With the polygon you previously created by unioning the two adm2s or adm3s you selected, use the `crop()` command to crop the raster describing the topography of your LMIC.  You could also `mask()` the topographical raster, but I am going to forego that step in favor of retaining the area within the bounding box used by the `sf` from my combined adm2.

```text
combined_topo <- crop(lbr_topo, combined_adm2s)
```

  





