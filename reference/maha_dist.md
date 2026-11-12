# Computes mahalanobis distance for each row of data frame

This function will return a vector, with the same length as the number
of rows of the provided data frame, corresponding to the average
mahalanobis distances of each row from the whole data set.

## Usage

``` r
maha_dist(data, keep.NA = TRUE, robust = FALSE, stringsAsFactors = FALSE)
```

## Arguments

- data:

  A data frame

- keep.NA:

  Ensure that every row with missing data remains NA in the output? TRUE
  by default.

- robust:

  Attempt to compute mahalanobis distance based on robust covariance
  matrix? FALSE by default

- stringsAsFactors:

  Convert non-factor string columns into factors? FALSE by default

## Value

A vector of observation-wise mahalanobis distances.

## Details

This is useful for finding anomalous observations, row-wise.

It will convert any categorical variables in the data frame into
numerics as long as they are factors. For example, in order for a
character column to be used as a component in the distance calculations,
it must either be a factor, or converted to a factor by using the
`stringsAsFactors` parameter.

## See also

[`insist_rows`](https://docs.ropensci.org/assertr/reference/insist_rows.md)

## Examples

``` r

maha_dist(mtcars)
#>  [1]  8.946673  8.287933  8.937150  6.096726  5.429061  8.877558  9.136276
#>  [8] 10.030345 22.593116 12.393107 11.058878  9.476126  5.594527  6.026462
#> [15] 11.201310  8.672093 12.257618  9.078630 14.954377 10.296463 13.432391
#> [22]  6.227235  5.786691 11.681526  6.718085  3.645789 18.356164 14.000669
#> [29] 21.573003 11.152850 19.192384  9.888781

maha_dist(iris, robust=TRUE)
#>   [1]  7.181303 14.209332  9.233412 14.029571  6.547538  9.032628  9.557745
#>   [8]  9.434082 16.327924 14.609934  7.944119 12.241370 14.152604 10.634152
#>  [15]  8.940285  9.311006  7.996840  7.676170 10.686693  6.772707 14.171183
#>  [22]  8.199367  4.819010 17.927827 21.970559 17.509804 12.134829  8.718618
#>  [29]  8.664029 14.539774 15.467206 13.918214 12.751421  7.800228 13.513486
#>  [36]  9.613279  9.535921  8.718478 13.079168  9.504772  7.041884 36.721567
#>  [43] 10.581647 18.598838 14.208248 15.428511  9.871731 10.898606  7.630712
#>  [50]  9.183846 12.142542  5.700266 15.153194  9.430086 12.108781 11.172977
#>  [57]  9.444704  5.395403 11.484362  7.646899 10.479824  5.254603 14.996254
#>  [64] 11.744912  2.849079  6.677997 10.917922  9.978773 24.822657  4.694515
#>  [71] 20.355909  3.146007 22.559940 18.395726  5.389387  6.864585 17.525227
#>  [78] 19.539023  8.151810  3.098777  4.944060  5.362978  2.057880 26.155842
#>  [85] 14.053245  8.768882 10.215374 17.593198  3.270086  5.936323 13.524049
#>  [92]  8.625081  3.824912  5.800611  5.591581  5.707430  3.987159  4.389560
#>  [99]  9.471902  3.068005 30.970783 32.288310 16.382188 27.303966 18.252965
#> [106] 14.211336 57.834820 27.316610 17.104499 29.976800 42.865459 24.851409
#> [113] 25.740563 34.263970 56.920919 43.839091 29.769508 30.314755  8.766718
#> [120] 35.514678 27.338244 44.696221 18.955613 38.729456 26.599257 32.185485
#> [127] 44.286331 45.304056 18.655092 42.634687 19.136274 40.640072 20.651593
#> [134] 46.870404 53.923075 20.573812 41.472972 33.431351 49.320574 31.907998
#> [141] 34.144669 57.844485 32.288310 20.731382 39.082779 47.916444 32.925457
#> [148] 34.182320 45.599451 41.065734


library(magrittr)            # for piping operator
library(dplyr)               # for "everything()" function

# using every column from mtcars, compute mahalanobis distance
# for each observation, and ensure that each distance is within 10
# median absolute deviations from the median
mtcars %>%
  insist_rows(maha_dist, within_n_mads(10), everything())
#>                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb
#> Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
#> Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
#> Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
#> Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
#> Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
#> Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1
#> Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
#> Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
#> Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
#> Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4
#> Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4
#> Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
#> Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
#> Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
#> Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4
#> Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4
#> Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4
#> Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
#> Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
#> Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
#> Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1
#> Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
#> AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2
#> Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4
#> Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2
#> Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
#> Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
#> Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
#> Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4
#> Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6
#> Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8
#> Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2
  ## anything here will run
```
