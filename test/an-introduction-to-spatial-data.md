# An Introduction to Spatial Data

We have had a bit of practice creating a theoretical environment, but now we will move to a more practical application.  In this exercise you will learn how to install a package and load a library of functions into R, install spatial data as a simple feature and then use the grammar of graphics \(aka `ggplot::`\) to plot your geospatial data.  To begin with, let's install a package that we will use in order to describe and analyze our simple features.

```r
install.packages("tidyverse", dependencies = TRUE)
```

In the above command we are installing a collection of packages designed for data science, where all packages share a common design.  Once RStudio has informed you that the package has been installed, you may then execute the command that makes the library function available for use during your current work session.

```r
library(tidyverse)
```

After executing the library command, R may inform you about the current version of attached packages while also identifying any conflicts that may exist.  Conflicts between functions often exist when one package installs a function that has the same name as another function in another package.  Generally, what happens, is the latest package to be installed will mask a same named function from a previously loaded library.

The tidyverse is not one library of functions, but is in fact a suite of packages where each one conforms to an underlying design philosphy, grammar and data structure.  In the previous exercise we used commands from the base R package, but in this exercise we will begin to consider the more recent development of the tidyverse syntax nomenclature that emerged from the gramar of graphics \(ggplot2\).  The [tidyverse](https://www.tidyverse.org/) is arguably a more coherent, effective and powerful approach to data science programming in R.

After installing and loading the `tidyverse` suite of packages, let's install yet another important important package for working with spatial data.

```r
install.packages("sf", dependencies = TRUE)
```

This will install the `sf` package,  or [simple features](https://r-spatial.github.io/sf/), which like the tidyverse is a recent, arguably more effective implementation of a design philosphopy for using spatial data in R.  The `sf::` package also has been designed to integrate with the `tidyverse` syntax.  After installing `sf::`, then as before run the `library()` function to load the library of functions contained within the package for use in your current R worksession.

After running the `install.packages()` command successfully, you should add a `#` at the beginning of that line in order to comment it out. Running the `install.package()` command is generally necessary only once, in order to retrieve the package from a remote location and install it on your local machine, but it is necessary to run the `library()` command each time you open R and wish to access a function from within that library.

Another helpful command to add at the beginning of your script is `rm(list=ls(all=TRUE))` , which will delete everything from your R workspace from the outset. By running this line of code first in your script, you will be working with what John Locke called a _tabula rasa_ or a clean slate from the outset. After adding the remove all function as your first line of code but after installing your packages and loading those libraries, be sure to set your working directory. While it's fine to use the drop down menu to find the location of your working directory, the first time, it is a good idea to copy that line of code into your script, so the `setwd()` command can be executed programmatically instead of through the GUI \(which will save you time\). At this point your script should look like the following snippet of code.

```r
rm(list=ls(all=TRUE))

# install.packages("tidyverse", dependencies = TRUE)
# install.packages("sf", dependencies = TRUE)

library(tidyverse)
library(sf)

setwd("the/path/to_my/working/directory")
```

The next step is to visit the [Humanitarian Data Exchange](https://data.humdata.org) website and begin to become familiar with all of the data available through that portal.  The front page of HDX offers a **Find Data** search tool on the right hand side towards the top.  As an example, enter **Liberia** into the find data search field and press enter.

![The Main Page for the HDX Website -- Notice the Find Data Search Field](../.gitbook/assets/screen-shot-2019-09-06-at-9.47.46-pm.png)

The HDX website should return 125 or so datasets for the West African country of Liberia. Included in the search results will be data describing Liberia's healthsites, settlements, roads, population, pregnancies, births, and a number of other local dimensions of human development.  Some of the data made available through HDX will have been remotely sensed, most typically from a satellite orbitting the earth.  This remotely sensed data is then usually classified according to different discrete types or perhaps by assigning values or interval of possible values.  Other times the data available will have been obtained from a source in the field, and most typically from some institution or group located or working within that particular country.  Surveys and census data are examples of _secondary sources_ that were most often obtained from local institutions.  Like remotely sensed data, secondary sources also serve to provide a description of existing conditions, while serving as the basis for further analysis, modeling, inference and potential simulations.

Scroll through the results until you find a data set that provides a spatial description of **Liberia's administrative boundaries**.  Administrative boundaries refer to the national border as well as all of the regional, district and local government subdivisions of that country.  Typically these administrative boundaries and subdivisions have been obtained and provided by one of the regional offices within the _United Nations Office for the Coordination of Humanitarian Affaris_ \(OCHA\).  For example, the secondary sources of data that describe Liberia's political geography has been provided by the _Regional Office of West and Central Africa_ \(ROWCA\), presumably as they have obtained these sources from a ministry of government from within Liberia.  Every country employs a unique nomenclature in order to describe its administrative subdivisions.  Liberia is first subdivided into _counties_ with each county further subdivided into _districts_.  Each of Liberia's _districts_ is then further subdivided into what are called _clan areas._

Once you have found the **Liberia Administrative Boundaries** link, click on it and follow it to a web page where a number of files will be made available to you under a **Data and Resources** tab.  

```r
ggplot() +
  geom_sf(data = your_sf_obj)
```

![Administrative Boundaries spatial data for Liberia made available by OCHA through HDX](../.gitbook/assets/screen-shot-2019-09-06-at-10.04.39-pm.png)

For our purposes, we want to obtain the national boundary \(admint\), first level administrative subdivisions \(adm1\) and second level administrative subdivisions \(adm2\).  Download each of these folders by clicking on the download tab off to the right of each file name.  After the folders have been downloaded, go to your working directory and create a new folder named **data** and then move the folders describing Liberia's administrative subdivisions to within that folder.  The structure of your working directory should look something like the following \(minus the additional folders\).

![Data and Script subfolders within my R Session Working Directory](../.gitbook/assets/screen-shot-2019-09-07-at-12.43.35-pm.png)

You will also notice that within each folder, there are a number of different files, each one with the same file name yet also having a unique file extension.  The file extension is the _three letter part of the file name that is to the right of the period_, and acts somewhat as an acronym for the file type.  For example, files that have the `.shp` file extension are called shapefiles.  A shapefile contains the geometry of the points, lines and polygons used to spatially describe, in this example, the political geography of Liberia.  A shapefile also requires most of the other files found in the folder in order for it to function properly.  For example, the `.prj` file provides the projection that is used when plotting the geometry.  The `.dbf` file provides the attributes associated with each spatial unit \(for example the name associated with each county or district\).  Other files also provide information that enables RStudio to further interpret the spatial information in order to better serve our purposes.

In order to import a shapefile into RStudio we are going to use a command from the `sf::` package \(simple features\).  RStudio will need to find each of the `.shp` files in order to import the international border, the first level administrative subdivisions and the second level administrative subdivisions.  If I have set my working directory to the **data** folder, then RStudio will need to traverse through the subfolder in order to locate the correct `.shp` files.  You also will need to use the `read_sf()` command to import the `.shp` file into RStudio and create a simple feature class object.

```r
lbr_int  <- add_command_here("add_folder_here/add_file_name_here.shp")
```

Once you have successfully executed the above function using the `sf::read_sf()` command, you should observe a new object named `lbr_int`appearing in the top right data pane within your RStudio environment.  To the right of your newly created object there is a small gridded box that you will be able to click on in order to view individual attributes associated with this simple feature class spatial object.  You will also notice that within the data pane, RStudio also provides you with some basic information about the object, in this case 1 observation that has 7 variables.

The `sf::` package also includes a function called `st_geometry()` that will enable you to view some of the basic geometry associated with the object you have named `lbr_int`.  Type the name of your object within the `st_geometry()` command so that RStudio will return some basic geometric information about our spatial object that describes Liberia's international border.  You don't necessarily need to write this command in your script, you can just enter it directly into the console

![Some basic R commands](../.gitbook/assets/screen-shot-2019-09-07-at-1.32.41-pm.png)

After using the `st_geometry()` command with our `lbr_int` object, RStudio provides us with a basic description that includes the geometry type \(polygons in this case, but it could also return points or lines\), the x & y minimum and maximum values or also know as the bounnding box \(bbox\), the epsg spatial reference identifier \(a number used to identify the projection\) and finally the projection string , which provides additional information about the projection used.

Now that we have conducted a cursory investigation of our simple feature object geometry, let's plot our simple features class object that describes the international border of Liberia.  To plot, we will use a series of functions from a package called `ggplot()`.  The gg in the package name `ggplot::` stands for the grammar of graphics, and is a very useful package for plotting all sorts of data, including spatial data classes created with the `sf::` package.  To start add `ggplot() +` to your script and then on the following line add the `geom_sf(data = your_sf_obj)` in order to specify the data that `ggplot()` should in producing its output.  

Following the `data =` argument, you can also specifiy the line weight for the border using the `size =` argument.  It is also possible to specify the `color =` as well as the opacity / transparency of your polygon using the `alpha =` argument.  With the following script I have set the international border line weight width to `1.5` , the color of the border to `"gold"` , the fill color for the internal portion of the polygon to `"green"` and the `alpha =`   value to .5 or 50% transparent.

![Liberia with a green fill and gold border](../.gitbook/assets/liberia%20%282%29.png)

It would also be helpful to have a label describing our plot.  In order to do this we can use either the `geom_sf_text()` command or the `geom_sf_label()` command.  In the following snippet of code you will notice that I have added the aesthetics argument within my `geom_sf_text()` command.  The `aes =` argument enables us to specify which variable contains the label we will place on our object.  If you click on the blue arrow to the left of the `lbr_int` object in the top right data pane, the object will expand below to reveal the names of all variables.  The second variable is named `CNTRY_NAME` and provides us with the name we will use as our label, Liberia.  Following the `aes()` argument, you can also specify the `size =` of your label as well as its `color =`.

```r
ggplot() +
  geom_sf(data = your_sf_obj,
          size = value,
          color = "color",
          fill = "color",
          alpha = value_between_0_&_1) +
  geom_sf_text(data = your_sf_obj,
               aes(label = variable_name),
               size = value,
               color = "color")
```

![Liberia labelled](../.gitbook/assets/liberia.png)

Good job!  You have successfully used ggplot from the tidyverse with the simple features package in order to properly project and plot Liberia's international border, as well as to include a label.  Now continue with the first level of administrative subdivisions, Liberia's fifteen counties.  In order to do this, return to your use of the `read_sf()` command in order to import and create an object named `lbr_adm1`.   

```r
lbr_adm1  <- add_command_here("add_folder_here/add_file_name_here.shp")
```

As before you could use the data pane in the top right corner to expand your view of the `lbr_adm1` file you created.  You can also click on the small grid symbol to the right of your data object \(within the data pane\) in order to view your data in a new tab in the same pane where your script is located.  Whereas before we had a simple feature class object with 1 observation with 7 variables, your `lbr_adm1` simple feature object has 15 observations, with each observation having 8 different variables describing some attribute associated with each individual polygon.  Let's plot both Liberia's international border as well as its 15 counties.

To do this, follow the same approach you used with the `lbr_int` object but replace it with the name of your adm1 spatial object, `lbr_adm1`.  Also follow the same approach you used for adding the labels in your previous snippet of code, but this time specify the variable with the county names from `lbr_adm1`.  

```r
ggplot() +
  geom_sf(data = your_adm1_sf_obj,
          size = value,
          color = "color",
          fill = "color",
          alpha = value) +
  geom_sf(data = your_int_sf_obj,
          size = value,
          color = "color",
          fill = "color",
          alpha = value) +
  geom_sf_text(data = your_adm1_sf_obj,
               aes(label = variable_name),
               size = value,
               color = "color") +
  geom_sf_label(data = your_int_sf_obj,
               aes(label = variable_name),
               size = value,
               color = "color")
```

The code above will produce the plot below when the`geom_sf()` function using the `lbr_adm1` arguments is specified with a line weight `size = 0.65`, line weight `color = "gray50"`, a polygon `fill = "gold3"` and a 65% opacity value of `alpha = 0.65`.  Additionally, I have set the `size = 2.0` , and the `alpha = 0` \(100% transparent\) for the `data = lbr_int` object. The `geom_sf()` command will default to a `color = "black"` if the line color is not specified. Additionally, since the `alpha = 0` no `fill = "color"` is needed \(since it will not appear\). The county labels have a `size = 2` \(and also defaults to a `color = "black"`, while the `geom_sf_text()` command to label Liberia has a `size = 12` argument. In order to nudge the label to the east and south I have also added the `nudge_x = 0.3` and `nudge_y = -.1` arguments to the `geom_sf_label()` command.

![Liberia and its 15 Counties](../.gitbook/assets/liberia%20%281%29.png)

After adding the counties go back and add the second level of administrative subdivisions, or districts.  Again use `read_sf()` to import that shapefile as a simple feature object into your RStudio workspace.  Use the  `geom_sf_text()` command to add the labels, while also making sure to specify the correct variable name in the `aes(label = variable_name)` argument.  Size the district borders and labels so they are smaller than the internation border as well as the county delineations.

```r
rm(list=ls(all=TRUE))

# install.packages("tidyverse", dependencies = TRUE)
# install.packages("sf", dependencies = TRUE)

library(tidyverse)
library(sf)

setwd("~/Tresors/teaching/project_folder/data")

lbr_int  <- read_sf("lbr_admbnda_admint_ocha/lbr_admbnda_admint_ocha.shp")
lbr_adm1  <- read_sf("lbr_admbnda_adm1_ocha/lbr_admbnda_adm1_ocha.shp")
lbr_adm2  <- read_sf("lbr_admbnda_adm2_ocha/lbr_admbnda_adm2_ocha.shp")

ggplot() +
  geom_sf(data = adm2_object,
          size = value,
          color = "color",
          fill = "color",
          alpha = value) +
  geom_sf(data = adm1_object,
          size = value,
          color = "gray50",
          alpha = value) +
  geom_sf(data = int_object,
          size = value,
          alpha = value) +
  geom_sf_text(data = adm2_object,
               aes(label = variable_name),
               size = value) +
  geom_sf_text(data = adm1_object,
               aes(label = variable_name),
               size = value)

ggsave("liberia.png")
```

Use `ggsave(file_name.png)` to save your plot as a `.png` file, to your working directory.

## Team Challenge Question

Follow the steps from above that you used to produce your plot of Liberia, but instead each team member should use their own selected LMIC country.  Go back to the HDX website and find the administrative boundaries for the LMIC country you have selected.  Plot and label the international border, the first level of administrative subdivisions and the second level of administrative subdivisions.

Meet with your group and prepare to present the best two plots for the Friday informal group presentation.  Then as a group, upload all 5 team members plots to \#data100\_igps \(informal group presentations\) by Sunday night.

## Individual Stretch Goal

Go to the [GADM](https://www.gadm.org) website and download the shapefiles for your selected country.  Compare their administrative subdivisions to those obtained from HDX.  Are they the same?  Are there any differences?  Which source do you think more closely describes to the local political reality in your selected LMIC?











