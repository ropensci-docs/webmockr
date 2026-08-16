# Getting Started

Load webmockr

``` r

library(webmockr)
```

Enable webmockr

``` r

webmockr::enable()
```

    ## CrulAdapter enabled!

    ## HttrAdapter enabled!

    ## Httr2Adapter enabled!

## Inside a test framework

``` r

library(crul)
```

    ## Warning: package 'crul' was built under R version 4.6.1

``` r

library(testthat)

# make a stub
stub_request("get", "https://httpbin.org/get") %>%
  to_return(body = "success!", status = 200)
```

    ## <webmockr stub> 
    ##   method: get
    ##   uri: https://httpbin.org/get
    ##   with: 
    ##     query: 
    ##     body: 
    ##     request_headers: 
    ##     auth: 
    ##   to_return: 
    ##   - status: 200
    ##     body: success!
    ##     response_headers: 
    ##     should_timeout: FALSE
    ##     should_raise: FALSE

``` r

# check that it's in the stub registry
stub_registry()
```

    ## <webmockr stub registry> 
    ##  Registered Stubs
    ##   GET: https://httpbin.org/get    | to_return:   with body "success!"  with status 200

``` r

# make the request
z <- crul::HttpClient$new(url = "https://httpbin.org")$get("get")

# run tests (nothing returned means it passed)
expect_is(z, "HttpResponse")
```

    ## Warning: `expect_is()` was deprecated in the 3rd edition.
    ## ℹ Use `expect_type()`, `expect_s3_class()`, or `expect_s4_class()` instead

``` r

expect_equal(z$status_code, 200)
expect_equal(z$parse("UTF-8"), "success!")
```

## Outside a test framework

``` r

library(crul)
```

### Stubbed request based on uri only and with the default response

``` r

stub_request("get", "https://httpbin.org/get")
```

    ## <webmockr stub> 
    ##   method: get
    ##   uri: https://httpbin.org/get
    ##   with: 
    ##     query: 
    ##     body: 
    ##     request_headers: 
    ##     auth: 
    ##   to_return:

``` r

x <- HttpClient$new(url = "https://httpbin.org")
x$get('get')
```

    ## <crul response> 
    ##   url: https://httpbin.org/get
    ##   request_headers: 
    ##     User-Agent: libcurl/8.5.0 r-curl/7.1.0 crul/1.6.0.9000
    ##     Accept-Encoding: gzip, deflate
    ##     Accept: application/json, text/xml, application/xml, */*
    ##   response_headers: 
    ##   status: 200

set return objects

``` r

stub_request("get", "https://httpbin.org/get") %>%
  wi_th(
    query = list(hello = "world")
  ) %>%
  to_return(status = 418)
```

    ## <webmockr stub> 
    ##   method: get
    ##   uri: https://httpbin.org/get
    ##   with: 
    ##     query: hello=world
    ##     body: 
    ##     request_headers: 
    ##     auth: 
    ##   to_return: 
    ##   - status: 418
    ##     body: 
    ##     response_headers: 
    ##     should_timeout: FALSE
    ##     should_raise: FALSE

``` r

x$get('get', query = list(hello = "world"))
```

    ## <crul response> 
    ##   url: https://httpbin.org/get
    ##   request_headers: 
    ##     User-Agent: libcurl/8.5.0 r-curl/7.1.0 crul/1.6.0.9000
    ##     Accept-Encoding: gzip, deflate
    ##     Accept: application/json, text/xml, application/xml, */*
    ##   response_headers: 
    ##   status: 418

### Stubbing requests based on method, uri and query params

``` r

stub_request("get", "https://httpbin.org/get") %>%
  wi_th(
    query = list(hello = "world"),
    headers = list(
      'User-Agent' = 'libcurl/7.51.0 r-curl/2.6 crul/0.3.6',
      'Accept-Encoding' = "gzip, deflate"
    )
  )
```

    ## <webmockr stub> 
    ##   method: get
    ##   uri: https://httpbin.org/get
    ##   with: 
    ##     query: hello=world
    ##     body: 
    ##     request_headers: User-Agent=libcurl/7.51.0 r-cur..., Accept-Encoding=gzip, deflate
    ##     auth: 
    ##   to_return:

``` r

stub_registry()
```

    ## <webmockr stub registry> 
    ##  Registered Stubs
    ##   GET: https://httpbin.org/get
    ##   GET: https://httpbin.org/get  with query params hello=world   | to_return:    with status 418
    ##   GET: https://httpbin.org/get  with query params hello=world   with headers {"User-Agent":"libcurl/7.51.0 r-curl/2.6 crul/0.3.6","Accept-Encoding":"gzip, deflate"}

``` r

x <- HttpClient$new(url = "https://httpbin.org")
x$get('get', query = list(hello = "world"))
```

    ## <crul response> 
    ##   url: https://httpbin.org/get
    ##   request_headers: 
    ##     User-Agent: libcurl/8.5.0 r-curl/7.1.0 crul/1.6.0.9000
    ##     Accept-Encoding: gzip, deflate
    ##     Accept: application/json, text/xml, application/xml, */*
    ##   response_headers: 
    ##   status: 418

### Stubbing requests and set expectation of a timeout

``` r

stub_request("post", "https://httpbin.org/post") %>% to_timeout()
```

    ## <webmockr stub> 
    ##   method: post
    ##   uri: https://httpbin.org/post
    ##   with: 
    ##     query: 
    ##     body: 
    ##     request_headers: 
    ##     auth: 
    ##   to_return: 
    ##   - status: 
    ##     body: 
    ##     response_headers: 
    ##     should_timeout: TRUE
    ##     should_raise: FALSE

``` r

x <- HttpClient$new(url = "https://httpbin.org")
x$post('post')
```

    ## Error:
    ## ! Request Timeout (HTTP 408).
    ##  - The client did not produce a request within the time that the server was prepared to wait. The client MAY repeat the request without modifications at any later time.

### Stubbing requests and set HTTP error expectation

``` r

library(fauxpas)
stub_request("get", "https://httpbin.org/get?a=b") %>% to_raise(HTTPBadRequest)
```

    ## <webmockr stub> 
    ##   method: get
    ##   uri: https://httpbin.org/get?a=b
    ##   with: 
    ##     query: 
    ##     body: 
    ##     request_headers: 
    ##     auth: 
    ##   to_return: 
    ##   - status: 
    ##     body: 
    ##     response_headers: 
    ##     should_timeout: FALSE
    ##     should_raise: HTTPBadRequest

``` r

x <- HttpClient$new(url = "https://httpbin.org")
x$get('get', query = list(a = "b"))
```

    ## Error:
    ## ! Bad Request (HTTP 400).
    ##  - The request could not be understood by the server due to malformed syntax. The client SHOULD NOT repeat the request without modifications.

## httr integration

``` r

library(webmockr)
library(httr)
```

    ## 
    ## Attaching package: 'httr'

    ## The following object is masked from 'package:crul':
    ## 
    ##     handle

``` r

# turn on httr mocking
httr_mock()
```

``` r

# no stub found
GET("https://httpbin.org/get")
#> Error: Real HTTP connections are disabled.
#> Unregistered request:
#>   GET https://httpbin.org/get   with headers {Accept: application/json, text/xml, application/xml, */*}
#>
#> You can stub this request with the following snippet:
#>
#>    stub_request('get', uri = 'https://httpbin.org/get') %>%
#>      wi_th(
#>        headers = list('Accept' = 'application/json, text/xml, application/xml, */*')
#>      )
#> ============================================================
```

make a stub

``` r

stub_request('get', uri = 'https://httpbin.org/get') %>%
  wi_th(
    headers = list(
      'Accept' = 'application/json, text/xml, application/xml, */*'
    )
  ) %>%
  to_return(
    status = 418,
    body = "I'm a teapot!!!",
    headers = list(im_a = "teapot")
  )
```

    ## <webmockr stub> 
    ##   method: get
    ##   uri: https://httpbin.org/get
    ##   with: 
    ##     query: 
    ##     body: 
    ##     request_headers: Accept=application/json, te...
    ##     auth: 
    ##   to_return: 
    ##   - status: 418
    ##     body: I'm a teapot!!!
    ##     response_headers: im_a=teapot
    ##     should_timeout: FALSE
    ##     should_raise: FALSE

now returns mocked response

``` r

(res <- GET("https://httpbin.org/get"))
res$status_code
#> [1] 418
res$headers
#> $im_a
#> [1] "teapot"
```

## httr2 integration

``` r

library(webmockr)
library(httr2)

# turn on httr2 mocking
enable()
```

``` r

# no stub found
req <- request("https://hb.opencpu.org/get")
req_perform(req)
#> Error: Real HTTP connections are disabled.
#> Unregistered request:
#>   GET https://hb.opencpu.org/get
#>
#> You can stub this request with the following snippet:
#>
#>    stub_request('get', uri = 'https://hb.opencpu.org/get')
#> ============================================================
```

make a stub

``` r

stub_request('get', uri = 'https://hb.opencpu.org/get') %>%
  to_return(
    status = 418,
    body = "I'm a teapot!!!",
    headers = list(im_a = "teapot")
  )
```

    ## <webmockr stub> 
    ##   method: get
    ##   uri: https://hb.opencpu.org/get
    ##   with: 
    ##     query: 
    ##     body: 
    ##     request_headers: 
    ##     auth: 
    ##   to_return: 
    ##   - status: 418
    ##     body: I'm a teapot!!!
    ##     response_headers: im_a=teapot
    ##     should_timeout: FALSE
    ##     should_raise: FALSE

now returns mocked response

``` r

req <- request("https://hb.opencpu.org/get")
res <- req_perform(req)
res
res$status_code
#> [1] 418
res$headers
#> <httr2_headers/list>
#> im_a: teapot
```

## Writing to disk

Write to a file before mocked request

``` r

## make a temp file
f <- tempfile(fileext = ".json")
## write something to the file
cat("{\"hello\":\"world\"}\n", file = f)
readLines(f)
```

    ## [1] "{\"hello\":\"world\"}"

``` r

## make the stub
invisible(
  stub_request("get", "https://httpbin.org/get") %>%
    to_return(body = file(f))
)
## make a request
out <- HttpClient$new("https://httpbin.org/get")$get(disk = f)
readLines(file(f))
```

    ## [1] "{\"hello\":\"world\"}"

OR - you can use
[`mock_file()`](https://docs.ropensci.org/webmockr/reference/mock_file.md)
to have `webmockr` handle file and contents

``` r

g <- tempfile(fileext = ".json")
## make the stub
invisible(
  stub_request("get", "https://httpbin.org/get") %>%
    to_return(body = mock_file(g, "{\"hello\":\"mars\"}\n"))
)
## make a request
out <- crul::HttpClient$new("https://httpbin.org/get")$get(disk = g)
readLines(out$content)
```

    ## [1] "{\"hello\":\"world\"}"

Writing to disk is supported in `crul`, `httr`, and `httr2`

## Many requests in a row

e.g., many redirects, then a final successful request

``` r

webmockr::enable()
library(crul)
library(fauxpas)

z <- stub_request("get", "https://httpbin.org/get")
to_return(z, status = 200, body = "foobar", headers = list(a = 5))
to_return(z, status = 200, body = "bears", headers = list(b = 6))
to_raise(z, HTTPBadRequest)
z

con <- crul::HttpClient$new(url = "https://httpbin.org")
# the first to_return()
first <- con$get("get")
first
first$parse("UTF-8")
# the second to_return()
second <- con$get("get")
second
second$parse("UTF-8")
# the third to_return() - fails as specified
third <- con$get("get")
```

Note that subsequent requests past the number of responses given with
[`to_return()`](https://docs.ropensci.org/webmockr/reference/to_return.md)/etc.
simply gives the last response you specified. Although if you set a
`to_timeout` or `to_raise` this feature won’t happen since you fail out.
