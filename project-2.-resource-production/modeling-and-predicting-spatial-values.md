# Modeling & Predicting Spatial Values

In this lab, you will use the model estimates in order to predict spatial values across the landscape of your selected LMIC.  To do this create a new script, install and load needed packages and libraries, and set your working directory.  Once you have your script set up to go with `sf::` , `raster::`, `tidyverse::`, `doParallel::`, and `snow::` all in place, again load your `RasterStack` into your RStudio workspace.  I named my 12 layer `RasterStack` that describes land use and land cover throughout Liberia, `lulc`, and it has the following characteristics.

![](../.gitbook/assets/screen-shot-2019-10-06-at-6.53.01-pm.png)

Also, load the `adm0` \(or international boundary\), `adm1` and `adm2` for your LMIC.  If you don't have your international boundary, go back to GADM, HDX or also look on Geoboundaries for the shapefile in order to import to your RStudio work session.

{% embed url="https://www.gadm.org" caption="Link to GADM" %}

{% embed url="https://data.humdata.org" caption="Link to HDX" %}

{% embed url="http://www.geoboundaries.org/data/1\_3\_3/zip/shapefile/" caption="Geoboundaries subdirectory with shapefiles by ISO code" %}

For this exercise, I will retrieve my shapefile from the Geoboundaries subdirectory and then use the `read_sf()` command to import the data as an object I named `lbr_int`.

You will also need the WorldPop raster later in the exercise in order to calculate a basic estimate of  spatial error.  In order to improve the predictive value of the model, I have gone back to the WorldPop raster file of Liberia for 2015, rather than 2019.  It is probably not going to have a huge impact, but if you want to try for the best results, the date value of your response variable should be the same as the date value of your geospatial covariates.

```r
lbr_pop15 <- raster("lbr_ppp_2015.tif")
```

You may have noticed when reviewing the characteristics of your `RasterStack` that many of the layers had `?` as the value for both the `min values` and `max values`.  The reason this occurred is because each of the layers within the `raster` is presenting interpretable values outside of the boundaries of our LMIC.  For example, with Liberia, you will notice that there is a large portion of the area within the plot that has an assigned value \(likely `NA`\) although it is technically not part of the raster analytical area.  In order to fix this problem, we need to use the `mask()` command to remove all of the gridcells that are not explicitly within the international border of our LMIC.

```r
yourRasterStack <- add_command_here(yourRasterStack, yourLMIC_intlborder)
```

It might take a few minutes to run the `mask()` command.  On a MBAir using the `mask()` command on a 12 layer `RasterStack` , each layer with about 25 million gridcells takes about 10 minutes.  Once the command is completed, you should now notice `min values` and `max values` when retrieving a summary of the object.

![](../.gitbook/assets/screen-shot-2019-10-06-at-7.50.14-pm.png)







