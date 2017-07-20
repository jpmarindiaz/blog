---
title: Rewriting pystr::pystr_format function in base R
date: '2017-07-20'
---

I recurrently want to render templates like this one: `"Hola {first_name} {last_name}"` with values in a list, like: 

```
template <- "Hola {first_name} {last_name}"
renderMyTemplate(template, list(first_name = "JP", last_name="Marín Díaz"))
# "Hola JP Marín Díaz"
```

I was using the `pystr` package for this. Actually I was using the whole package for only one of its functions: `pystr_format()`.

A few days ago, we realized the the package was no [longer maintained](https://github.com/Ironholds/pystr/issues/11) for the latest R version. Some efforts to keep it alive in CRAN are on the way. For those like myself who only need to format templates here is function to do exactly this using only base R. It works for data.frames too and it happens to be faster than the good old `pystr_format()`, at least in the silly benchmark I performed.


```{r}

tpl_format <- function(tpl, l){
  if(class(l) == "list"){
    listToNameValue <- function(l){
      mapply(function(i,j) list(name = j, value = i), l, names(l), SIMPLIFY = FALSE)
    }
    f <- function(tpl,l){
      gsub(paste0("{",l$name,"}"), l$value, tpl, fixed = TRUE)
    }
    return( Reduce(f,listToNameValue(l), init = tpl))
  }
  if(class(l) == "data.frame"){
    myTranspose <- function(x) lapply(1:nrow(x), function(i) lapply(d, "[[", i))
    return( unlist(lapply(myTranspose(l), function(l, tpl) rep_tpl(tpl, l), tpl = tpl)) )
  }
}

```


```{r test}
tpl <- "{name} fdla {last} {other}"
l <- list(name = "NAME", last = "LAST", other = "OTHER",  mote = "fdasf")
d <- data.frame(name = c("ana","jp"), last = c("heran", "marin"), n = c(1,2))

rep_tpl(tpl, l)
rep_tpl(tpl, d)
pystr::pystr_format(tpl, l)
pystr::pystr_format(tpl, d)

```

```
microbenchmark::microbenchmark(
  rep_tpl(tpl, l),
  pystr::pystr_format(tpl, l)
)
#Unit: microseconds
#                        expr    min       lq      mean   median       uq     max neval
#             rep_tpl(tpl, l) 42.500  47.8885  65.65773  53.3420  58.1765 399.373   100
# pystr::pystr_format(tpl, l) 95.278 105.8865 131.94053 118.6685 128.6940 542.297   100
```

```
microbenchmark::microbenchmark(
  rep_tpl(tpl, d),
  pystr::pystr_format(tpl, d)
)
#Unit: microseconds
#                        expr     min      lq     mean   median       uq      max neval
#             rep_tpl(tpl, d) 154.627 165.006 203.1093 177.5755 210.0555  586.461   100
# pystr::pystr_format(tpl, d) 394.064 416.068 493.6397 443.0620 509.1740 1027.248   100
```


Here is my session Info

```
> sessionInfo()
R version 3.3.2 (2016-10-31)
Platform: x86_64-apple-darwin13.4.0 (64-bit)
Running under: macOS Sierra 10.12.5

locale:
[1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

loaded via a namespace (and not attached):
 [1] colorspace_1.3-2       scales_0.4.1           microbenchmark_1.4-2.1
 [4] lazyeval_0.2.0         plyr_1.8.4             tools_3.3.2           
 [7] gtable_0.2.0           tibble_1.3.3           Rcpp_0.12.11.4        
[10] ggplot2_2.2.1          grid_3.3.2             rlang_0.1.1           
[13] munsell_0.4.3          pystr_2.0.0   
```




