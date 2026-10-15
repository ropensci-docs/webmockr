# List or clear requests in the request registry

List or clear requests in the request registry

## Usage

``` r
request_registry()

request_registry_clear()
```

## Value

an object of class `RequestRegistry`, print method gives the requests in
the registry and the number of times each one has been performed

## Details

`request_registry()` lists the requests that have been made that
webmockr knows about; `request_registry_clear()` resets the request
registry (removes all recorded requests)

## See also

Other request-registry:
[`HashCounter`](https://docs.ropensci.org/webmockr/reference/HashCounter.md),
[`RequestRegistry`](https://docs.ropensci.org/webmockr/reference/RequestRegistry.md)

## Examples

``` r
webmockr::enable()
#> CrulAdapter enabled!
#> HttrAdapter enabled!
#> Httr2Adapter enabled!
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

# nothing in the request registry
request_registry()
#> <webmockr request registry> 
#>  Registered Requests

# make the request
z <- crul::HttpClient$new(url = "https://httpbin.org")$get("get")

# check the request registry - the request was made 1 time
request_registry()
#> <webmockr request registry> 
#>  Registered Requests
#>   GET:  https://httpbin.org/get   with headers {Accept-Encoding: gzip, deflate, Accept: application/json, text/xml, application/xml, */*} was made 1 times
#> 

# do the request again
z <- crul::HttpClient$new(url = "https://httpbin.org")$get("get")

# check the request registry - now it's been made 2 times, yay!
request_registry()
#> <webmockr request registry> 
#>  Registered Requests
#>   GET:  https://httpbin.org/get   with headers {Accept-Encoding: gzip, deflate, Accept: application/json, text/xml, application/xml, */*} was made 2 times
#> 

# clear the request registry
request_registry_clear()
webmockr::disable()
#> CrulAdapter disabled!
#> HttrAdapter disabled!
#> Httr2Adapter disabled!
```
