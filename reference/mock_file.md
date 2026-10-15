# Mock file

Mock file

## Usage

``` r
mock_file(path, payload)
```

## Arguments

- path:

  (character) a file path. required

- payload:

  (character) string to be written to the file given at `path`
  parameter. required

## Value

a list with S3 class `mock_file`

## Examples

``` r
mock_file(path = tempfile(), payload = "{\"foo\": \"bar\"}")
#> <mock file>
#>  path: /tmp/RtmpiDSAHW/file6122c9b5789
#>  payload: {"foo": "bar"}
```
