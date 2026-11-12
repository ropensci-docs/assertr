# Raises error if dynamically created predicate is FALSE for any row after applying row reduction function

Meant for use in a data analysis pipeline, this function applies a
function to a data frame that reduces each row to a single value. Then,
a predicate generating function is applied to row reduction values. It
will then use these predicates to check each of the row reduction
values. If any of these predicate applications yield FALSE, this
function will raise an error, effectively terminating the pipeline
early. If there are no FALSEs, this function will just return the data
that it was supplied for further use in later parts of the pipeline.

## Usage

``` r
insist_rows(
  data,
  row_reduction_fn,
  predicate_generator,
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

- row_reduction_fn:

  A function that returns a value for each row of the provided data
  frame

- predicate_generator:

  A function that is applied to the results of the row reduction
  function. This will produce, a true predicate function to be applied
  to every element in the vector that the row reduction function
  returns.

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

By default, the `data` is returned if dynamically created predicate
assertion is TRUE and and error is thrown if not. If a non-default
`success_fun` or `error_fun` is used, the return values of these
function will be returned.

## Details

For examples of possible choices for the `success_fun` and `error_fun`
parameters, run
[`help("success_and_error_functions")`](https://docs.ropensci.org/assertr/reference/success_and_error_functions.md)

## Note

See
[`vignette("assertr")`](https://docs.ropensci.org/assertr/articles/assertr.md)
for how to use this in context

## See also

[`insist`](https://docs.ropensci.org/assertr/reference/insist.md)
[`assert_rows`](https://docs.ropensci.org/assertr/reference/assert_rows.md)
[`assert`](https://docs.ropensci.org/assertr/reference/assert.md)
[`verify`](https://docs.ropensci.org/assertr/reference/verify.md)

## Examples
