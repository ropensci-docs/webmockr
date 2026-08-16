# Partially match request query parameters or request bodies

For use inside
[`wi_th()`](https://docs.ropensci.org/webmockr/reference/wi_th.md)

## Usage

``` r
including(x)

excluding(x)
```

## Arguments

- x:

  (list) a list; may support other classes in the future

## Value

same as `x`, but with two attributes added:

- partial_match: always `TRUE`

- partial_type: the type of match, one of `include` or `exclude`

## Headers

Matching on headers already handles partial matching. That is,
`wi_th(headers = list(Fruit = "pear"))` matches any request that has any
request header that matches - the request can have other request
headers, but those don't matter as long as there is a match. These
helpers (`including`/`excluding`) are needed for query parameters and
bodies because by default matching must be exact for those.

## Examples

``` r
including(list(foo = "bar"))
#> <partial match>
#>   partial type: include
#>   length: 1
excluding(list(foo = "bar"))
#> <partial match>
#>   partial type: exclude
#>   length: 1

# get just keys by setting values as NULL
including(list(foo = NULL, bar = NULL))
#> <partial match>
#>   partial type: include
#>   length: 2

# in a stub
req <- stub_request("get", "https://httpbin.org/get")
req
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 

## query
wi_th(req, query = list(foo = "bar"))
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: foo=bar
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
wi_th(req, query = including(list(foo = "bar")))
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: including(foo=bar)
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
wi_th(req, query = excluding(list(foo = "bar")))
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: excluding(foo=bar)
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 

## body
wi_th(req, body = list(foo = "bar"))
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body (class: list): foo=bar
#>     request_headers: 
#>     auth: 
#>   to_return: 
wi_th(req, body = including(list(foo = "bar")))
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body (class: partial): including(foo=bar)
#>     request_headers: 
#>     auth: 
#>   to_return: 
wi_th(req, body = excluding(list(foo = "bar")))
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body (class: partial): excluding(foo=bar)
#>     request_headers: 
#>     auth: 
#>   to_return: 

# cleanup
stub_registry_clear()
```
