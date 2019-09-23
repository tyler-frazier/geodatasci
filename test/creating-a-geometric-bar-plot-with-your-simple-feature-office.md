# Creating a Geometric Bar Plot with your Simple Feature office

In the previous exercise, you extracted population data from a raster, and then aggregated these totals to the first level administrative area of your selected LMIC.  You then added this new column describing the population of each first level administrative subdivision to your simple feature object.  Now we are going to use that newly created column as the basis for generating a geometric bar plot of population, share of population and density by first level adminsitrative subdivision.

First, rerun the code you used to create your adm1 `sf` class object in R, including the newly added population column.  Click on the View grid symbol to the right of the data object in the top right RStudio pane under the environment tab.  When the data viewer appears in the top left pane, it should look something like the following.

![Viewer displaying the attributes of an sf object](../.gitbook/assets/screen-shot-2019-09-22-at-9.19.22-pm.png)

