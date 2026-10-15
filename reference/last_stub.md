# Get the last stub created

Get the last stub created

## Usage

``` r
last_stub()
```

## Value

`NULL` if no stubs found; otherwise the last stub created as a
`StubbedRequest` class

## Examples

``` r
if (FALSE) { # interactive()
# no requests
stub_registry_clear()
last_stub()

# a stub is found
stub_request("head", "https://nytimes.com")
last_stub()

stub_request("post", "https://nytimes.com/stories")
last_stub()

# cleanup
stub_registry_clear()
}
```
