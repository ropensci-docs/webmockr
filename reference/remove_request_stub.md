# Remove a request stub

Remove a request stub

## Usage

``` r
remove_request_stub(stub)
```

## Arguments

- stub:

  a request stub, of class `StubbedRequest`

## Value

logical, `TRUE` if removed, `FALSE` if not removed

## See also

Other stub-registry:
[`StubRegistry`](https://docs.ropensci.org/webmockr/reference/StubRegistry.md),
[`stub_registry()`](https://docs.ropensci.org/webmockr/reference/stub_registry.md),
[`stub_registry_clear()`](https://docs.ropensci.org/webmockr/reference/stub_registry_clear.md)

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
remove_request_stub(x)
stub_registry()
#> <webmockr stub registry> 
#>  Registered Stubs
```
