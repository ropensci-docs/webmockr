# Get a diff of a stub request body and a request body from an http request

Requires the Suggested package `diffobj`

## Usage

``` r
stub_body_diff(stub = last_stub(), request = last_request())
```

## Arguments

- stub:

  object of class `StubbedRequest`. required. default is to call
  [`last_stub()`](https://docs.ropensci.org/webmockr/reference/last_stub.md),
  which gets the last stub created

- request:

  object of class `RequestSignature`. required. default is to call
  [`last_request()`](https://docs.ropensci.org/webmockr/reference/last_request.md),
  which gets the last stub created

## Value

object of class `Diff` from the diffobj package

## Details

Returns error message if either `stub` or `request` are `NULL`. Even
though you may not intentionally pass in a `NULL`, the return values of
[`last_stub()`](https://docs.ropensci.org/webmockr/reference/last_stub.md)
and
[`last_request()`](https://docs.ropensci.org/webmockr/reference/last_request.md)
when there's nothing found is `NULL`.

Under the hood the Suggested package `diffobj` is used to do the
comparison.

## See also

[`webmockr_configure()`](https://docs.ropensci.org/webmockr/reference/webmockr_configure.md)
to toggle `webmockr` showing request body diffs when there's not a
match. `stub_body_diff()` is offered as a manual way to compare requests
and stubs - whereas turning on with
[`webmockr_configure()`](https://docs.ropensci.org/webmockr/reference/webmockr_configure.md)
will do the diff for you.

## Examples

``` r
if (FALSE) { # interactive()
# stops with error if no stub and request
request_registry_clear()
stub_registry_clear()
stub_body_diff()

# Gives diff when there's a stub and request found - however, no request body
stub_request("get", "https://hb.opencpu.org/get")
enable()
library(crul)
HttpClient$new("https://hb.opencpu.org")$get(path = "get")
stub_body_diff()

# Gives diff when there's a stub and request found - with request body
stub_request("post", "https://hb.opencpu.org/post") %>%
  wi_th(body = list(apple = "green"))
enable()
library(crul)
HttpClient$new("https://hb.opencpu.org")$post(
  path = "post", body = list(apple = "red")
)
stub_body_diff()

# Gives diff when there's a stub and request found - with request body
stub_request("post", "https://hb.opencpu.org/post") %>%
  wi_th(body = "the quick brown fox")
HttpClient$new("https://hb.opencpu.org")$post(
  path = "post", body = "the quick black fox"
)
stub_body_diff()
}
```
