# Returns TRUE if value is not NA

This is the inverse of [`is.na`](https://rdrr.io/r/base/NA.html). This
is a convenience function meant to be used as a predicate in an
[`assertr`](https://docs.ropensci.org/assertr/reference/assertr.md)
assertion.

## Usage

``` r
not_na(x, allow.NaN = FALSE)
```

## Arguments

- x:

  A R object that supports [is.na](https://rdrr.io/r/base/NA.html) an
  [is.nan](https://rdrr.io/r/base/is.finite.html)

- allow.NaN:

  A logical indicating whether NaNs should be allowed (default FALSE)

## Value

A vector of the same length that is TRUE when the element is not NA and
FALSE otherwise

## See also

[`is.na`](https://rdrr.io/r/base/NA.html)
[`is.nan`](https://rdrr.io/r/base/is.finite.html)

## Examples

``` r
not_na(NA)
#> [1] FALSE
not_na(2.8)
#> [1] TRUE
not_na("tree")
#> [1] TRUE
not_na(c(1, 2, NA, 4))
#> [1]  TRUE  TRUE FALSE  TRUE
```
