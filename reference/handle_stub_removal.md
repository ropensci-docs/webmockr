# Handle stub removal

Handle stub removal

## Usage

``` r
handle_stub_removal(.data, code)
```

## Arguments

- .data:

  an object of class `StubbedRequest` required

- code:

  a code block. required

## Value

if no error, the result of running `code`; if an error occurs
[`withCallingHandlers()`](https://rdrr.io/r/base/conditions.html) throws
a warning and then the stub is removed
