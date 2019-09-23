# Creating a Geometric Bar Plot with your Simple Feature object

In the previous exercise, you extracted population data from a raster, and then aggregated these totals to the first level administrative area of your selected LMIC.  You then added this new column describing the population of each first level administrative subdivision to your simple feature object.  Now we are going to use that newly created column as the basis for generating a geometric bar plot of population, share of population and density by first level adminsitrative subdivision.

Rerun the code you used to create your adm1 `sf` class object in R, including the newly added population column.  Click on the `View()` grid symbol to the right of the data object in the top right, RStudio pane under the environment tab.  When the data viewer appears in the top left pane \(beside your script tab\), it should look something like the following.

![Viewer displaying the attributes of an sf object](../.gitbook/assets/screen-shot-2019-09-22-at-9.19.22-pm.png)

Confirm that your `sf` object has the name of each first level administrative subdivision as well as the population data you calculated and introduced.  Then use the `save()` command to save your `sf` object to your working directory.

```r
save(your_adm1_obj, file = "name_of_the_file_you_save.RData")
```

Once you have run the `save()` command you should be able to find your newly created `.RData` file in your working directory.  Please keep in mind that this `.RData` file will be different from the one you previously saved that contained the results from your `extract()` , therefor be certain to name it differntly, or else you may write over your previous saved `.RData` file, and effectively erasing it.  Save the `.RData` file containing your  `sf` class object.  Create and name a new script in RStudio, while saving it to your working directory.

As you have done with your prior scripts, start with the `rm()` command to clean the workspace, followed with `install.packages()` which are normally all commented off with the `#` at the beginning of each line and then the `library()` command, in order to load your needed libraries of commands.

```r
rm(list=ls(all=TRUE))

# install.packages("tidyverse", dependencies = TRUE)
# install.packages("sf", dependencies = TRUE)

library(tidyverse)
library(sf)
 
setwd("~/your/working/directory/for_data")
```

Open the `tidyverse::` and `sf::` libraries and set your working directory.  Use the `load()` command to import the `sf` object contained within your  `.RData` file into your workspace.  

```r
load("name_of_the_file_you_saved.RData")
```

After you have executed the above command, you should notice your adm1 `sf` object reappear in the top right pane under the environment tab.  Confirm the newly created `pop19` variable is present in your `sf` class object by using the `View()` command or data viewer.

Add two new columns to your adm1 object.  First will be a column that provides us with the area of each first level administrative subdivision unit in square kilometers, while the second column will describe density of your LMIC.  In order to add these two columns, we will use the `%>%` operator followed by the `mutate()` function.  The `mutate()` command is part of the tidyverse syntax and is used to create a new variable which is calculated from data found in another variable.  As part of the argument within the `mutate()` command, you will give the new column that you are creating a name.

Start with the name of your adm1 object followed by the pipe operator, which you will assign to the same named adm1 object, thus writing over and replacing it with the newly incorporated and created columns. The first newly created column will be named `area`.  In order to calculate this newly created column, we will also use a new command from the `sf` library of functions called `st_area()`.  

```r
yourLMIC_adm1 <- yourLMIC_adm1 %>%
  mutate(area = sf::new_command_here(yourLMIC_adm1))
```

After you execute this command, view the data associated with yout adm1 object and confirm that you have a new column named `area`. 

![The last two columns of your adm1 object](../.gitbook/assets/screen-shot-2019-09-22-at-10.15.28-pm.png)

While these area calculations are accurate, to describe a country in square meters is probably not the most useful unit to select.  Instead of meters squared, we will convert our unit of measurement to square kilometers.  In order to do this, we must first install a new library of functions for use in RStudio.  Install the `units::` package and use the `library()` command in order to make it available for use.

The command we need from the `units::` package is `set_units()`, although this time we will nest our command within a `%>%` to modify the units of measurement from `m^2` to `km^2`.  Notice how the last parenthesis doesn't coorespond with the new command from the `units::` library but rather with the parenthesis from the prior line.  We specify our syntax in this manner since we are applying the `set_units()` command to the results which have been _piped_  from the `st_area()` command.

```r
yourLMIC_adm1 <- yourLMIC_adm1 %>%
  mutate(area = sf::new_command_here(yourLMIC_adm1) %>% 
           units::new_command_here(new_units))
```

The second step in creating our two new columns is to use the `area` variable _on the fly_ to calculate a column named `density` .  This second new column will be the result of our `area` column divided by the `pop19` variable \(which we created in the last exercise\).  

```r
yourLMIC_adm1 <- yourLMIC_adm1 %>%
  mutate(area = sf::new_command_here(yourLMIC_adm1) %>% 
           units::new_command_here(new_units)) %>%
  mutate(density = numerator_variable / denominator_variable)
```

Since we have modfied the units, you should notice both the variables `area` and `density` being described in units of persons per square kilometer.

![Three newly created spatial, descriptive statistical variables](../.gitbook/assets/screen-shot-2019-09-22-at-10.39.17-pm.png)

That is all the data we need for now.  Start the creation of your geometric bar plot by first piping `%>%`  your adm1 object to a newly specified `ggplot` object.  Add the aesthetics to your `ggplot` object using the `ggplot()` command and specifying the  `x` and `y` variables from your `sf` class object.  These `x` and `y` objects will be used to plot the values using the `x` and `y` axes \(although we will flip the horizontal to the verticle and _vice-versa_ in a moment\).

Since we are generating a bar plot, we will use the `geom_bar() +` command.  Include the `stat = "identity"` argument to plot the values of individual units of observation, in this case the population of each first level administrative subdivision from your LMIC.  Also add a `color =`  argument to your `geom_bar()` command and set the width of each bar.  Following the `geom_bar()` command, use the `coord_flip()` to flip the county names along the xaxis and give them a verticle disposition.

```r
yourLMIC_adm1 %>%
  ggplot(aes(x=your_adm1_names, y=pop19)) +
  geom_bar(stat="identity", color="color", width=value) +
  coord_flip() +
  xlab("label") + ylab("label")
```

![](../.gitbook/assets/rplot03%20%281%29.png)

Let's order our counties in accordance with population size from largest to smallest in order to more easily associate the descriptive statistics presented in our bar plot with the spatial descriptive statistics we previosuly created with our map.  Add a second `%>%` after your adm1 object, where you will reorder the adm1 names based on the variable `pop19`.  Use the `mutate()` command again to write over the existing variable for adm1 names.  The key command you are adding within the `mutate()` argument is `fct_reorder()` which will change the order of the first named variable \(in this case `admin1name`\) based on the descending rank order of the second variable \(`pop19`\).  While I am using the raw population counts to change the county order listed along the verticle axis, you could use also the `area` or `density` variables.

```r
yourLMIC_adm1 %>%
  mutate(admin1name = fct_reorder(admin1name, pop19)) %>%
  ggplot(aes(x=your_adm1_names, y=pop19)) +
  geom_bar(stat="identity", color="color", width=value) +
  coord_flip() +
  xlab("label") + ylab("label")
```

In addition to changing the order of the adm1 names, also add an annotation to each bar that indicates the share of the total population located within that subdivision.  Use the `geom_text()` command to add labels to your bar plot and set the `label =`  argument within the `aes()` parameter in order to calculate each administrative units share of the total population.  Divide the `sum()` of `pop19` variable in the denominator by the raw `pop19`  counts as the numerator.  Place the division of these values within the `percentage()` command from the `scales::` library \(you'll need to install this new package\).

Place the value that describes each administrative unit's share of the total population within the center of each bar using the `position =` .  Set it using the `position_stack(vjust = 0.5)` command with a verticle adjust to the center of the bar \(half the total width\).  Also, decrease the size of the text annotations.

```r
  geom_text(aes(label=percent(pop19/sum(pop19))),
            position = position_stack(vjust = 0.5),
            size=2.0)
```

![](../.gitbook/assets/rplot01%20%282%29.png)

The last step of creating our geometric bar plot is to add a `fill =`  argument to the `ggplot(aes())` command that will be used to map a color to each counties population total, based on its place along the continuous scale from maximum to minimum.  As we did with our spatial description of population, also add the `scale_fill_gradient()` command to define colors that will coorespond to the `low =` and `high =`  values.  Use your assignment operator to create a new ggplot object that will be plotted with spatial description of your LMIC.

```r
yourLMIC_bplt <- yourLMIC_adm1 %>%
  mutate(admin1name = fct_reorder(admin1name, pop19)) %>%
  ggplot(aes(x=admin1name, y=pop19, fill = pop19)) +
  geom_bar(stat="identity", color="color", width=value) +
  coord_flip() +
  xlab("label") + ylab("label") +
  geom_text(aes(label=percent(pop19/sum(pop19))), 
            position = position_stack(vjust = 0.5),
            color="black", size=2.0) +
  scale_fill_gradient(low = "yellow", high = "red")
```

![](../.gitbook/assets/rplot02%20%281%29.png)

Return to the spatial plot that you created in the last exercise.  Copy the snippet of code that you used with the `geom_sf(aes(fill = pop19))` command in order to plot the population of every first level administrative subdivision along a contiuous scale for your LMIC.  Paste this snippet into your new script.  Add a new line to the snippet where you use the `geom_sf_text()` command to set plot the density of each individual adm1 object beneath its name.  Use the `aes(label=command(variable,2)` argument to add the `density` values.  Also, use the `round()` command, so the values from this variable are limited to two decimal points.  Nudge the density values, so they appear benath each label, while also modifying their size and color.

```r
  geom_sf_text(aes(label=round(add_variable_here, 2)),
            color="color", size=add_size, nudge_y = add_value) +
```

![](../.gitbook/assets/rplot05.png)

Finally, install the package `ggpubr` and use the command `ggarrange()` to arrange your two plots together side by side.

```r
liberia <- ggarrange(your_spatial_plot, your_bar_plot, nrow = 1, widths = c(2.25,2))
```

Use the `ggtitle()` command to title each plot, and then also use the `annotate_figure()` command to set a common title for the combination of the two descriptive results. 

```r
annotate_figure(liberia, top = text_grob("Liberia", color = "black", face = "bold", size = 26))
```

To save your two plots together, use the `ggsave()` command.  Modify the `width =` and the `height =` commands to set the dimensions for your combined spatial and bar plot.  Use the `dpi =`  command to set the number of dots per inch, or effectively increase the resolution.

```r
ggsave("liberia.png", width = 20, height = 10, dpi = 200)
```

![](../.gitbook/assets/liberia%20%284%29.png)



## Project 1. Individual Deliverable

Upload the combined spatial description and geometric bar plot of your selected LMIC to the slack channel \#data100\_project1 no later than 11:59PM on Saturday, September 28th.

## Individual Stretch Goal 1

Again create a combined spatial description and geometric bar plot of your LMIC, but this time use the adm2 `sf` object you created in part 2, stretch goal 2.  Include this with your deliverable posted to \#data100\_project1.

## Individual Stretch Goal 2

Use the `render_movie("liberia.mp4")` command to create an orbitting video of the three dimension spatial plot you created in part 2, stretch goal 3.  Also, include this with your deliverable posted to \#data100\_project1.

 

