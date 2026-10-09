# Generates random ID string

This is used to generate id for each assertion error.

## Usage

``` r
generate_id()
```

## Details

For single assertion that checks multiple columns, each error log is
stored as a separate element. We provide the ID to allow detecting which
errors come from the same assertion.
