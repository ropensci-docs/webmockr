# Stub an http request

Stub an http request

## Usage

``` r
stub_request(method = "get", uri = NULL, uri_regex = NULL)
```

## Arguments

- method:

  (character) HTTP method, one of "get", "post", "put", "patch", "head",
  "delete", "options" - or the special "any" (for any method)

- uri:

  (character) The request uri. Can be a full or partial uri. webmockr
  can match uri's without the "http" scheme, but does not match if the
  scheme is "https". required, unless `uri_regex` given. See
  [UriPattern](https://docs.ropensci.org/webmockr/reference/UriPattern.md)
  for more. See the "uri vs. uri_regex" section

- uri_regex:

  (character) A URI represented as regex. required, if `uri` not given.
  See examples and the "uri vs. uri_regex" section

## Value

an object of class `StubbedRequest`, with print method describing the
stub.

## Details

Internally, this calls
[StubbedRequest](https://docs.ropensci.org/webmockr/reference/StubbedRequest.md)
which handles the logic

See
[`stub_registry()`](https://docs.ropensci.org/webmockr/reference/stub_registry.md)
for listing stubs,
[`stub_registry_clear()`](https://docs.ropensci.org/webmockr/reference/stub_registry_clear.md)
for removing all stubs and
[`remove_request_stub()`](https://docs.ropensci.org/webmockr/reference/remove_request_stub.md)
for removing specific stubs

If multiple stubs match the same request, we use the first stub. So if
you want to use a stub that was created after an earlier one that
matches, remove the earlier one(s).

Note on
[`wi_th()`](https://docs.ropensci.org/webmockr/reference/wi_th.md): If
you pass `query`, values are coerced to character class in the recorded
stub. You can pass numeric, integer, etc., but all will be coerced to
character.

See [`wi_th()`](https://docs.ropensci.org/webmockr/reference/wi_th.md)
for details on request body/query/headers and
[`to_return()`](https://docs.ropensci.org/webmockr/reference/to_return.md)
for details on how response status/body/headers are handled

## Note

Trailing slashes are dropped from stub URIs before matching

## uri vs. uri_regex

When you use `uri`, we compare the URIs without query params AND also
the query params themselves without the URIs.

When you use `uri_regex` we don't compare URIs and query params; we just
use your regex string defined in `uri_regex` as the pattern for a call
to [grepl](https://rdrr.io/r/base/grep.html)

## Mocking writing to disk

See
[mocking-disk-writing](https://docs.ropensci.org/webmockr/reference/mocking-disk-writing.md)

## Error handling

To construct stubs, one uses `stub_request()` first - which registers
the stub in the stub registry. Any additional calls to modify the stub
with for example
[`wi_th()`](https://docs.ropensci.org/webmockr/reference/wi_th.md) or
[`to_return()`](https://docs.ropensci.org/webmockr/reference/to_return.md)
can error. In those error cases we ideally want to remove (unregister)
the stub because you certainly don't want a registered stub that is not
exactly what you intended.

When you encounter an error creating a stub you should see a warning
message that the stub has been removed, for example:

    stub_request("get", "https://httpbin.org/get") %>%
      wi_th(query = mtcars)
    #> Error in `wi_th()`:
    #> ! z$query must be of class list or partial
    #> Run `rlang::last_trace()` to see where the error occurred.
    #> Warning message:
    #> Encountered an error constructing stub
    #> • Removed stub
    #> • To see a list of stubs run stub_registry()

## See also

[`wi_th()`](https://docs.ropensci.org/webmockr/reference/wi_th.md),
[`to_return()`](https://docs.ropensci.org/webmockr/reference/to_return.md),
[`to_timeout()`](https://docs.ropensci.org/webmockr/reference/to_timeout.md),
[`to_raise()`](https://docs.ropensci.org/webmockr/reference/to_raise.md),
[`mock_file()`](https://docs.ropensci.org/webmockr/reference/mock_file.md)

## Examples

``` r
# basic stubbing
stub_request("get", "https://httpbin.org/get")
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
stub_request("post", "https://httpbin.org/post")
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 

# any method, use "any"
stub_request("any", "https://httpbin.org/get")
#> <webmockr stub> 
#>   method: any
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 

# list stubs
stub_registry()
#> <webmockr stub registry> 
#>  Registered Stubs
#>   GET: https://httpbin.org/get
#>   POST: https://httpbin.org/post
#>   ANY: https://httpbin.org/get

# request headers
stub_request("get", "https://httpbin.org/get") %>%
  wi_th(headers = list("User-Agent" = "R"))
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: User-Agent=R
#>     auth: 
#>   to_return: 

# request body
stub_request("post", "https://httpbin.org/post") %>%
  wi_th(body = list(foo = "bar"))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body (class: list): foo=bar
#>     request_headers: 
#>     auth: 
#>   to_return: 
stub_registry()
#> <webmockr stub registry> 
#>  Registered Stubs
#>   POST: https://httpbin.org/post   with body {"foo":"bar"}
library(crul)
#> Warning: package ‘crul’ was built under R version 4.6.1
#> 
#> Attaching package: ‘crul’
#> The following object is masked from ‘package:httr’:
#> 
#>     handle
x <- crul::HttpClient$new(url = "https://httpbin.org")
enable(adapter = "crul")
#> CrulAdapter enabled!
x$post("post", body = list(foo = "bar"))
#> <crul response> 
#>   url: https://httpbin.org/post
#>   request_headers: 
#>     User-Agent: libcurl/8.5.0 r-curl/7.1.0 crul/1.6.0.9000
#>     Accept-Encoding: gzip, deflate
#>     Accept: application/json, text/xml, application/xml, */*
#>   response_headers: 
#>   status: 200

# add expectation with to_return
stub_request("get", "https://httpbin.org/get") %>%
  wi_th(
    query = list(hello = "world"),
    headers = list("User-Agent" = "R")
  ) %>%
  to_return(status = 200, body = "stuff", headers = list(a = 5))
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: hello=world
#>     body: 
#>     request_headers: User-Agent=R
#>     auth: 
#>   to_return: 
#>   - status: 200
#>     body: stuff
#>     response_headers: a=5
#>     should_timeout: FALSE
#>     should_raise: FALSE

# list stubs again
stub_registry()
#> <webmockr stub registry> 
#>  Registered Stubs
#>   POST: https://httpbin.org/post   with body {"foo":"bar"}
#>   GET: https://httpbin.org/get  with query params hello=world   with headers {"User-Agent":"R"} | to_return:   with body "stuff"  with status 200  with headers {"a":5}

# regex
stub_request("get", uri_regex = ".+ample\\..")
#> <webmockr stub> 
#>   method: get
#>   uri: .+ample\..
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 

# set stub an expectation to timeout
stub_request("get", "https://httpbin.org/get") %>% to_timeout()
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: 
#>     response_headers: 
#>     should_timeout: TRUE
#>     should_raise: FALSE
x <- crul::HttpClient$new(url = "https://httpbin.org")
try(x$get("get"))
#> Error : Request Timeout (HTTP 408).
#>  - The client did not produce a request within the time that the server was prepared to wait. The client MAY repeat the request without modifications at any later time.

# raise exception
library(fauxpas)
stub_request("get", "https://httpbin.org/get") %>% to_raise(HTTPAccepted)
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: 
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: HTTPAccepted
stub_request("get", "https://httpbin.org/get") %>%
  to_raise(HTTPAccepted, HTTPGone)
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: 
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: HTTPAccepted, HTTPGone

x <- crul::HttpClient$new(url = "https://httpbin.org")
stub_request("get", "https://httpbin.org/get") %>% to_raise(HTTPBadGateway)
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: 
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: HTTPBadGateway
enable(adapter = "crul")
#> CrulAdapter enabled!
try(x$get("get"))
#> Error : Accepted (HTTP 202).
#>  - The request has been accepted for processing, but the processing has not been completed.  The request might or might not eventually be acted upon, as it might be disallowed when processing actually takes place. There is no facility for re-sending a status code from an asynchronous operation such as this.
#> The 202 response is intentionally non-committal. Its purpose is to allow a server to accept a request for some other process (perhaps a batch-oriented process that is only run once per day) without requiring that the user agent's connection to the server persist until the process is completed. The entity returned with this response SHOULD include an indication of the request's current status and either a pointer to a status monitor or some estimate of when the user can expect the request to be fulfilled.

# pass a list to .list
z <- stub_request("get", "https://httpbin.org/get")
wi_th(z, .list = list(query = list(foo = "bar")))
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: foo=bar
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 

# just body
stub_request("any", uri_regex = ".+") %>%
  wi_th(body = list(foo = "bar"))
#> <webmockr stub> 
#>   method: any
#>   uri: .+
#>   with: 
#>     query: 
#>     body (class: list): foo=bar
#>     request_headers: 
#>     auth: 
#>   to_return: 
## with crul
library(crul)
x <- crul::HttpClient$new(url = "https://httpbin.org")
enable(adapter = "crul")
#> CrulAdapter enabled!
x$post("post", body = list(foo = "bar"))
#> <crul response> 
#>   url: https://httpbin.org/post
#>   request_headers: 
#>     User-Agent: libcurl/8.5.0 r-curl/7.1.0 crul/1.6.0.9000
#>     Accept-Encoding: gzip, deflate
#>     Accept: application/json, text/xml, application/xml, */*
#>   response_headers: 
#>   status: 200
x$put("put", body = list(foo = "bar"))
#> <crul response> 
#>   url: https://httpbin.org/put
#>   request_headers: 
#>     User-Agent: libcurl/8.5.0 r-curl/7.1.0 crul/1.6.0.9000
#>     Accept-Encoding: gzip, deflate
#>     Accept: application/json, text/xml, application/xml, */*
#>   response_headers: 
#>   status: 200
## with httr
library(httr)
httr_mock()
POST("https://example.com", body = list(foo = "bar"))
#> Response [https://example.com]
#>   Date: 2026-08-16 15:59
#>   Status: 200
#>   Content-Type: <unknown>
#> <EMPTY BODY>
PUT("https://google.com", body = list(foo = "bar"))
#> Response [https://google.com]
#>   Date: 2026-08-16 15:59
#>   Status: 200
#>   Content-Type: <unknown>
#> <EMPTY BODY>

# just headers
headers <- list(
  "Accept-Encoding" = "gzip, deflate",
  "Accept" = "application/json, text/xml, application/xml, */*"
)
stub_request("any", uri_regex = ".+") %>% wi_th(headers = headers)
#> <webmockr stub> 
#>   method: any
#>   uri: .+
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: Accept-Encoding=gzip, deflate, Accept=application/json, te...
#>     auth: 
#>   to_return: 
library(crul)
x <- crul::HttpClient$new(url = "https://httpbin.org", headers = headers)
enable(adapter = "crul")
#> CrulAdapter enabled!
x$post("post")
#> <crul response> 
#>   url: https://httpbin.org/post
#>   request_headers: 
#>     User-Agent: libcurl/8.5.0 r-curl/7.1.0 crul/1.6.0.9000
#>     Accept-Encoding: gzip, deflate
#>     Accept: application/json, text/xml, application/xml, */*
#>   response_headers: 
#>   status: 200
x$put("put", body = list(foo = "bar"))
#> <crul response> 
#>   url: https://httpbin.org/put
#>   request_headers: 
#>     User-Agent: libcurl/8.5.0 r-curl/7.1.0 crul/1.6.0.9000
#>     Accept-Encoding: gzip, deflate
#>     Accept: application/json, text/xml, application/xml, */*
#>   response_headers: 
#>   status: 200

# many responses
## the first response matches the first to_return call, and so on
stub_request("get", "https://httpbin.org/get") %>%
  to_return(status = 200, body = "foobar", headers = list(a = 5)) %>%
  to_return(status = 200, body = "bears", headers = list(b = 6))
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 200
#>     body: foobar
#>     response_headers: a=5
#>     should_timeout: FALSE
#>     should_raise: FALSE
#>   - status: 200
#>     body: bears
#>     response_headers: b=6
#>     should_timeout: FALSE
#>     should_raise: FALSE
con <- crul::HttpClient$new(url = "https://httpbin.org")
con$get("get")$parse("UTF-8")
#> [1] ""
con$get("get")$parse("UTF-8")
#> [1] ""

## OR, use times with to_return() to repeat the same response many times
library(fauxpas)
stub_request("get", "https://httpbin.org/get") %>%
  to_return(status = 200, body = "apple-pie", times = 2) %>%
  to_raise(HTTPUnauthorized)
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 200
#>     body: apple-pie
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
#>   - status: 200
#>     body: apple-pie
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
#>   - status: 
#>     body: 
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: HTTPUnauthorized
con <- crul::HttpClient$new(url = "https://httpbin.org")
con$get("get")$parse("UTF-8")
#> [1] "apple-pie"
con$get("get")$parse("UTF-8")
#> [1] "apple-pie"
try(con$get("get")$parse("UTF-8"))
#> Error : Unauthorized (HTTP 401).
#>  - The request requires user authentication. The response MUST include a WWW-Authenticate header field (section 14.47) containing a challenge applicable to the requested resource. The client MAY repeat the request with a suitable Authorization header field (section 14.8). If the request already included Authorization credentials, then the 401 response indicates that authorization has been refused for those credentials. If the 401 response contains the same challenge as the prior response, and the user agent has already attempted authentication at least once, then the user SHOULD be presented the entity that was given in the response, since that entity might include relevant diagnostic information. HTTP access authentication is explained in HTTP Authentication: Basic and Digest Access Authentication [43].

# partial matching
## query parameters
library(httr)
enable(adapter = "httr")
#> HttrAdapter enabled!
### matches
stub_request("get", "https://hb.opencpu.org/get") %>%
  wi_th(query = including(list(fruit = "pear"))) %>%
  to_return(body = "matched on partial query!")
#> <webmockr stub> 
#>   method: get
#>   uri: https://hb.opencpu.org/get
#>   with: 
#>     query: including(fruit=pear)
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: matched on partial query!
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
resp <- GET("https://hb.opencpu.org/get",
  query = list(fruit = "pear", bread = "scone")
)
rawToChar(content(resp))
#> [1] "matched on partial query!"
### doesn't match
stub_registry_clear()
stub_request("get", "https://hb.opencpu.org/get") %>%
  wi_th(query = list(fruit = "pear")) %>%
  to_return(body = "didn't match, ugh!")
#> <webmockr stub> 
#>   method: get
#>   uri: https://hb.opencpu.org/get
#>   with: 
#>     query: fruit=pear
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: didn't match, ugh!
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
try({
  GET("https://hb.opencpu.org/get",
    query = list(fruit = "pear", meat = "chicken"))
})
#> Error in webmockr::HttrAdapter$new()$handle_request(req) : 
#>   Real HTTP connections are disabled.
#> ! Unregistered request:
#> ℹ GET:  https://hb.opencpu.org/get?fruit=pear&meat=chicken   with headers {Accept: application/json, text/xml, application/xml, */*}
#> 
#> You can stub this request with the following snippet:
#>  stub_request('get', uri = 'https://hb.opencpu.org/get?fruit=pear&meat=chicken') %>%
#>      wi_th(
#>        headers = list('Accept' = 'application/json, text/xml, application/xml, */*')
#>      )
#> 
#> registered request stubs:
#>  GET: https://hb.opencpu.org/get  with query params fruit=pear   | to_return:   with body "didn't match, ugh!"
#> 
#> 
#> ============================================================

## request body
### matches - including
stub_request("post", "https://hb.opencpu.org/post") %>%
  wi_th(body = including(list(fruit = "pear"))) %>%
  to_return(body = "matched on partial body!")
#> <webmockr stub> 
#>   method: post
#>   uri: https://hb.opencpu.org/post
#>   with: 
#>     query: 
#>     body (class: partial): including(fruit=pear)
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: matched on partial body!
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
resp <- POST("https://hb.opencpu.org/post",
  body = list(fruit = "pear", meat = "chicken")
)
rawToChar(content(resp))
#> [1] "matched on partial body!"
### matches - excluding
stub_request("post", "https://hb.opencpu.org/post") %>%
  wi_th(body = excluding(list(fruit = "pear"))) %>%
  to_return(body = "matched on partial body!")
#> <webmockr stub> 
#>   method: post
#>   uri: https://hb.opencpu.org/post
#>   with: 
#>     query: 
#>     body (class: partial): excluding(fruit=pear)
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 
#>     body: matched on partial body!
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE
res <- POST("https://hb.opencpu.org/post",
  body = list(color = "blue")
)
rawToChar(content(res))
#> [1] "matched on partial body!"
POST("https://hb.opencpu.org/post",
  body = list(fruit = "pear", meat = "chicken"))
#> Response [https://hb.opencpu.org/post]
#>   Date: 2026-08-16 15:59
#>   Status: 200
#>   Content-Type: <unknown>
#>   Size: 24 B
#> <BINARY BODY>

# clear all stubs
stub_registry()
#> <webmockr stub registry> 
#>  Registered Stubs
#>   POST: https://hb.opencpu.org/post   with body {"fruit":"pear"}  | to_return:   with body "matched on partial body!"
#>   POST: https://hb.opencpu.org/post   with body {"fruit":"pear"}  | to_return:   with body "matched on partial body!"
stub_registry_clear()
```
