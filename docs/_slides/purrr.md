---
---

# Iterate with purrr

===

We already used stringr in the dplyr lesson to modify NAICS codes: `str_detect`, `str_c`, `str_remove`

Here we will manipulate the "term"" column of the `broom` output to improve figure axis labels. Load `stringr`

Load `stringr` as well as `dplyr`.



~~~r
> library(stringr)
> library(dplyr)
~~~
{:.input title="Console"}


~~~

Attaching package: 'dplyr'
~~~
{:.output}


~~~
The following objects are masked from 'package:stats':

    filter, lag
~~~
{:.output}


~~~
The following objects are masked from 'package:base':

    intersect, setdiff, setequal, union
~~~
{:.output}


===

Use `dplyr`'s `pull` function to extract the column "term" from the tidyfit1 data frame. 
Remove the word "Sector" and modify to title case.



~~~r
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

Another handy function in `stringr` truncates long strings



~~~r
> tidyfit1 %>%
+   pull(term) %>%
+   str_remove("Sector") %>%
+   str_to_title() %>%
+   str_trunc(30, side = "right", ellipsis = "")
~~~
{:.input title="Console"}


~~~
 [1] "(Intercept)"                    "Agriculture Forestry Fishing A"
 [3] "Arts Entertainment And Recreat" "Construction"                  
 [5] "Educational Services"           "Finance And Insurance"         
 [7] "Health Care And Social Assista" "Information"                   
 [9] "Management Of Companies And En" "Manufacturing"                 
[11] "Mining Quarrying And Oil And G" "Other Services Except Public A"
[13] "Professional Scientific And Te" "Real Estate And Rental And Lea"
[15] "Retail Trade"                   "Transportation And Warehousing"
[17] "Utilities"                      "Wholesale Trade"               
~~~
{:.output}


===

A core syntax element of the tidyverse is the **piped workflow** where the object on the left-hand side of `%>%` becomes the first argument to the function on the right-hand side. This reduces intermediate objects filling up your workspace and can improve readability. 



~~~r
term1 <- pull(tidyfit1, term)
term2 <- str_remove(term1, "Sector")
term3 <- str_to_title(term2)
~~~
{:.text-document title="worksheet-1.R"}


or 



~~~r
> str_to_title(str_remove(pull(tidyfit1, term), "Sector"))
~~~
{:.input title="Console"}


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

Another core tidyverse method is to use `purrr`'s `map_` functions for iteration, instead of for loops, s/l/apply functions, or copy-paste. Here we use `map_chr` to create the new term vector within a mutate function. The `.` represents each item from the first argument to be iterated over and the `~` is an anonymous function. `map_chr` returns a character vector. 



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


