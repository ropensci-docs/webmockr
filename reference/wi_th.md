# Set additional parts of a stubbed request

Set query params, request body, request headers and/or basic_auth

## Usage

``` r
wi_th(.data, ..., .list = list())
```

## Arguments

- .data:

  input. Anything that can be coerced to a `StubbedRequest` class object

- ...:

  Comma separated list of named variables. accepts the following:
  `query`, `body`, `headers`, `basic_auth`. See Details.

- .list:

  named list, has to be one of `query`, `body`, `headers` and/or
  `basic_auth`. An alternative to passing in via `...`. Don't pass the
  same thing to both, e.g. don't pass 'query' to `...`, and also 'query'
  to this parameter

## Value

an object of class `StubbedRequest`, with print method describing the
stub

## Details

`with` is a function in the `base` package, so we went with `wi_th`

Values for query, body, headers, and basic_auth:

- query: (list) a named list. values are coerced to character class in
  the recorded stub. You can pass numeric, integer, etc., but all will
  be coerced to character.

- body: various, including character string, list, raw, numeric, upload
  ([`crul::upload()`](https://docs.ropensci.org/crul/reference/upload.html),
  [`httr::upload_file()`](https://httr.r-lib.org/reference/upload_file.html),
  [`curl::form_file()`](https://jeroen.r-universe.dev/curl/reference/multipart.html),
  or
  [`curl::form_data()`](https://jeroen.r-universe.dev/curl/reference/multipart.html)
  they both create the same object in the end). for the special case of
  an empty request body use `NA` instead of `NULL` because with `NULL`
  we can't determine if the user did not supply a body or they supplied
  `NULL` to indicate an empty body.

- headers: (list) a named list

- basic_auth: (character) a length two vector, username and password. We
  don't do any checking of the username/password except to detect edge
  cases where for example, the username/password were probably not set
  by the user on purpose (e.g., a URL is picked up by an environment
  variable). Only basic authentication supported
  <https://en.wikipedia.org/wiki/Basic_access_authentication>.

Note that there is no regex matching on query, body, or headers. They
are tested for matches in the following ways:

- query: compare stubs and requests with
  [`identical()`](https://rdrr.io/r/base/identical.html). this compares
  named lists, so both list names and values are compared

- body: varies depending on the body format (list vs. character, etc.)

- headers: compare stub and request values with `==`. list names are
  compared with `%in%`. `basic_auth` is included in headers (with the
  name Authorization)

## Note

see more examples in
[`stub_request()`](https://docs.ropensci.org/webmockr/reference/stub_request.md)

## See also

[`including()`](https://docs.ropensci.org/webmockr/reference/including.md)

## Examples

``` r
# first, make a stub object
req <- stub_request("post", "https://httpbin.org/post")

# add body
# list
wi_th(req, body = list(foo = "bar"))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body (class: list): foo=bar
#>     request_headers: 
#>     auth: 
#>   to_return: 
# string
wi_th(req, body = '{"foo": "bar"}')
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body (class: character): {"foo": "bar"}
#>     request_headers: 
#>     auth: 
#>   to_return: 
# raw
wi_th(req, body = charToRaw('{"foo": "bar"}'))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body (class: raw): raw bytes, length: 14
#>     request_headers: 
#>     auth: 
#>   to_return: 
# numeric
wi_th(req, body = 5)
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body (class: numeric): 5
#>     request_headers: 
#>     auth: 
#>   to_return: 
# an upload
wi_th(req, body = crul::upload(system.file("CITATION")))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body (class: form_file): crul::upload("/usr/lib/R/library/base/CITATION", type="text/plain")
#>     request_headers: 
#>     auth: 
#>   to_return: 
# wi_th(req, body = httr::upload_file(system.file("CITATION")))

# add query - has to be a named list
wi_th(req, query = list(foo = "bar"))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: foo=bar
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 

# add headers - has to be a named list
wi_th(req, headers = list(foo = "bar"))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: foo=bar
#>     auth: 
#>   to_return: 
wi_th(req, headers = list(`User-Agent` = "webmockr/v1", hello = "world"))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: User-Agent=webmockr/v1, hello=world
#>     auth: 
#>   to_return: 

# .list - pass in a named list instead
wi_th(req, .list = list(body = list(foo = "bar")))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body (class: list): foo=bar
#>     request_headers: 
#>     auth: 
#>   to_return: 

# basic authentication
wi_th(req, basic_auth = c("user", "pass"))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: Basic dXNlcjpwYXNz
#>   to_return: 
wi_th(req, basic_auth = c("user", "pass"), headers = list(foo = "bar"))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: foo=bar
#>     auth: Basic dXNlcjpwYXNz
#>   to_return: 

# partial matching, query params
## including
wi_th(req, query = including(list(foo = "bar")))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: including(foo=bar)
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
## excluding
wi_th(req, query = excluding(list(foo = "bar")))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: excluding(foo=bar)
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 

# partial matching, body
## including
wi_th(req, body = including(list(foo = "bar")))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body (class: partial): including(foo=bar)
#>     request_headers: 
#>     auth: 
#>   to_return: 
## excluding
wi_th(req, body = excluding(list(foo = "bar")))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body (class: partial): excluding(foo=bar)
#>     request_headers: 
#>     auth: 
#>   to_return: 

# basic auth
## including
wi_th(req, body = including(list(foo = "bar")))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body (class: partial): including(foo=bar)
#>     request_headers: 
#>     auth: 
#>   to_return: 
## excluding
wi_th(req, body = excluding(list(foo = "bar")))
#> <webmockr stub> 
#>   method: post
#>   uri: https://httpbin.org/post
#>   with: 
#>     query: 
#>     body (class: partial): excluding(foo=bar)
#>     request_headers: 
#>     auth: 
#>   to_return: 
```
