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

```text
# install.packages("tidyverse", dependencies = TRUE)
# install.packages("sf", dependencies = TRUE)

library(tidyverse)
library(sf)
```

Your R script to this point should appear as above.  You will also notice that I have commented out lines 1 & 2 in the above snippet of code.  Running the `install.package()` is only necessary one time, in order to retrieve the package from a remote location and install it on your local machine, but it is necessary to run the `library()` command each time you open R and wish to access a function from within that library.  Therefor, as we did in the previous exercise, I have used the `#` sign to comment out those two lines of code, so R will ignore it.



