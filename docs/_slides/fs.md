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

Copy into new folders (maybe only copy the ones that work here?)



~~~r
> file_copy(details, new_path = dir_create("data/details/")) # slow
~~~
{:.input title="Console"}


===

Read in files from new location and create one big data frame.

`map_df` applies function to a list of elements and binds dfs together
assuming they can be combined. Read in *just* files 57-59. 



~~~r
> details <- dir_ls("data/details")
> basename(details)
~~~
{:.input title="Console"}


~~~
 [1] "StormEvents_details-ftp_v1.0_d1950_c20140824.csv"
 [2] "StormEvents_details-ftp_v1.0_d1951_c20140824.csv"
 [3] "StormEvents_details-ftp_v1.0_d1952_c20140824.csv"
 [4] "StormEvents_details-ftp_v1.0_d1953_c20140824.csv"
 [5] "StormEvents_details-ftp_v1.0_d1954_c20140824.csv"
 [6] "StormEvents_details-ftp_v1.0_d1955_c20140824.csv"
 [7] "StormEvents_details-ftp_v1.0_d1956_c20140824.csv"
 [8] "StormEvents_details-ftp_v1.0_d1957_c20140824.csv"
 [9] "StormEvents_details-ftp_v1.0_d1958_c20140824.csv"
[10] "StormEvents_details-ftp_v1.0_d1959_c20140824.csv"
[11] "StormEvents_details-ftp_v1.0_d1960_c20140824.csv"
[12] "StormEvents_details-ftp_v1.0_d1961_c20140824.csv"
[13] "StormEvents_details-ftp_v1.0_d1962_c20140824.csv"
[14] "StormEvents_details-ftp_v1.0_d1963_c20140824.csv"
[15] "StormEvents_details-ftp_v1.0_d1964_c20140824.csv"
[16] "StormEvents_details-ftp_v1.0_d1965_c20140824.csv"
[17] "StormEvents_details-ftp_v1.0_d1966_c20140824.csv"
[18] "StormEvents_details-ftp_v1.0_d1967_c20140824.csv"
[19] "StormEvents_details-ftp_v1.0_d1968_c20140824.csv"
[20] "StormEvents_details-ftp_v1.0_d1969_c20140824.csv"
[21] "StormEvents_details-ftp_v1.0_d1970_c20140824.csv"
[22] "StormEvents_details-ftp_v1.0_d1971_c20140824.csv"
[23] "StormEvents_details-ftp_v1.0_d1972_c20140824.csv"
[24] "StormEvents_details-ftp_v1.0_d1973_c20140824.csv"
[25] "StormEvents_details-ftp_v1.0_d1974_c20140824.csv"
[26] "StormEvents_details-ftp_v1.0_d1975_c20140824.csv"
[27] "StormEvents_details-ftp_v1.0_d1976_c20140824.csv"
[28] "StormEvents_details-ftp_v1.0_d1977_c20140824.csv"
[29] "StormEvents_details-ftp_v1.0_d1978_c20140824.csv"
[30] "StormEvents_details-ftp_v1.0_d1979_c20140824.csv"
[31] "StormEvents_details-ftp_v1.0_d1980_c20140824.csv"
[32] "StormEvents_details-ftp_v1.0_d1981_c20140824.csv"
[33] "StormEvents_details-ftp_v1.0_d1982_c20140824.csv"
[34] "StormEvents_details-ftp_v1.0_d1983_c20140824.csv"
[35] "StormEvents_details-ftp_v1.0_d1984_c20140824.csv"
[36] "StormEvents_details-ftp_v1.0_d1985_c20140824.csv"
[37] "StormEvents_details-ftp_v1.0_d1986_c20140824.csv"
[38] "StormEvents_details-ftp_v1.0_d1987_c20140824.csv"
[39] "StormEvents_details-ftp_v1.0_d1988_c20140824.csv"
[40] "StormEvents_details-ftp_v1.0_d1989_c20140824.csv"
[41] "StormEvents_details-ftp_v1.0_d1990_c20140824.csv"
[42] "StormEvents_details-ftp_v1.0_d1991_c20140824.csv"
[43] "StormEvents_details-ftp_v1.0_d1992_c20140824.csv"
[44] "StormEvents_details-ftp_v1.0_d1993_c20140824.csv"
[45] "StormEvents_details-ftp_v1.0_d1994_c20140824.csv"
[46] "StormEvents_details-ftp_v1.0_d1995_c20140916.csv"
[47] "StormEvents_details-ftp_v1.0_d1996_c20140916.csv"
[48] "StormEvents_details-ftp_v1.0_d1997_c20140824.csv"
[49] "StormEvents_details-ftp_v1.0_d1998_c20140824.csv"
[50] "StormEvents_details-ftp_v1.0_d1999_c20140915.csv"
[51] "StormEvents_details-ftp_v1.0_d2000_c20140824.csv"
[52] "StormEvents_details-ftp_v1.0_d2001_c20140824.csv"
[53] "StormEvents_details-ftp_v1.0_d2002_c20140824.csv"
[54] "StormEvents_details-ftp_v1.0_d2003_c20140824.csv"
[55] "StormEvents_details-ftp_v1.0_d2004_c20140824.csv"
[56] "StormEvents_details-ftp_v1.0_d2005_c20140824.csv"
[57] "StormEvents_details-ftp_v1.0_d2006_c20140824.csv"
[58] "StormEvents_details-ftp_v1.0_d2007_c20140824.csv"
[59] "StormEvents_details-ftp_v1.0_d2008_c20140824.csv"
[60] "StormEvents_details-ftp_v1.0_d2009_c20140824.csv"
[61] "StormEvents_details-ftp_v1.0_d2010_c20140824.csv"
[62] "StormEvents_details-ftp_v1.0_d2011_c20140824.csv"
[63] "StormEvents_details-ftp_v1.0_d2012_c20140824.csv"
[64] "StormEvents_details-ftp_v1.0_d2013_c20140824.csv"
[65] "StormEvents_details-ftp_v1.0_d2014_c20140824.csv"
~~~
{:.output}




~~~r
> details_df <- details[57:59] %>% 
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

