# stub_registry_clear

Clear all stubs in the stub registry

## Usage

``` r
stub_registry_clear()
```

## Value

an empty list invisibly

## See also

Other stub-registry:
[`StubRegistry`](https://docs.ropensci.org/webmockr/reference/StubRegistry.md),
[`remove_request_stub()`](https://docs.ropensci.org/webmockr/reference/remove_request_stub.md),
[`stub_registry()`](https://docs.ropensci.org/webmockr/reference/stub_registry.md)

## Examples

``` r
(x <- stub_request("get", "https://httpbin.org/get"))
#> <webmockr stub> 
#>   method: get
#>   uri: https://httpbin.org/get
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 
stub_registry()
#> <webmockr stub registry> 
#>  Registered Stubs
#>   GET: https://httpbin.org/get
stub_registry_clear()
stub_registry()
#> <webmockr stub registry> 
#>  Registered Stubs
```
