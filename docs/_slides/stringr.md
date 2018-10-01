---
---

# String manipulation

===

We already saw some examples of stringr in the dplyr lesson 
(`str_detect`, `str_c`, `str_remove`), but let's do some more

Remove the word "Sector"" and modify to title case. Notice the use of
`dplyr::pull` to get a vector out of a data frame



~~~r
library(stringr)
library(dplyr)

tidyfit1 %>%
  pull(term) %>%
  str_remove("Sector") %>%
  str_to_title()
~~~
{:.text-document title="worksheet-1.R"}


~~~
 [1] "(Intercept)"                                   
 [2] "Agriculture Forestry Fishing And Hunting"      
 [3] "Arts Entertainment And Recreation"             
 [4] "Construction"                                  
 [5] "Educational Services"                          
 [6] "Finance And Insurance"                         
 [7] "Health Care And Social Assistance"             
 [8] "Information"                                   
 [9] "Management Of Companies And Enterprises"       
[10] "Manufacturing"                                 
[11] "Mining Quarrying And Oil And Gas Extraction"   
[12] "Other Services Except Public Administration"   
[13] "Professional Scientific And Technical Services"
[14] "Real Estate And Rental And Leasing"            
[15] "Retail Trade"                                  
[16] "Transportation And Warehousing"                
[17] "Utilities"                                     
[18] "Wholesale Trade"                               
~~~
{:.output}


===

Use purrr for iteration!



~~~r
> library(purrr)
> tidyfit1 <- tidyfit1 %>%
+   mutate(term = map_chr(term, 
+           ~str_remove(., "Sector") %>% 
+            str_to_title())) 
~~~
{:.input title="Console"}




~~~r
tidyfit1$term
~~~
{:.text-document title="Console"}


~~~
 [1] "(Intercept)"                                   
 [2] "Agriculture Forestry Fishing And Hunting"      
 [3] "Arts Entertainment And Recreation"             
 [4] "Construction"                                  
 [5] "Educational Services"                          
 [6] "Finance And Insurance"                         
 [7] "Health Care And Social Assistance"             
 [8] "Information"                                   
 [9] "Management Of Companies And Enterprises"       
[10] "Manufacturing"                                 
[11] "Mining Quarrying And Oil And Gas Extraction"   
[12] "Other Services Except Public Administration"   
[13] "Professional Scientific And Technical Services"
[14] "Real Estate And Rental And Leasing"            
[15] "Retail Trade"                                  
[16] "Transportation And Warehousing"                
[17] "Utilities"                                     
[18] "Wholesale Trade"                               
~~~
{:.output}


===

str_trunc for truncating



~~~r
> tidyfit1 %>%
+   mutate(term = map_chr(term, 
+           ~str_trunc(., 30, side = "right", ellipsis = "")))
~~~
{:.input title="Console"}


~~~
                             term  estimate std.error statistic
1                     (Intercept) 12177.778  215.6370  56.47352
2  Agriculture Forestry Fishing A 15790.308  317.2988  49.76479
3  Arts Entertainment And Recreat  5664.618  317.3309  17.85082
4                    Construction 22220.913  304.3456  73.01210
5            Educational Services 21800.994  320.9289  67.93092
6           Finance And Insurance 25548.393  305.9275  83.51126
7  Health Care And Social Assista 16309.403  304.5159  53.55846
8                     Information 23335.758  312.9391  74.56965
9  Management Of Companies And En 49795.072  551.0509  90.36383
10                  Manufacturing 26274.310  306.4083  85.74933
11 Mining Quarrying And Oil And G 43897.054  344.9798 127.24528
12 Other Services Except Public A  9850.114  304.7358  32.32346
13 Professional Scientific And Te 30326.366  306.6891  98.88309
14 Real Estate And Rental And Lea 19145.623  316.2501  60.53950
15                   Retail Trade  8203.758  304.1761  26.97043
16 Transportation And Warehousing 28509.098  305.2284  93.40251
17                      Utilities 44643.180  316.8512 140.89638
18                Wholesale Trade 26765.918  308.3853  86.79374
         p.value  conf.low conf.high
1   0.000000e+00 11755.138 12600.419
2   0.000000e+00 15168.414 16412.202
3   4.771120e-71  5042.661  6286.575
4   0.000000e+00 21624.406 22817.419
5   0.000000e+00 21171.985 22430.003
6   0.000000e+00 24948.786 26147.999
7   0.000000e+00 15712.563 16906.243
8   0.000000e+00 22722.409 23949.107
9   0.000000e+00 48715.032 50875.111
10  0.000000e+00 25673.760 26874.859
11  0.000000e+00 43220.906 44573.202
12 7.772501e-227  9252.843 10447.385
13  0.000000e+00 29725.267 30927.466
14  0.000000e+00 18525.784 19765.462
15 4.719179e-159  7607.584  8799.932
16  0.000000e+00 27910.861 29107.334
17  0.000000e+00 44022.163 45264.197
18  0.000000e+00 26161.494 27370.343
~~~
{:.output}


===


