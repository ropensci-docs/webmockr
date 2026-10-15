# Expectation for what's returned from a stubbed request

Set response status code, response body, and/or response headers

## Usage

``` r
to_return(.data, ..., .list = list(), times = 1)
```

## Arguments

- .data:

  input. Anything that can be coerced to a `StubbedRequest` class object

- ...:

  Comma separated list of named variables. accepts the following:
  `status`, `body`, `headers`. See Details for more.

- .list:

  named list, has to be one of 'status', 'body', and/or 'headers'. An
  alternative to passing in via `...`. Don't pass the same thing to
  both, e.g. don't pass 'status' to `...`, and also 'status' to this
  parameter

- times:

  (integer) number of times the given response should be returned;
  default: 1. value must be greater than or equal to 1. Very large
  values probably don't make sense, but there's no maximum value. See
  Details.

## Value

an object of class `StubbedRequest`, with print method describing the
stub

## Details

Values for status, body, and headers:

- status: (numeric/integer) three digit status code

- body: various: `character`, `json`, `list`, `raw`, `numeric`, `NULL`,
  `FALSE`, a file connection (other connetion types not supported), or a
  `mock_file` function call (see
  [`mock_file()`](https://docs.ropensci.org/webmockr/reference/mock_file.md))

- headers: (list) a named list, must be named

response headers are returned with all lowercase names and the values
are all of type character. if numeric/integer values are given (e.g.,
`to_return(headers = list(a = 10))`), we'll coerce any numeric/integer
values to character.

## Note

see more examples in
[`stub_request()`](https://docs.ropensci.org/webmockr/reference/stub_request.md)

## multiple `to_return()`

You can add more than one `to_return()` to a webmockr stub (including
[`to_raise()`](https://docs.ropensci.org/webmockr/reference/to_raise.md),
[`to_timeout()`](https://docs.ropensci.org/webmockr/reference/to_timeout.md)).
Each one is a HTTP response returned. That is, you'll match to an HTTP
request based on
[`stub_request()`](https://docs.ropensci.org/webmockr/reference/stub_request.md)
and [`wi_th()`](https://docs.ropensci.org/webmockr/reference/wi_th.md);
the first time the request is made, the first response is returned; the
second time the request is made, the second response is returned; and so
on.

Be aware that webmockr has to track number of requests (see
[`request_registry()`](https://docs.ropensci.org/webmockr/reference/request_registry.md)),
and so if you use multiple `to_return()` or the `times` parameter, you
must clear the request registry in order to go back to mocking responses
from the start again.
[`webmockr_reset()`](https://docs.ropensci.org/webmockr/reference/webmockr_reset.md)
clears the stub registry and the request registry, after which you can
use multiple responses again (after creating your stub(s) again of
course)

## Raise vs. Return

[`to_raise()`](https://docs.ropensci.org/webmockr/reference/to_raise.md)
always raises a stop condition, while `to_return(status=xyz)` only sets
the status code on the returned HTTP response object. So if you want to
raise a stop condition then
[`to_raise()`](https://docs.ropensci.org/webmockr/reference/to_raise.md)
is what you want. But if you don't want to raise a stop condition use
`to_return()`. Use cases for each vary. For example, in a unit test you
may have a test expecting a 503 error; in this case
[`to_raise()`](https://docs.ropensci.org/webmockr/reference/to_raise.md)
makes sense. In another case, if a unit test expects to test some aspect
of an HTTP response object that httr, httr2, or crul typically returns,
then you'll want `to_return()`.

## Examples

``` r
# first, make a stub object
foo <- function() {
  stub_request("post", "https://httpbin.org/post")
}

# add status, body and/or headers
foo() %>% to_return(status = 200)
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 200
#>     body: 
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
foo() %>% to_return(body = "stuff")
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: stuff
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
foo() %>% to_return(body = list(a = list(b = "world")))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: a = list(b = "world")
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
foo() %>% to_return(headers = list(a = 5))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: 
#>     response_headers: a=5
#>     should_timeout: FALSE
#>     should_raise: FALSE
foo() %>%
  to_return(status = 200, body = "stuff", headers = list(a = 5))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 200
#>     body: stuff
#>     response_headers: a=5
#>     should_timeout: FALSE
#>     should_raise: FALSE

# .list - pass in a named list instead
foo() %>% to_return(.list = list(body = list(foo = "bar")))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: foo=bar
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE

# multiple responses using chained `to_return()`
foo() %>%
  to_return(body = "stuff") %>%
  to_return(body = "things")
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: stuff
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
#>   - status: 
#>     body: things
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE

# many of the same response using the times parameter
foo() %>% to_return(body = "stuff", times = 3)
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: stuff
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
#>   - status: 
#>     body: stuff
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
#>   - status: 
#>     body: stuff
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
```
