# Adding transportation facilities & health care services

To start the final part of project 3, head back to the HDX website that we used all the way back during the first few weeks of the semester and enter the name of your selected LMIC.  Again, I will select Liberia and begin to browse through the available data.  Identify the road network dataset for your LMIC and then select it.  Select the download button on the subsequent webpage and obtain the available data.  Move the folder you just downloaded \(including the shapefile and all of its other associated files\) to your working directory.

Import the roads shapefile into RStudio using the `read_sf()` command.

```text
LMIC_roads  <- add_command_here("data_folder/LMIC_roads.shp")
```

Using the polygon you created at the end of the previous exercise use the `st_crop()` command to crop your `LMIC_roads` object to just those roadways that are located within the adm2 or adm3 previously selected.

```text
adm2_roads <- add_command_here(LMIC_roads, subset_adm2)
```

Use the `table()` command to review the different classifications of roads that populate your adm2.  Most likely the variable you will be interested in producing a table that describes the different discrete values is named `CATEGORY`.

```text
add_command_here(object$variable)
```

Take each of these different discrete outcomes within your roads `sf` object and use the `filter()` command to subset based on each different classification.

```text
primary <- combined_rds %>%
  filter(CATEGORY == "Primary Routes")

paved <- combined_rds %>%
  filter(CATEGORY == "Paved")

tracks <- combined_rds %>%
  filter(CATEGORY == "Tracks")
```



 

