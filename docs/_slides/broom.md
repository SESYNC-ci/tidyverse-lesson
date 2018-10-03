---
---

# Tidy models with broom

We will start with the Census data set that was generated in the prior lesson.

Recall that we were interested modeling the median income across counties. 

$$
median\_income \sim industry + establishment\_size
$$

===

Read in the `acs_cbp.csv` using the appropriate function in `readr`. 



~~~r
> library(readr)
> acs_cbp <- read_csv("data/acs_cbp.csv")
~~~
{:.input title="Console"}


~~~
Parsed with column specification:
cols(
  FIPS = col_character(),
  Sector = col_character(),
  N1_4 = col_integer(),
  N5_9 = col_integer(),
  N10_19 = col_integer(),
  N20_49 = col_integer(),
  N50_99 = col_integer(),
  N100_249 = col_integer(),
  N250_499 = col_integer(),
  N500_999 = col_integer(),
  N1000 = col_integer(),
  N1000_1 = col_integer(),
  N1000_2 = col_integer(),
  N1000_3 = col_integer(),
  N1000_4 = col_integer(),
  County = col_character(),
  median_income = col_integer()
)
~~~
{:.output}


===

Create a simple model comparing median income across Sectors. 
One way to view details of the model fit is with `summary`. 



~~~r
> fit1 <- glm(median_income ~ Sector, 
+             family = gaussian, 
+             data = acs_cbp)
> summary(fit1)
~~~
{:.input title="Console"}


~~~

Call:
glm(formula = median_income ~ Sector, family = gaussian, data = acs_cbp)

Deviance Residuals: 
   Min      1Q  Median      3Q     Max  
-55098   -5879    -722    4487  190213  

Coefficients:
                                                     Estimate Std. Error
(Intercept)                                           12177.8      215.6
Sectoragriculture forestry fishing and hunting        15790.3      317.3
Sectorarts entertainment and recreation                5664.6      317.3
Sectorconstruction                                    22220.9      304.3
Sectoreducational services                            21801.0      320.9
Sectorfinance and insurance                           25548.4      305.9
Sectorhealth care and social assistance               16309.4      304.5
Sectorinformation                                     23335.8      312.9
Sectormanagement of companies and enterprises         49795.1      551.1
Sectormanufacturing                                   26274.3      306.4
Sectormining quarrying and oil and gas extraction     43897.1      345.0
Sectorother services except public administration      9850.1      304.7
Sectorprofessional scientific and technical services  30326.4      306.7
Sectorreal estate and rental and leasing              19145.6      316.3
Sectorretail trade                                     8203.8      304.2
Sectortransportation and warehousing                  28509.1      305.2
Sectorutilities                                       44643.2      316.9
Sectorwholesale trade                                 26765.9      308.4
                                                     t value Pr(>|t|)    
(Intercept)                                            56.47   <2e-16 ***
Sectoragriculture forestry fishing and hunting         49.77   <2e-16 ***
Sectorarts entertainment and recreation                17.85   <2e-16 ***
Sectorconstruction                                     73.01   <2e-16 ***
Sectoreducational services                             67.93   <2e-16 ***
Sectorfinance and insurance                            83.51   <2e-16 ***
Sectorhealth care and social assistance                53.56   <2e-16 ***
Sectorinformation                                      74.57   <2e-16 ***
Sectormanagement of companies and enterprises          90.36   <2e-16 ***
Sectormanufacturing                                    85.75   <2e-16 ***
Sectormining quarrying and oil and gas extraction     127.25   <2e-16 ***
Sectorother services except public administration      32.32   <2e-16 ***
Sectorprofessional scientific and technical services   98.88   <2e-16 ***
Sectorreal estate and rental and leasing               60.54   <2e-16 ***
Sectorretail trade                                     26.97   <2e-16 ***
Sectortransportation and warehousing                   93.40   <2e-16 ***
Sectorutilities                                       140.90   <2e-16 ***
Sectorwholesale trade                                  86.79   <2e-16 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for gaussian family taken to be 144008361)

    Null deviance: 1.3833e+13  on 49315  degrees of freedom
Residual deviance: 7.0993e+12  on 49298  degrees of freedom
  (3503 observations deleted due to missingness)
AIC: 1066393

Number of Fisher Scoring iterations: 2
~~~
{:.output}


===

That output is decidely untidy. The `broom` package will clean up
model outputs such as what is returned from `lm`, `nls`, `t.test`. 

The `tidy` function creates a data frame with one row for each
important component of the model.



~~~r
> library(broom)
> tidy(fit1)
~~~
{:.input title="Console"}


~~~
                                                   term  estimate
1                                           (Intercept) 12177.778
2        Sectoragriculture forestry fishing and hunting 15790.308
3               Sectorarts entertainment and recreation  5664.618
4                                    Sectorconstruction 22220.913
5                            Sectoreducational services 21800.994
6                           Sectorfinance and insurance 25548.393
7               Sectorhealth care and social assistance 16309.403
8                                     Sectorinformation 23335.758
9         Sectormanagement of companies and enterprises 49795.072
10                                  Sectormanufacturing 26274.310
11    Sectormining quarrying and oil and gas extraction 43897.054
12    Sectorother services except public administration  9850.114
13 Sectorprofessional scientific and technical services 30326.366
14             Sectorreal estate and rental and leasing 19145.623
15                                   Sectorretail trade  8203.758
16                 Sectortransportation and warehousing 28509.098
17                                      Sectorutilities 44643.180
18                                Sectorwholesale trade 26765.918
   std.error statistic       p.value
1   215.6370  56.47352  0.000000e+00
2   317.2988  49.76479  0.000000e+00
3   317.3309  17.85082  4.771120e-71
4   304.3456  73.01210  0.000000e+00
5   320.9289  67.93092  0.000000e+00
6   305.9275  83.51126  0.000000e+00
7   304.5159  53.55846  0.000000e+00
8   312.9391  74.56965  0.000000e+00
9   551.0509  90.36383  0.000000e+00
10  306.4083  85.74933  0.000000e+00
11  344.9798 127.24528  0.000000e+00
12  304.7358  32.32346 7.772501e-227
13  306.6891  98.88309  0.000000e+00
14  316.2501  60.53950  0.000000e+00
15  304.1761  26.97043 4.719179e-159
16  305.2284  93.40251  0.000000e+00
17  316.8512 140.89638  0.000000e+00
18  308.3853  86.79374  0.000000e+00
~~~
{:.output}


===

This may be useful for plotting, especially with the argument 
to include estimated confidence intervals to use with `ggplot2`'s
`geom_errobar`. 



~~~r
> tidyfit1 <- tidy(fit1, conf.int = TRUE)
> 
> library(ggplot2)
> ggplot(tidyfit1, aes(x = term, 
+                      y = estimate)) +
+   geom_point() +
+   geom_errorbar(aes(ymin = conf.low, 
+                     ymax = conf.high)) + 
+   theme_bw() +
+   coord_flip()
~~~
{:.input title="Console"}
![ ]({{ site.baseurl }}/images/broom/unnamed-chunk-4-1.png)
{:.captioned}

===

Use `glance` to retrieve goodness of fit measures and related statistics
as one row per model. The metrics will depend on model type. 



~~~r
> glance(fit1)
~~~
{:.input title="Console"}


~~~
  null.deviance df.null    logLik     AIC     BIC     deviance df.residual
1  1.383328e+13   49315 -533177.3 1066393 1066560 7.099324e+12       49298
~~~
{:.output}


===

Use `augment` to add a column to a dataset containing information such as fitted values,
residuals, or cluster assignments. Column names have a `.` prefix to avoid overwriting
existing column names. The first argument is a model object and the 2nd is data.



~~~r
> acs_cbp2 <- augment(fit1, data = acs_cbp)
> names(acs_cbp2)
~~~
{:.input title="Console"}


~~~
 [1] "FIPS"          "Sector"        "N1_4"          "N5_9"         
 [5] "N10_19"        "N20_49"        "N50_99"        "N100_249"     
 [9] "N250_499"      "N500_999"      "N1000"         "N1000_1"      
[13] "N1000_2"       "N1000_3"       "N1000_4"       "County"       
[17] "median_income" ".fitted"       ".se.fit"       ".resid"       
[21] ".hat"          ".sigma"        ".cooksd"       ".std.resid"   
~~~
{:.output}


