# Extracting Populations from a Raster and Aggregating to each Unit

Now that you have selected your LMIC and produced a basic geospatial description of that country at both the adm1 and adm2 levels of government, you are now set to join some data to each of those units and begin conducting a basic descriptive analysis.  Start by going back to the HDX website and search for the available datasets associated with your selected country.  Look for a dataset with the name of your country followed by the term population.  For Liberia the link is named **Liberia - Population**.  After you find the link, follow it where you should find a page that lists the names of several `.tif` files under the **Data and Resources** tab.  Since it is the year 2019, go ahead and download the file for this year.  For Liberia the file is named **lbr\_ppp\_2019.tif**.  

![Liberia&apos;s World Pop data as found on HDX  ](../.gitbook/assets/screen-shot-2019-09-15-at-1.23.26-pm.png)

Clicking on the download tab may automatically begin the process of downloading the `.tif` file into your downloads folder.  Sometimes your web browser may be set to try and display the image file directly within the browser itself.  You should still be able to save the file directly to your downloads folder, OR go back to the download tab, right click on it, and select **download linked file**, in order to override any attempt to display the image.

After you have succesfully downloaded the file, go to your project folder that you previously used as your working directory and create a new folder within the `/data` folder that will be dedicated to raw data from worldpop.

![Structure within the Data Folder](../.gitbook/assets/screen-shot-2019-09-15-at-3.17.40-pm.png)

Once you have your `.tif` file located within a subdirectory of the data folder, you can go ahead and open up RStudio.  Create a new file, R Script, and save it in your scripts folder.  Add the `rm(list=ls(all=TRUE))` at the beginning of your code and then load the tidyverse and sf libraries.  Following your libraries, be sure to set your working directory.

```r
rm(list=ls(all=TRUE))

# install.packages("tidyverse", dependencies = TRUE)
# install.packages("sf", dependencies = TRUE)

library(tidyverse)
library(sf)

setwd("~/path/to_my/working/directory/")
```

Now for this exercise, we will install a new package and then load its library of functions.  Use the `install.packages()` to install the `raster::` package.  Be sure to set the `dependencies = TRUE` argument within your command.  After you have successfully installed the `raster::` package, use the `library()` function to load `raster::` and make its set of commands available as part of your current RStudio work session.

The first command we will use from the `raster::` package shares the same name as the library itself.  We use the `raster()` function to import our `.tif` file from its location within our data subdirectory to the current RStudio work session.  Keep in mind, if you set your working directory to the `/data` folder, but then also created a subfolder named `/world_pop` you will need to include the subdirectory path, as well as the full name of the `.tif` within the `raster()` command.

```r
myLMIC_ppp_pop19 <- add_command_here("add_folder_name_here/add_file_name_here.tif")
```

Once you have created your new raster object, by using the `raster()` function, you should notice a new _Formal class RasterLayer_ data object appear in the top right data pane.  In order to find out some basic information about my newly created raster object, I will type the name of my object directly into the console.





