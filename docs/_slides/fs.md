---
---

# File manipulation

The `fs` package has functions for interacting with the file system.

===

We will copy some files from public-data for demonstration purposes.



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



~~~r
> file_copy(details[57:59], new_path = dir_create("data/details/"))
~~~
{:.input title="Console"}


===

Read in files from new location and create one big data frame.

`map_df` applies function to a list of elements and binds dfs together
assuming they can be combined.  



~~~r
> details <- dir_ls("data/details")
> basename(details)
~~~
{:.input title="Console"}


~~~
[1] "StormEvents_details-ftp_v1.0_d2006_c20140824.csv"
[2] "StormEvents_details-ftp_v1.0_d2007_c20140824.csv"
[3] "StormEvents_details-ftp_v1.0_d2008_c20140824.csv"
~~~
{:.output}




~~~r
> details_df <- details %>% 
+   map_df(read_csv, .id = "filename")
~~~
{:.input title="Console"}




~~~r
> head(details_df)
~~~
{:.input title="Console"}


~~~
# A tibble: 6 x 52
  filename BEGIN_YEARMONTH BEGIN_DAY BEGIN_TIME END_YEARMONTH END_DAY
  <chr>              <int>     <int>      <int>         <int>   <int>
1 data/de…          200604         7       1515        200604       7
2 data/de…          200601         1          0        200601      31
3 data/de…          200601         1          0        200601      31
4 data/de…          200601         1          0        200601      31
5 data/de…          200601         1          0        200601      31
6 data/de…          200601        30        500        200601      31
# ... with 46 more variables: END_TIME <int>, EPISODE_ID <int>,
#   EVENT_ID <int>, STATE <chr>, STATE_FIPS <int>, YEAR <int>,
#   MONTH_NAME <chr>, EVENT_TYPE <chr>, CZ_TYPE <chr>, CZ_FIPS <int>,
#   CZ_NAME <chr>, WFO <chr>, BEGIN_DATE_TIME <chr>, CZ_TIMEZONE <chr>,
#   END_DATE_TIME <chr>, INJURIES_DIRECT <int>, INJURIES_INDIRECT <int>,
#   DEATHS_DIRECT <int>, DEATHS_INDIRECT <int>, DAMAGE_PROPERTY <chr>,
#   DAMAGE_CROPS <chr>, SOURCE <chr>, MAGNITUDE <dbl>,
#   MAGNITUDE_TYPE <chr>, FLOOD_CAUSE <chr>, CATEGORY <chr>,
#   TOR_F_SCALE <chr>, TOR_LENGTH <dbl>, TOR_WIDTH <dbl>,
#   TOR_OTHER_WFO <chr>, TOR_OTHER_CZ_STATE <chr>,
#   TOR_OTHER_CZ_FIPS <chr>, TOR_OTHER_CZ_NAME <chr>, BEGIN_RANGE <int>,
#   BEGIN_AZIMUTH <chr>, BEGIN_LOCATION <chr>, END_RANGE <int>,
#   END_AZIMUTH <chr>, END_LOCATION <chr>, BEGIN_LAT <dbl>,
#   BEGIN_LON <dbl>, END_LAT <dbl>, END_LON <dbl>,
#   EPISODE_NARRATIVE <chr>, EVENT_NARRATIVE <chr>, DATA_SOURCE <chr>
~~~
{:.output}


