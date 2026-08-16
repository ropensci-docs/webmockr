# Set raise error condition

Set raise error condition

## Usage

``` r
to_raise(.data, ...)
```

## Arguments

- .data:

  input. Anything that can be coerced to a `StubbedRequest` class object

- ...:

  One or more HTTP exceptions from the fauxpas package. Run
  `grep("HTTP*", getNamespaceExports("fauxpas"), value = TRUE)` for a
  list of possible exceptions

## Value

an object of class `StubbedRequest`, with print method describing the
stub

## Details

The behavior in the future will be:

When multiple exceptions are passed, the first is used on the first
mock, the second on the second mock, and so on. Subsequent mocks use the
last exception

But for now, only the first exception is used until we get that fixed

## Note

see examples in
[`stub_request()`](https://docs.ropensci.org/webmockr/reference/stub_request.md)

## Raise vs. Return

`to_raise()` always raises a stop condition, while
`to_return(status=xyz)` only sets the status code on the returned HTTP
response object. So if you want to raise a stop condition then
`to_raise()` is what you want. But if you don't want to raise a stop
condition use
[`to_return()`](https://docs.ropensci.org/webmockr/reference/to_return.md).
Use cases for each vary. For example, in a unit test you may have a test
expecting a 503 error; in this case `to_raise()` makes sense. In another
case, if a unit test expects to test some aspect of an HTTP response
object that httr, httr2, or crul typically returns, then you'll want
[`to_return()`](https://docs.ropensci.org/webmockr/reference/to_return.md).
