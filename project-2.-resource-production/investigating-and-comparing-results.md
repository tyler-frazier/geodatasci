# Investigating and Comparing Results

Load all of your covariates, import your adm0 \(international boundary\) to `crop()` and `mask()` your `RasterBrick` and then use `writeRaster()` to save it.  Later, use the `brick()` function to import your `RasterBrick` to your RStudio work session as needed.  Make sure the layers in your `RasterBrick` are named after using the `brick()` command.  Use the `names()` command to name your layers.

```r
f <- list.files(pattern="lbr_esaccilc_dst", recursive=TRUE)
lulc <- stack(lapply(f, function(i) raster(i, band=1)))
nms <- sub("_100m_2015.tif", "", sub("lbr_esaccilc_", "", f))
names(lulc) <- nms
topo <- raster("lbr_srtm_topo_100m.tif")
slope <- raster("lbr_srtm_slope_100m.tif")
ntl <- raster("lbr_viirs_100m_2015.tif")
lulc <- addLayer(lulc, topo, slope, ntl)
names(lulc)[c(1,10:12)] <- c("water","topo","slope", "ntl")

lbr_adm0  <- read_sf("gadm36_LBR_0.shp")

lulc <- crop(lulc, lbr_adm0)
lulc <- mask(lulc, lbr_adm0)

writeRaster(lulc, filename = "lulc.tif", overwrite = TRUE)
# lulc <- stack("lulc.tif")
lulc <- brick("lulc.tif")

names(lulc) <- c("water", "dst011" , "dst040", "dst130", "dst140", "dst150", 
                 "dst160", "dst190", "dst200", "topo", "slope", "ntl")
```

Obtain the 2015 WorldPop persons per pixel file for your LMIC.  Make sure your adm `sf` object has the total population per subdivision as well as its area and density.  Summarize all twelve geospatial covariates in adm groups by `sum` and by `mean`.  Modify the following code to create your adm2 or adm3 object \(you only have to select one, in the following example I have selected adm3 for Liberia\).

```r
lbr_pop15 <- raster("lbr_ppp_2015.tif")
# lbr_adm1  <- read_sf("gadm36_LBR_1.shp")
# lbr_adm2  <- read_sf("gadm36_LBR_2.shp")
lbr_adm3  <- read_sf("gadm36_LBR_3.shp")

# ncores <- detectCores() - 1
# beginCluster(ncores)
# pop_vals_adm1 <- raster::extract(lbr_pop15, lbr_adm1, df = TRUE)
# pop_vals_adm2 <- raster::extract(lbr_pop15, lbr_adm2, df = TRUE)
# pop_vals_adm3 <- raster::extract(lbr_pop15, lbr_adm3, df = TRUE)
# endCluster()
# save(pop_vals_adm1, pop_vals_adm2, pop_vals_adm3, file = "lbr_pop_vals.RData")

load("lbr_pop_vals.RData")

# totals_adm1 <- pop_vals_adm1 %>%
#   group_by(ID) %>%
#   summarize(pop15 = sum(lbr_ppp_2015, na.rm = TRUE))
# 
# lbr_adm1 <- lbr_adm1 %>%
#   add_column(pop15 = totals_adm1$pop15)
# 
# lbr_adm1 <- lbr_adm1 %>%
#   mutate(area = st_area(lbr_adm1) %>%
#            set_units(km^2)) %>%
#   mutate(density = pop15 / area)

# totals_adm2 <- pop_vals_adm2 %>%
#   group_by(ID) %>%
#   summarize(pop15 = sum(lbr_ppp_2015, na.rm = TRUE))
# 
# lbr_adm2 <- lbr_adm2 %>%
#   add_column(pop15 = totals_adm2$pop15)
# 
# lbr_adm2 <- lbr_adm2 %>%
#   mutate(area = st_area(lbr_adm2) %>%
#            set_units(km^2)) %>%
#   mutate(density = pop15 / area)

totals_adm3 <- pop_vals_adm3 %>%
  group_by(ID) %>%
  summarize(pop15 = sum(lbr_ppp_2015, na.rm = TRUE))

lbr_adm3 <- lbr_adm3 %>%
  add_column(pop15 = totals_adm3$pop15)

lbr_adm3 <- lbr_adm3 %>%
  mutate(area = st_area(lbr_adm3) %>% 
           set_units(km^2)) %>%
  mutate(density = pop15 / area)

#save(lbr_adm1, lbr_adm2, lbr_adm3, file = "lbr_adms.RData")

# lulc <- brick("lulc.tif")

# names(lulc) <- c("water", "dst011" , "dst040", "dst130", "dst140", "dst150", 
#                 "dst160", "dst190", "dst200", "topo", "slope", "ntl")

# ncores <- detectCores() - 1
# beginCluster(ncores)
# lulc_vals_adm1 <- raster::extract(lulc, lbr_adm1, df = TRUE)
# lulc_vals_adm2 <- raster::extract(lulc, lbr_adm2, df = TRUE)
# lulc_vals_adm3 <- raster::extract(lulc, lbr_adm3, df = TRUE)
# endCluster()
# save(lulc_vals_adm1, lulc_vals_adm2, lulc_vals_adm3, file = "lulc_vals_adms.RData")

load("lulc_vals_adms.RData")

# lulc_ttls_adm1 <- lulc_vals_adm1 %>%
#   group_by(ID) %>%
#   summarize_all(sum, na.rm = TRUE)

# lulc_ttls_adm2 <- lulc_vals_adm2 %>%
#   group_by(ID) %>%
#   summarize_all(sum, na.rm = TRUE)

lulc_ttls_adm3 <- lulc_vals_adm3 %>%
  group_by(ID) %>%
  summarize_all(sum, na.rm = TRUE)

lulc_means_adm3 <- lulc_vals_adm3 %>%
  group_by(ID) %>%
  summarize_all(mean, na.rm = TRUE)

# lbr_adm1 <- bind_cols(lbr_adm1, lulc_ttls_adm1)
# lbr_adm2 <- bind_cols(lbr_adm2, lulc_ttls_adm2)

lbr_adm3 <- bind_cols(lbr_adm3, lulc_ttls_adm3, lulc_means_adm3)

save(lbr_adm3, file = "lbr_adm3.RData")
```

Load your geospatial covariate `RasterBrick` of land use and land cover `lulc`, your 2015 WorldPop `raster` and  your adm `sf` object.  View your adm `sf` object and notice that you now have two summary sets of columns that describe each of your twelve geospatial covariates.  The first set of columns describes the sum of all values per adm while the second set describes the mean of all values per adm.  Also notice that in the second set, each variable  has had the number 1 added to its name to differentiate it from the first series.

Use the `lm()` function to estimate three models.  First use `pop15` as the response variable and the `sum` of each geospatial covariate per adm as the predictors.  Second, again use `pop15` as the response variable but this time instead use the `mean` of each geospatial covariate per adm as the predictors.  Third, use the logarithm of 2015 population `log(pop15)` as the response and the `mean` of each geospatial covariate per adm as the predictors.  Notice I created a new variable named `logpop15` but you could just as easily have specified `log(pop15)` within the call of your model.

```r
model.sums <- lm(pop15 ~ water + dst011 + dst040 + dst130 + dst140 + dst150 + dst160 + dst190 + dst200 + topo + slope + ntl, data=lbr_adm3)
model.means <- lm(pop15 ~ water1 + dst0111 + dst0401 + dst1301 + dst1401 + dst1501 + dst1601 + dst1901 + dst2001 + topo1 + slope1 + ntl1, data=lbr_adm3)

lbr_adm3$logpop15 <- log(lbr_adm3$pop15)
model.logpop15 <- lm(logpop15 ~ water1 + dst0111 + dst0401 + dst1301 + dst1401 + dst1501 + dst1601 + dst1901 + dst2001 + topo1 + slope1 + ntl1, data=lbr_adm3)
```

Check the summary output from each model.

```r
summary(model.sums)
summary(model.means)
summary(model.logpop15)
```

Make sure the names of each layer in your `RasterBrick` matches the names of the independent variables in each of your models.  Notice how the second two models use the `mean` of each geospatial covarariate and the layer names are modified accordingly to match.

```r
names(lulc) <- c("water", "dst011" , "dst040", "dst130", "dst140", "dst150", "dst160", "dst190", "dst200", "topo", "slope", "ntl")
lulc1 <- lulc
names(lulc1) <- c("water1", "dst0111" , "dst0401", "dst1301", "dst1401", "dst1501", "dst1601", "dst1901", "dst2001", "topo1", "slope1", "ntl1")
```

Use the `predict()` function from the `raster::` package with the appropriate `RasterBrick` and `model` to predict each gridcells value.  Use the `save()` and then the `load()` command in order to reduce computation time after restarting your work session. 

```r
predicted_values_sums <- raster::predict(lulc, model.sums)
predicted_values_means <- raster::predict(lulc1, model.means)
predicted_values_logpop15 <- raster::predict(lulc1, model.logpop15)

#save(predicted_values_sums, predicted_values_means, predicted_values_logpop15, file = "predicted_values.RData")
```



```r
ncores <- detectCores() - 1
beginCluster(ncores)
pred_vals_adm3_sums <- raster::extract(predicted_values_sums, lbr_adm3, df=TRUE)
pred_vals_adm3_means <- raster::extract(predicted_values_means, lbr_adm3, df=TRUE)
pred_vals_adm3_logpop15 <- raster::extract(predicted_values_logpop15, lbr_adm3, df=TRUE)
endCluster()

save(pred_vals_adm3_sums, pred_vals_adm3_means, pred_vals_adm3_logpop15, file = "predicted_values_adm3s.RData")

```



















