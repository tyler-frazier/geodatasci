# Installing R and R Studio on your Computer

## What is R?

R is a free software environment for statistical computing and graphics that compiles and runs on a wide variety of UNIX platforms, Windows and MacOS.  It is a very capable programming environment for offering a good introduction to data science methods.  R is also extensible for executing some of the most poweful, advanced, and state of the art statistical and machine language functions within the context of a wide variety of disciplines and applications.  Using R is capable of working with big data, high dimension data, spatial data, temporal data, as well as data at pretty much any imaginable scale available, from the to the quark and everywhere in between.

The statistical programming language R can be considered as different from machine languages such a **C** or **Java**.  R is often described as an interpreted programming language, where commands and their arguments are interpreted prior to being compiled by the programming engine.  **Python** is another, closely related interpreted programming language.  Interpreted languages are generally more accessible since the commands are often more readily understandable.  For example, commands such as `plot`, `read.csv()`, or `cbind()` can be fairly easily understood as the commands for plotting an object, importing a `.csv` file or binding together columns of data. 

**R** can also function stand alone, or you have the option of installing what is called an integrated developer environment \(IDE\).  One of the most popular IDEs for **R** is called RStudio.  In order for RStudio to function properly, you will first need to install your R programming framework, before installing the IDE.

## Installing R

Before installing R on your operating system, it is a good idea to briefly assess the state of your computer and its constituent hardware as well as the state of your operating system.  Prior to installing a new software environment, such as R, I always recommend the following.

1. Do your best to equip your personal computer with the latest release of your operating system
2. Make sure you have installed all essential updates for your operating system
3. Restart your computer
4. Make sure that all non essential processes have not automatically opened at login, such as e-mail, messaging systems, internet browsers or any other software

After you have updated your computer and done your best to preserve all computational power for the installation process, go the **R Project for Statistical Computing** website.

{% embed url="https://www.r-project.org" %}

Find the **download** link and click on it.  If this is the first time you have downloaded **R**, then it is likely that you will also need to select a CRAN mirror, from which you will download your file.  Choose one of the mirrors from within the USA, preferable a server that is relatively close to your current location.  I typically select, Duke, Carnegie Mellon or Oak Ridge National Laboratory.   A more comprehensive install of R on a Mac OS X will include the following steps.

1. Click on the `R.pkg`  file to download the latest release.  Following the steps and install **R** on your computer.
2. Click on the **XQuartz** link and download the latest release of `XQuartz.dmg` .  It is recommended to update your XQuartz system each time you install or update **R**.
3. Click on the **tools** link and download the latest `clang.pkg` and `gfortran.pkg`. Install both.

Following are two video tutorials that will also assist you to install **R** on your personal computer.  The first one is for installing **R** on a Mac, while the second video will guide you through the process on Windows.

{% embed url="https://www.youtube.com/watch?v=V2x\_SWJCd1A&t=11s" caption="Video tutorial of how to install R on a Mac" %}

{% embed url="https://www.youtube.com/watch?v=1A-xvxNhd2w" caption="Video tutorial of how to install R on Windows" %}

## Installing RStudio

RStudio is a type of software that operates in tandem with your R framework in order to assist you with coding, executing commands, saving plots and a number of other different functions.  This type of extensions of the basic programming framework is often called an integrated development environment \(IDE\). RStudio is an IDE that will help you take better control of your programming.  While the two are closely aligned in design and function, it is important to recognizing that RStudio is a separate program, which depends on **R** first having been installed.

To install RStudio go to the following webpage and download the appropriate installer for your operating system.  

{% embed url="https://www.rstudio.com/products/rstudio/download/\#download" %}





