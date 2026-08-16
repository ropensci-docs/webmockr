# Get the last HTTP request made

Get the last HTTP request made

## Usage

``` r
last_request()
```

## Value

`NULL` if no requests registered; otherwise the last registered request
made as a `RequestSignature` class

## Examples

``` r
if (FALSE) { # interactive()
# no requests
request_registry_clear()
last_request()

# a request is found
enable()
stub_request("head", "https://nytimes.com")
library(crul)
crul::ok("https://nytimes.com")
last_request()

# cleanup
request_registry_clear()
stub_registry_clear()
}
```
