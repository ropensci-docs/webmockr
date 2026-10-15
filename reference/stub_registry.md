# List stubs in the stub registry

List stubs in the stub registry

## Usage

``` r
stub_registry()
```

## Value

an object of class `StubRegistry`, print method gives the stubs in the
registry

## See also

Other stub-registry:
[`StubRegistry`](https://docs.ropensci.org/webmockr/reference/StubRegistry.md),
[`remove_request_stub()`](https://docs.ropensci.org/webmockr/reference/remove_request_stub.md),
[`stub_registry_clear()`](https://docs.ropensci.org/webmockr/reference/stub_registry_clear.md)

## Examples

``` r
# make a stub
stub_request("get", "https://httpbin.org/get") %>%
  to_return(body = "success!", status = 200)
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
#>     body: success!
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE

# check the stub registry, there should be one in there
stub_registry()
#> <webmockr stub registry> 
#>  Registered Stubs
#>   GET: https://httpbin.org/get    | to_return:   with body "success!"  with status 200

# make another stub
stub_request("get", "https://httpbin.org/get") %>%
  to_return(body = "woopsy", status = 404)
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
#>   - status: 404
#>     body: woopsy
#>     response_headers: 
#>     should_timeout: FALSE
#>     should_raise: FALSE

# check the stub registry, now there are two there
stub_registry()
#> <webmockr stub registry> 
#>  Registered Stubs
#>   GET: https://httpbin.org/get    | to_return:   with body "success!"  with status 200
#>   GET: https://httpbin.org/get    | to_return:   with body "woopsy"  with status 404

# to clear the stub registry
stub_registry_clear()
```
