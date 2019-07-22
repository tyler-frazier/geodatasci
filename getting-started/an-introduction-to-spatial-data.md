# An Introduction to Spatial Data

Since we have had a bit of practice with creating a theoretical environment, let's go ahead and move to a more practical application.  In this exercise you will learn how to install a package and load a library of functions into R, install spatial data as a simple feature and then plot your geospatial data.  To begin with, let's install a package that we will use in order to describe and analyze our simple features.

```r
install.packages("tidyverse")
```

In the above command we are installing a collection of packages designed for data science, where all packages share an underlying design philosophy, grammar, and data structures.  Once RStudio has informed you that the package has been installed, you may then execute the command that makes the library function available for use during your current work session.

```text
library(tidyverse)
```

After executing the library command, R may inform you about the current version of attached packages while also identifying any conflicts that may exist.  Conflicts between functions often exist when one package installs a function that has the same name as another function in another package.  Generally, what happens, is the latest package to be installed will mask a same named function from a previously loaded library.

The tidyverse is not one library of functions, but is in fact a suite of packages where each one conforms to an underlying design philosphy, grammar and data structure.  In the previous exercise we used commands from the base R package, but in this exercise we will begin to consider the more recent development of the tidyverse syntax nomenclature that emerged from the gramar of graphics \(ggplot2\).  The [tidyverse](https://www.tidyverse.org/) is arguably more coherent, effective and powerful approach to data science programming in R.

