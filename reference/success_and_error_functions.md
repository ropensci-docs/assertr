# Success and error functions

The behavior of functions like `assert`, `assert_rows`, `insist`,
`insist_rows`, `verify` when the assertion passes or fails is
configurable via the `success_fun` and `error_fun` parameters,
respectively. The `success_fun` parameter takes a function that takes
the data passed to the assertion function as a parameter. You can write
your own success handler function, but there are a few provided by this
package:

- `success_continue` - just returns the data that was passed into the
  assertion function

- `success_logical` - returns TRUE

- `success_append` - returns the data that was passed into the assertion
  function but also stores basic information about verification result

- `success_report` - When success results are stored, and each
  verification ended up with success prints summary of all successful
  validations

- `success_df_return` - When success results are stored, and each
  verification ended up with success prints data.frame with verification
  results

The `error_fun` parameter takes a function that takes the data passed to
the assertion function as a parameter. You can write your own error
handler function, but there are a few provided by this package:

- `error_stop` - Prints a summary of the errors and halts execution.

- `error_report` - Prints all the information available about the errors
  in a "tidy" `data.frame` (including information such as the name of
  the predicate used, the offending value, etc...) and halts execution.

- `error_append` - Attaches the errors to a special attribute of `data`
  and returns the data. This is chiefly to allow assertr errors to be
  accumulated in a pipeline so that all assertions can have a chance to
  be checked and so that all the errors can be displayed at the end of
  the chain.

- `error_return` - Returns the raw object containing all the errors

- `error_df_return` - Returns a "tidy" `data.frame` containing all the
  errors, including informations such as the name of the predicate used,
  the offending value, etc...

- `error_logical` - returns FALSE

- `just_warn` - Prints a summary of the errors but does not halt
  execution, it just issues a warning.

- `warn_report` - Prints all the information available about the errors
  but does not halt execution, it just issues a warning.

- `defect_report` - For single rule and defective data it displays short
  info about skipping current assertion. For `chain_end` sums up all
  skipped rules for defective data.

- `defect_df_return` - For single rule and defective data it returns
  info data.frame about skipping current assertion. For `chain_end`
  returns all skipped rules info data.frame for defective data.

You may find the third type of data verification result. In a scenario
when validation rule was obligatory (obligatory = TRUE) in order to
execute the following ones we may want to skip them and register that
fact. In order to do this there are three callbacks reacting to
defective data:

- `defect_report` - For single rule and defective data it displays short
  info about skipping current assertion.

- `defect_df_return` - For single rule and defective data it returns
  info data.frame about skipping current assertion.

- `defect_append` - Appends info about skipped rule due to data defect
  into one of data attributes. Rules skipped on defective data, or its
  summary, can be returned with proper error_fun callback in
  `chain_end`.

## Usage

``` r
success_logical(data, ...)

success_continue(data, ...)

success_append(data, ...)

success_report(data, ...)

success_df_return(data, ...)

error_stop(errors, data = NULL, warn = FALSE, ...)

just_warn(errors, data = NULL)

error_report(errors, data = NULL, warn = FALSE, ...)

warn_report(errors, data = NULL)

error_append(errors, data = NULL)

warning_append(errors, data = NULL)

error_return(errors, data = NULL)

error_df_return(errors, data = NULL)

error_logical(errors, data = NULL, ...)

defect_append(errors, data, ...)

defect_report(errors, data, ...)

defect_df_return(errors, data, ...)
```

## Arguments

- data:

  A data frame

- ...:

  Further arguments passed to or from other methods

- errors:

  A list of objects of class `assertr_errors`

- warn:

  If TRUE, assertr will issue a warning instead of an error
