# Raises error if predicate is FALSE in any columns selected

Meant for use in a data analysis pipeline, this function will just
return the data it's supplied if there are no FALSEs when the predicate
is applied to every element of the columns indicated. If any element in
any of the columns, when applied to the predicate, is FALSE, then this
function will raise an error, effectively terminating the pipeline
early.

## Usage

``` r
assert(
  data,
  predicate,
  ...,
  success_fun = success_continue,
  error_fun = error_stop,
  skip_chain_opts = FALSE,
  obligatory = FALSE,
  defect_fun = defect_append,
  description = NA
)
```

## Arguments

- data:

  A data frame

- predicate:

  A function that returns FALSE when violated

- ...:

  Comma separated list of unquoted expressions. Uses dplyr's `select` to
  select columns from data.

- success_fun:

  Function to call if assertion passes. Defaults to returning `data`.

- error_fun:

  Function to call if assertion fails. Defaults to printing a summary of
  all errors.

- skip_chain_opts:

  If TRUE, `success_fun` and `error_fun` are used even if assertion is
  called within a chain.

- obligatory:

  If TRUE and assertion failed the data is marked as defective. For
  defective data, all the following rules are handled by `defect_fun`
  function.

- defect_fun:

  Function to call when data is defective. Defaults to skipping
  assertion and storing info about it in special attribute.

- description:

  Custom description of the rule. Is stored in result reports and data.

## Value

By default, the `data` is returned if predicate assertion is TRUE and
and error is thrown if not. If a non-default `success_fun` or
`error_fun` is used, the return values of these function will be
returned.

## Details

For examples of possible choices for the `success_fun` and `error_fun`
parameters, run
[`help("success_and_error_functions")`](https://docs.ropensci.org/assertr/reference/success_and_error_functions.md)

## Note

See
[`vignette("assertr")`](https://docs.ropensci.org/assertr/articles/assertr.md)
for how to use this in context

## See also

[`verify`](https://docs.ropensci.org/assertr/reference/verify.md)
[`insist`](https://docs.ropensci.org/assertr/reference/insist.md)
[`assert_rows`](https://docs.ropensci.org/assertr/reference/assert_rows.md)
[`insist_rows`](https://docs.ropensci.org/assertr/reference/insist_rows.md)

## Examples
