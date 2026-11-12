# Returns TRUE where no elements appear more than once

This function is meant to take only a vector. It relies heavily on the
[`duplicated`](https://rdrr.io/r/base/duplicated.html) function where it
can be thought of as the inverse. Where this function differs,
though–besides being only meant for one vector or column–is that it
marks the first occurrence of a duplicated value as "non unique", as
well.

## Usage

``` r
is_uniq(..., allow.na = FALSE)
```

## Arguments

- ...:

  One or more vectors to check for unique combinations of elements

- allow.na:

  A logical indicating whether NAs should be preserved as missing values
  in the return value (FALSE) or if they should be treated just like any
  other value (TRUE) (default is FALSE)

## Value

A vector of the same length where the corresponding element is TRUE if
the element only appears once in the vector and FALSE otherwise

## See also

[`duplicated`](https://rdrr.io/r/base/duplicated.html)

## Examples

``` r

is_uniq(1:10)
#>  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
is_uniq(c(1,1,2,3), c(1,2,2,3))
#> [1] TRUE TRUE TRUE TRUE

if (FALSE) { # \dontrun{
# returns FALSE where a "5" appears
is_uniq(c(1:10, 5))
} # }

library(magrittr)

if (FALSE) { # \dontrun{
# this fails 4 times
mtcars %>% assert(is_uniq, qsec)
} # }

# to allow NAs, use `verify`, which hands `is_uniq` the whole column
# (a lambda/anonymous function inside `assert` only ever sees one
# element at a time, so it would never find a duplicate):

df <- data.frame(id = c(1, 2, NA, 4))
df %>%
  verify(is_uniq(id, allow.na=TRUE))
#>   id
#> 1  1
#> 2  2
#> 3 NA
#> 4  4
```
