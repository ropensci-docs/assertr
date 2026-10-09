# assertr: Assertive programming for R analysis pipeline.

The assertr package supplies a suite of functions designed to verify
assumptions about data early in an analysis pipeline. See the assertr
vignette or the documentation for more information  
\>
[`vignette("assertr")`](https://docs.ropensci.org/assertr/articles/assertr.md)

## Details

You may also want to read the documentation for the functions that
`assertr` provides:

- [`assert`](https://docs.ropensci.org/assertr/reference/assert.md)

- [`verify`](https://docs.ropensci.org/assertr/reference/verify.md)

- [`insist`](https://docs.ropensci.org/assertr/reference/insist.md)

- [`assert_rows`](https://docs.ropensci.org/assertr/reference/assert_rows.md)

- [`insist_rows`](https://docs.ropensci.org/assertr/reference/insist_rows.md)

- [`not_na`](https://docs.ropensci.org/assertr/reference/not_na.md)

- [`in_set`](https://docs.ropensci.org/assertr/reference/in_set.md)

- [`has_all_names`](https://docs.ropensci.org/assertr/reference/has_all_names.md)

- [`is_uniq`](https://docs.ropensci.org/assertr/reference/is_uniq.md)

- [`num_row_NAs`](https://docs.ropensci.org/assertr/reference/num_row_NAs.md)

- [`maha_dist`](https://docs.ropensci.org/assertr/reference/maha_dist.md)

- [`col_concat`](https://docs.ropensci.org/assertr/reference/col_concat.md)

- [`within_bounds`](https://docs.ropensci.org/assertr/reference/within_bounds.md)

- [`within_n_sds`](https://docs.ropensci.org/assertr/reference/within_n_sds.md)

- [`within_n_mads`](https://docs.ropensci.org/assertr/reference/within_n_mads.md)

- [`success_and_error_functions`](https://docs.ropensci.org/assertr/reference/success_and_error_functions.md)

- [`chaining_functions`](https://docs.ropensci.org/assertr/reference/chaining_functions.md)

## Examples

``` r
library(magrittr)     # for the piping operator
library(dplyr)
#> 
#> Attaching package: ‘dplyr’
#> The following objects are masked from ‘package:stats’:
#> 
#>     filter, lag
#> The following objects are masked from ‘package:base’:
#> 
#>     intersect, setdiff, setequal, union

# this confirms that
#   - that the dataset contains more than 10 observations
#   - that the column for 'miles per gallon' (mpg) is a positive number
#   - that the column for 'miles per gallon' (mpg) does not contain a datum
#     that is outside 4 standard deviations from its mean, and
#   - that the am and vs columns (automatic/manual and v/straight engine,
#     respectively) contain 0s and 1s only
#   - each row contains at most 2 NAs
#   - each row's mahalanobis distance is within 10 median absolute deviations of
#     all the distance (for outlier detection)

mtcars %>%
  verify(nrow(.) > 10) %>%
  verify(mpg > 0) %>%
  insist(within_n_sds(4), mpg) %>%
  assert(in_set(0,1), am, vs) %>%
  assert_rows(num_row_NAs, within_bounds(0,2), everything()) %>%
  insist_rows(maha_dist, within_n_mads(10), everything()) %>%
  group_by(cyl) %>%
  summarise(avg.mpg=mean(mpg))
#> # A tibble: 3 × 2
#>     cyl avg.mpg
#>   <dbl>   <dbl>
#> 1     4    26.7
#> 2     6    19.7
#> 3     8    15.1

```
