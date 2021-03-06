---
---

# Embrace factors

`forcats` is for factors. Not to be confused with the `forecast` package.

===

Make the model term column a factor to use `fct_reorder` for sorting.



~~~r
> library(forcats)
> 
> tidyfit1 %>%
+   mutate(term = as_factor(term)) %>%
+   mutate(
+     term = fct_reorder(term, estimate)) %>%
+   ggplot(aes(x = term, y = estimate)) +
+   geom_point() +
+   geom_errorbar(aes(ymin = conf.low, 
+                     ymax = conf.high)) + 
+   theme_bw() +
+   coord_flip()
~~~
{:title="Console" .input}
![ ]({% include asset.html path="images/forcats/unnamed-chunk-1-1.png" %})
{:.captioned}

===

`fct_collapse` to combine factors



~~~r
> # example
~~~
{:title="Console" .input}



