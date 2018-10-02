---
---

# File manipulation

The `fs` package has functions for interacting with the file system.

===

We will copy some files from public-data for demonstration purposes



~~~r
> library(fs)
> path <- "/nfs/public-data/NOAA/www.ncdc.noaa.gov"
~~~
{:.input title="Console"}


===

Find files with matching patterns 



~~~r
> details <- dir_ls(path, recursive = TRUE, regexp = "details")
> # locations <- dir_ls(path, recursive = TRUE, regexp = "locations")
> # fatalities <- dir_ls(path, recursive = TRUE, regexp = "fatalities")
~~~
{:.input title="Console"}


===

Copy *just* files 57-59 into a new folder called "details" in the data folder. 









