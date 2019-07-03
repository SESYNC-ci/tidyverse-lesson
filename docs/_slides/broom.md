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
{:title="Console" .input}


~~~
Parsed with column specification:
cols(
  FIPS = col_character(),
  Sector = col_character(),
  N1_4 = col_double(),
  N5_9 = col_double(),
  N10_19 = col_double(),
  N20_49 = col_double(),
  N50_99 = col_double(),
  N100_249 = col_double(),
  N250_499 = col_double(),
  N500_999 = col_double(),
  N1000 = col_double(),
  N1000_1 = col_double(),
  N1000_2 = col_double(),
  N1000_3 = col_double(),
  N1000_4 = col_double(),
  County = col_character(),
  median_income = col_double()
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
{:title="Console" .input}


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
{:title="Console" .input}


~~~
# A tibble: 18 x 5
   term                              estimate std.error statistic   p.value
   <chr>                                <dbl>     <dbl>     <dbl>     <dbl>
 1 (Intercept)                         12178.      216.      56.5 0.       
 2 Sectoragriculture forestry fishi…   15790.      317.      49.8 0.       
 3 Sectorarts entertainment and rec…    5665.      317.      17.9 4.77e- 71
 4 Sectorconstruction                  22221.      304.      73.0 0.       
 5 Sectoreducational services          21801.      321.      67.9 0.       
 6 Sectorfinance and insurance         25548.      306.      83.5 0.       
 7 Sectorhealth care and social ass…   16309.      305.      53.6 0.       
 8 Sectorinformation                   23336.      313.      74.6 0.       
 9 Sectormanagement of companies an…   49795.      551.      90.4 0.       
10 Sectormanufacturing                 26274.      306.      85.7 0.       
11 Sectormining quarrying and oil a…   43897.      345.     127.  0.       
12 Sectorother services except publ…    9850.      305.      32.3 7.77e-227
13 Sectorprofessional scientific an…   30326.      307.      98.9 0.       
14 Sectorreal estate and rental and…   19146.      316.      60.5 0.       
15 Sectorretail trade                   8204.      304.      27.0 4.72e-159
16 Sectortransportation and warehou…   28509.      305.      93.4 0.       
17 Sectorutilities                     44643.      317.     141.  0.       
18 Sectorwholesale trade               26766.      308.      86.8 0.       
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
{:title="Console" .input}
![ ]({% include asset.html path="images/broom/unnamed-chunk-4-1.png" %})
{:.captioned}

===

Use `glance` to retrieve goodness of fit measures and related statistics
as one row per model. The metrics will depend on model type. 



~~~r
> glance(fit1)
~~~
{:title="Console" .input}


~~~
# A tibble: 1 x 7
  null.deviance df.null   logLik      AIC      BIC deviance df.residual
          <dbl>   <int>    <dbl>    <dbl>    <dbl>    <dbl>       <int>
1       1.38e13   49315 -533177. 1066393. 1066560.  7.10e12       49298
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
{:title="Console" .input}


~~~
 [1] "FIPS"          "Sector"        "N1_4"          "N5_9"         
 [5] "N10_19"        "N20_49"        "N50_99"        "N100_249"     
 [9] "N250_499"      "N500_999"      "N1000"         "N1000_1"      
[13] "N1000_2"       "N1000_3"       "N1000_4"       "County"       
[17] "median_income" ".fitted"       ".se.fit"       ".resid"       
[21] ".hat"          ".sigma"        ".cooksd"       ".std.resid"   
~~~
{:.output}


