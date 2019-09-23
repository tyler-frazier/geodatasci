# Creating a Geometric Bar Plot with your Simple Feature object

In the previous exercise, you extracted population data from a raster, and then aggregated these totals to the first level administrative area of your selected LMIC.  You then added this new column describing the population of each first level administrative subdivision to your simple feature object.  Now we are going to use that newly created column as the basis for generating a geometric bar plot of population, share of population and density by first level adminsitrative subdivision.

First, rerun the code you used to create your adm1 `sf` class object in R, including the newly added population column.  Click on the View grid symbol to the right of the data object in the top right RStudio pane under the environment tab.  When the data viewer appears in the top left pane, it should look something like the following.

![Viewer displaying the attributes of an sf object](../.gitbook/assets/screen-shot-2019-09-22-at-9.19.22-pm.png)

Confirm that your `sf` object has the name of each first level administrative subdivision as well as the population data you calculated and introduced.  Then use the `save()` command to save your `sf` object to your working directory.

```r
save(your_adm1_obj, file = "name_of_the_file_you_save.RData")
```

Once you have run the `save()` command you should be able to find your newly created `.RData` file in your working directory.  After you have saved the `.RData` file containing your  `sf` class object, create a new script in RStudio, and save it to your working directory.

As you have done with your prior scripts, start with the `rm()` command to clean the workspace, followed with `install.packages()` which are normally all commented off with the `#` at the beginning of each line and then the `library()` command, in order to load your needed libraries of commands.

```r
rm(list=ls(all=TRUE))

# install.packages("tidyverse", dependencies = TRUE)
# install.packages("sf", dependencies = TRUE)

library(tidyverse)
library(sf)
 
setwd("~/your/working/directory/for_data")
```

Once you have loaded the `tidyverse::` and `sf::` libraries as well as set your working directory, use the `load()` command to load into your workspace the `.RData` file that contains your adm1 `sf` class object with the newly created `pop19` variable \(column\).

```r
load("name_of_the_file_you_saved.RData")
```

One you have executed this command you should notice your adm1 `sf` object reappear in the top right pane under the environment tab.

Next, we are going to add two new columns to our adm1 object, first is a column that provides us with the area in square kilometers and the second is a column that describes the density of each first level administrative subdivision of your LMIC.  In order to add these two columns, we will use the `%>%` operator followed by the `mutate()` function.  The `mutate()` command is part of the tidyverse syntax and is used to create a new variable which is calculated from data found in another variable.  As part of the argument within the `mutate()` command, you will give the new column that you are creating a name.

Start with just the name of your adm1 object, the pipe operator and newly created column which we will name `area`.  In order to calculate this newly created column, we will also use a new command from the `sf` library of functions called `st_area()`.  

```r
yourLMIC_adm1 <- yourLMIC_adm1 %>%
  mutate(area = sf::new_command_here(yourLMIC_adm1))
```

After you execute this command, view the data associated with yout adm1 object and confirm that you have a new column named `area`. 

![](../.gitbook/assets/screen-shot-2019-09-22-at-10.15.28-pm.png)

















