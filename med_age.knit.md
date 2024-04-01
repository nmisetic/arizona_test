---
title: "Median Age"
format: html
editor: visual
---

## Median Age Map


```r
knitr::opts_chunk$set(echo = TRUE)

library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.5
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ ggplot2   3.5.0     ✔ tibble    3.2.1
## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
## ✔ purrr     1.0.2     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

```r
library(tigris)
```

```
## To enable caching of data, set `options(tigris_use_cache = TRUE)`
## in your R script or .Rprofile.
```

```r
library(sf)
```

```
## Linking to GEOS 3.8.0, GDAL 3.0.4, PROJ 6.3.1; sf_use_s2() is TRUE
```

```r
library(tidycensus)
library (dplyr)
library (ggplot2)
library(htmltools)
library(janitor)
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

```r
library(here)
```

```
## here() starts at /cloud/project
```

```r
library(mapview)
library(leafsync)
library(leaflet.extras2)
```

```
## Loading required package: leaflet
```

```r
options(tigris_class = "sf")
```


```r
myapikey <- "7ec164ce2e6d7eff05a3da72fa85dec41773e398"
census_api_key(myapikey, overwrite = TRUE)
```

```
## To install your API key for use in future sessions, run this function with `install = TRUE`.
```


```r
arizona_voters_age <- get_acs(
  geography = 'tract',
  variables = c( 
    median_age = 'B01002A_001'
  ),
  state = 'AZ',
  output = "wide",
  geometry = TRUE
)
```

```
## Getting data from the 2018-2022 5-year ACS
```

```
## Downloading feature geometry from the Census website.  To cache shapefiles for use in future sessions, set `options(tigris_use_cache = TRUE)`.
```

```
## 
```


```r
arizona_voters_age <- arizona_voters_age %>%
  select(-ends_with("M"))

colnames(arizona_voters_age) <- sub("E$", "", colnames(arizona_voters_age))
```


```r
mapview(arizona_voters_age, zcol = "median_age")
```

```{=html}
<div class="leaflet html-widget html-fill-item" id="htmlwidget-b9957bf5bbcf34f46b02" style="width:672px;height:480px;"></div>
```

[Back](https://nmisetic.github.io/arizona_test/)