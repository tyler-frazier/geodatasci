# An Introduction to Spatial Data

Since we have had a bit of practice with creating a theoretical environment, let's go ahead and move to a more practical application.  In this exercise you will learn how to install a package and load a library of functions into R, install spatial data as a simple feature and then plot your geospatial data.  To begin with, let's install a package that we will use in order to describe and analyze our simple features.

```r
install.packages("tidyverse", dependencies = TRUE)
```

In the above command we are installing a collection of packages designed for data science, where all packages share an common design.  Once RStudio has informed you that the package has been installed, you may then execute the command that makes the library function available for use during your current work session.

```r
library(tidyverse)
```

After executing the library command, R may inform you about the current version of attached packages while also identifying any conflicts that may exist.  Conflicts between functions often exist when one package installs a function that has the same name as another function in another package.  Generally, what happens, is the latest package to be installed will mask a same named function from a previously loaded library.

The tidyverse is not one library of functions, but is in fact a suite of packages where each one conforms to an underlying design philosphy, grammar and data structure.  In the previous exercise we used commands from the base R package, but in this exercise we will begin to consider the more recent development of the tidyverse syntax nomenclature that emerged from the gramar of graphics \(ggplot2\).  The [tidyverse](https://www.tidyverse.org/) is arguably a more coherent, effective and powerful approach to data science programming in R.

After installing and loading the `tidyverse` suite of packages, let's install yet another important important package for working with spatial data.

```r
install.packages("sf", dependencies = TRUE)
```

This will install the `sf` package,  or [simple features](https://r-spatial.github.io/sf/), which like the tidyverse is a recent, arguable more effective implementation of a design philosphopy for using spatial data in R.  The `sf` package also has been designed to integrate with the `tidyverse` syntax.  After installing sf, then as before run the `library()` function to load the library of functions contained within the package for use in your current R worksession.

After running the `install.packages()` command successfully, you should add a \# at the beginning of that line in order to comment it out. Running the `install.package()` command is only necessary one time, in order to retrieve the package from a remote location and install it on your local machine, but it is necessary to run the `library()` command each time you open R and wish to access a function from within that library.

Another helpful command to add at the beginning of your script is `rm(list=ls(all=TRUE))` , which will delete everything from your R workspace from the outset. By running this line of code first in your script, you will be working with what John Locke called a tabula rasa or a clean slate from the outset. After adding the remove all function as your first line of code but after installing your packages and loading those libraries, be sure to set your working directory. While it's fine to use the drop down menu to find the location of your working directory, the first time, it is always a good idea to copy that line of code into your script, so the `setwd()` command can be executed programmatically instead of through the GUI \(which will save you time\). At this point your script should look like the following snippet of code.

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

The HDX website should return 125 or so datasets for the West African country of Liberia. Included in the search results will be data describing Liberia's healthsites, settlements, roads, population, pregnancies, births, and a number of other local dimensions of human development.  Scroll through the results until you find a data set that provides a spatial description of Liberia's administrative boundaries.  The administrative boundaries refers to the national border as well as all of the regional, district and local government subdivisions of that country.  Every country employs a unique nomenclature in order to describe its administrative subdivisions.  For example, in the United States, our nation is first subdivided into states and then each state is subdivided into counties.  In comparison, Liberia is first subdivided into _counties_ with each county further subdivided into _districts_.  Each of Liberia's _districts_ is then further subdivided into what is called a _clan area_.

Once you have found the **Liberia Administrative Boundaries** link, click on it and follow it to a web page where a number of files will be made available to you under a **Data and Resources** tab.  

![Administrative Boundaries spatial data for Liberia made available by OCHA through HDX](../.gitbook/assets/screen-shot-2019-09-06-at-10.04.39-pm.png)

For our purposes, we want to obtain the national boundary \(admint\), first level administrstive subdivisions \(adm1\) and second level administrative subdivisions \(adm2\).  Download each of these folders by clicking on the download tab off to the right of each file name.



## 









