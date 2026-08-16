# webmockr: Stubbing and Setting Expectations on 'HTTP' Requests

Stubbing and setting expectations on 'HTTP' requests. Includes tools for
stubbing 'HTTP' requests, including expected request conditions and
response conditions. Match on 'HTTP' method, query parameters, request
body, headers and more. Can be used for unit tests or outside of a
testing context.

## Features

- Stubbing HTTP requests at low http client lib level

- Setting and verifying expectations on HTTP requests

- Matching requests based on method, URI, headers and body

- Supports multiple HTTP libraries, including crul, httr, and httr2

- Supports async http request mocking with crul only

## See also

Useful links:

- <https://github.com/ropensci/webmockr>

- <https://books.ropensci.org/http-testing/>

- <https://docs.ropensci.org/webmockr/>

- Report bugs at <https://github.com/ropensci/webmockr/issues>

## Author

**Maintainer**: Scott Chamberlain <myrmecocystus+r@gmail.com>
([ORCID](https://orcid.org/0000-0003-1444-9135))

Authors:

- Scott Chamberlain <myrmecocystus+r@gmail.com>
  ([ORCID](https://orcid.org/0000-0003-1444-9135))

Other contributors:

- Aaron Wolen ([ORCID](https://orcid.org/0000-0003-2542-2202))
  \[contributor\]

- rOpenSci ([ROR](https://ror.org/019jywm96)) \[funder\]

## Examples

``` r
library(webmockr)
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
stub_registry()
#> <webmockr stub registry> 
#>  Registered Stubs
#>   POST: https://httpbin.org/post    | to_return:    with status 200
#>   POST: https://httpbin.org/post    | to_return:   with body "stuff"
#>   POST: https://httpbin.org/post    | to_return:   with body {"a":{"b":"world"}}
#>   POST: https://httpbin.org/post    | to_return:     with headers {"a":5}
#>   POST: https://httpbin.org/post    | to_return:   with body "stuff"  with status 200  with headers {"a":5}
#>   POST: https://httpbin.org/post    | to_return:   with body {"foo":"bar"}
#>   POST: https://httpbin.org/post    | to_return:   with body "stuff"     | to_return:   with body "things"
#>   POST: https://httpbin.org/post    | to_return:   with body "stuff"     | to_return:   with body "stuff"     | to_return:   with body "stuff"
#>   GET: https://httpbin.org/get
#>   POST: https://httpbin.org/post
```
