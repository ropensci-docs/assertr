# Concatenate all columns of each row in data frame into a string

This function will return a vector, with the same length as the number
of rows of the provided data frame. Each element of the vector will be
it's corresponding row with all of its values (one for each column)
"pasted" together in a string.

## Usage

``` r
col_concat(data, sep = "")
```

## Arguments

- data:

  A data frame

- sep:

  A string to separate the columns with (default: "")

## Value

A vector of rows concatenated into strings

## See also

[`paste`](https://rdrr.io/r/base/paste.html)

## Examples

``` r

col_concat(mtcars)
#>                       Mazda RX4                   Mazda RX4 Wag 
#>     "2161601103.92.6216.460144"    "2161601103.92.87517.020144" 
#>                      Datsun 710                  Hornet 4 Drive 
#>   "22.84108933.852.3218.611141" "21.462581103.083.21519.441031" 
#>               Hornet Sportabout                         Valiant 
#>  "18.783601753.153.4417.020032"  "18.162251052.763.4620.221031" 
#>                      Duster 360                       Merc 240D 
#>  "14.383602453.213.5715.840034"    "24.44146.7623.693.19201042" 
#>                        Merc 230                        Merc 280 
#>  "22.84140.8953.923.1522.91042" "19.26167.61233.923.4418.31044" 
#>                       Merc 280C                      Merc 450SE 
#> "17.86167.61233.923.4418.91044" "16.48275.81803.074.0717.40033" 
#>                      Merc 450SL                     Merc 450SLC 
#> "17.38275.81803.073.7317.60033"   "15.28275.81803.073.78180033" 
#>              Cadillac Fleetwood             Lincoln Continental 
#>  "10.484722052.935.2517.980034"    "10.4846021535.42417.820034" 
#>               Chrysler Imperial                        Fiat 128 
#> "14.784402303.235.34517.420034"   "32.4478.7664.082.219.471141" 
#>                     Honda Civic                  Toyota Corolla 
#> "30.4475.7524.931.61518.521142"  "33.9471.1654.221.83519.91141" 
#>                   Toyota Corona                Dodge Challenger 
#> "21.54120.1973.72.46520.011031"  "15.583181502.763.5216.870032" 
#>                     AMC Javelin                      Camaro Z28 
#>  "15.283041503.153.43517.30032"  "13.383502453.733.8415.410034" 
#>                Pontiac Firebird                       Fiat X1-9 
#> "19.284001753.083.84517.050032"    "27.3479664.081.93518.91141" 
#>                   Porsche 914-2                    Lotus Europa 
#>    "264120.3914.432.1416.70152" "30.4495.11133.771.51316.91152" 
#>                  Ford Pantera L                    Ferrari Dino 
#>   "15.883512644.223.1714.50154"   "19.761451753.622.7715.50156" 
#>                   Maserati Bora                      Volvo 142E 
#>     "1583013353.543.5714.60158"   "21.441211094.112.7818.61142" 

library(magrittr)            # for piping operator

# you can use "assert_rows", "is_uniq", and this function to
# check if joint duplicates (across different columns) appear
# in a data frame
if (FALSE) { # \dontrun{
mtcars %>%
  assert_rows(col_concat, is_uniq, mpg, hp)
  # fails because the first two rows are jointly duplicates
  # on these two columns
} # }

mtcars %>%
  assert_rows(col_concat, is_uniq, mpg, hp, wt) # ok
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
```
