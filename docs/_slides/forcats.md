---
---

# Embrace factors

forcats for factors. not to be confused with forecast. This could go in a different spot of the lesson

===

Make the model term column a factor to use `fct_reorder` for sorting.



~~~r
> library(forcats)
> 
> tidyfit1 %>%
+   mutate(term = as_factor(term)) %>%
+   mutate(term = fct_reorder(term, estimate)) %>%
+   ggplot(aes(x = term, y = estimate)) +
+   geom_point() +
+   geom_errorbar(aes(ymin = conf.low, ymax = conf.high)) + 
+   theme_bw() +
+   coord_flip()
~~~
{:.input title="Console"}
![ ]({{ site.baseurl }}/images/forcats/unnamed-chunk-1-1.png)
{:.captioned}



