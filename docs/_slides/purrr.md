---
---

# Iterate with purrr

===

Use `map_%` functions in purrr for iteration. 



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


