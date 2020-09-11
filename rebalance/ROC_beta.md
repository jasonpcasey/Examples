ROC\_beta
================

``` r
library(ggplot2)
```

    ## Warning: replacing previous import 'vctrs::data_frame' by 'tibble::data_frame'
    ## when loading 'dplyr'

``` r
mk_curve <- function(a, b, left = 0, right = 1) {
  d <- data.frame(
    t = seq(left, right, length.out = 101)
  )
  d$x <- 1 - pbeta(d$t, shape1 = a, shape2 = b)
  d$y <- 1 - pbeta(d$t, shape1 = b, shape2 = a)
  d$a <- a
  d$b <- b
  d$what <- paste0('a=', a, ', b=', b)
  d
}

plot_curve_pair <- function(a1, b1, a2, b2, left = 0, right = 1) {
  d1 <- mk_curve(a1, b1, left = left, right = right)
  d2 <- mk_curve(a2, b2, left = left, right = right)
  
  ggplot() + 
    geom_line(data = d1,
              mapping = aes(x = x, y = y),
              color = 'DarkGreen') +
    geom_line(data = d2,
              mapping = aes(x = x, y = y),
              color = "Purple") + 
    theme(aspect.ratio = 1) +
    ggtitle(paste0(
      'a1=', a1,
      ', b1=', b1,
      ', a2=', a2,
      ', b2=', b2
    ))
}

plot_curve_pair(2, 3.1, 1.93, 3)
```

![](ROC_beta_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
plot_curve_pair(2, 3.1, 3, 3)
```

![](ROC_beta_files/figure-gfm/unnamed-chunk-2-2.png)<!-- -->

``` r
plot_curve_pair(6, 14, 3, 7)
```

![](ROC_beta_files/figure-gfm/unnamed-chunk-2-3.png)<!-- -->

``` r
plot_curve_pair(1, 3, 2, 5)
```

![](ROC_beta_files/figure-gfm/unnamed-chunk-2-4.png)<!-- -->

``` r
d <- data.frame(
    t = seq(0, 1, length.out = 101)
  )
d$c <- pbeta(d$t, shape1 = 1, shape2 = 3)
d$d <- pbeta(d$t, shape1 = 2, shape2 = 5)

ggplot(data = d) +
  geom_line(mapping = aes(x = t, y = c), color = "DarkGreen") +
  geom_line(mapping = aes(x = t, y = d), color = "Purple") +
  theme(aspect.ratio = 1) +
  ggtitle("crossing CDFs")
```

![](ROC_beta_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
plot_curve_pair(1, 3, 2, 5, left = 0.275, right = 0.5)
```

![](ROC_beta_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
plot_curve_pair(1, 3, 2, 5, left = 0.0, right = 0.1)
```

![](ROC_beta_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->