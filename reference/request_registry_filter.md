# Request registry filter

If no filters are given, returns all requests

## Usage

``` r
request_registry_filter(method = NULL, url = NULL, body = NULL, headers = NULL)
```

## Arguments

- method:

  (character) http method. default: `NULL`

- url:

  (character) a url. default: `NULL`

- body:

  (various) a request body. default: `NULL`. Can be any of: `character`,
  `json`, `list`, `raw`, `numeric`, `NULL`, `FALSE`

- headers:

  (list) if given, must be a named list. default: `NULL`

## Value

list, length of number of unique requests recorded, or those requests
matching filters supplied by parameters

## Examples

``` r
enable(adapter="httr")
#> HttrAdapter enabled!

stub_request("any", uri_regex = ".+")
#> <webmockr stub> 
#>   method: any
#>   uri: .+
#>   with: 
#>     query: 
#>     body: 
#>     request_headers: 
#>     auth: 
#>   to_return: 

library(httr)
GET("http://example.com")
#> Response [http://example.com]
#>   Date: 2026-08-16 15:59
#>   Status: 200
#>   Content-Type: <unknown>
#> <EMPTY BODY>
GET("https://hb.cran.dev/get")
#> Response [https://hb.cran.dev/get]
#>   Date: 2026-08-16 15:59
#>   Status: 200
#>   Content-Type: <unknown>
#> <EMPTY BODY>
POST("https://hb.cran.dev/post", body = list(fruit = "apple"))
#> Response [https://hb.cran.dev/post]
#>   Date: 2026-08-16 15:59
#>   Status: 200
#>   Content-Type: <unknown>
#> <EMPTY BODY>
POST("https://hb.cran.dev/post", body = list(cheese = "swiss"))
#> Response [https://hb.cran.dev/post]
#>   Date: 2026-08-16 15:59
#>   Status: 200
#>   Content-Type: <unknown>
#> <EMPTY BODY>
GET("https://hb.cran.dev/get", add_headers(Accept = "application/json"))
#> Response [https://hb.cran.dev/get]
#>   Date: 2026-08-16 15:59
#>   Status: 200
#>   Content-Type: <unknown>
#> <EMPTY BODY>

request_registry_filter()
#> [[1]]
#> [[1]]$key
#> [1] "GET:  http://example.com   with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$count
#> [1] 1
#> 
#> [[1]]$method
#> [1] "get"
#> 
#> [[1]]$uri
#> [1] "http://example.com"
#> 
#> [[1]]$body
#> [1] NA
#> 
#> [[1]]$headers
#> [[1]]$headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
#> [[1]]$proxies
#> [1] NA
#> 
#> [[1]]$auth
#> [1] NA
#> 
#> [[1]]$url
#> [[1]]$url$url
#> [1] "http://example.com"
#> 
#> 
#> [[1]]$disk
#> [1] NA
#> 
#> [[1]]$fields
#> [1] NA
#> 
#> [[1]]$output
#> [1] NA
#> 
#> [[1]]$key
#> [1] "GET:  http://example.com   with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$request
#> <RequestSignature> 
#>   method: GET
#>   uri: http://example.com
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#> 
#> [[1]]$count
#> [1] 1
#> 
#> 
#> [[2]]
#> [[2]]$key
#> [1] "GET:  https://hb.cran.dev/get   with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[2]]$count
#> [1] 1
#> 
#> [[2]]$method
#> [1] "get"
#> 
#> [[2]]$uri
#> [1] "https://hb.cran.dev/get"
#> 
#> [[2]]$body
#> [1] NA
#> 
#> [[2]]$headers
#> [[2]]$headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
#> [[2]]$proxies
#> [1] NA
#> 
#> [[2]]$auth
#> [1] NA
#> 
#> [[2]]$url
#> [[2]]$url$url
#> [1] "https://hb.cran.dev/get"
#> 
#> 
#> [[2]]$disk
#> [1] NA
#> 
#> [[2]]$fields
#> [1] NA
#> 
#> [[2]]$output
#> [1] NA
#> 
#> [[2]]$key
#> [1] "GET:  https://hb.cran.dev/get   with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[2]]$request
#> <RequestSignature> 
#>   method: GET
#>   uri: https://hb.cran.dev/get
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#> 
#> [[2]]$count
#> [1] 1
#> 
#> 
#> [[3]]
#> [[3]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {fruit: apple}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[3]]$count
#> [1] 1
#> 
#> [[3]]$method
#> [1] "post"
#> 
#> [[3]]$uri
#> [1] "https://hb.cran.dev/post"
#> 
#> [[3]]$body
#> [[3]]$body$fruit
#> [1] "apple"
#> 
#> 
#> [[3]]$headers
#> [[3]]$headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
#> [[3]]$proxies
#> [1] NA
#> 
#> [[3]]$auth
#> [1] NA
#> 
#> [[3]]$url
#> [[3]]$url$url
#> [1] "https://hb.cran.dev/post"
#> 
#> 
#> [[3]]$disk
#> [1] NA
#> 
#> [[3]]$fields
#> [[3]]$fields$fruit
#> [1] "apple"
#> 
#> 
#> [[3]]$output
#> [1] NA
#> 
#> [[3]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {fruit: apple}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[3]]$request
#> <RequestSignature> 
#>   method: POST
#>   uri: https://hb.cran.dev/post
#>   body: 
#>      fruit: apple
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#>   fields: 
#>      fruit: apple
#> 
#> [[3]]$count
#> [1] 1
#> 
#> 
#> [[4]]
#> [[4]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {cheese: swiss}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[4]]$count
#> [1] 1
#> 
#> [[4]]$method
#> [1] "post"
#> 
#> [[4]]$uri
#> [1] "https://hb.cran.dev/post"
#> 
#> [[4]]$body
#> [[4]]$body$cheese
#> [1] "swiss"
#> 
#> 
#> [[4]]$headers
#> [[4]]$headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
#> [[4]]$proxies
#> [1] NA
#> 
#> [[4]]$auth
#> [1] NA
#> 
#> [[4]]$url
#> [[4]]$url$url
#> [1] "https://hb.cran.dev/post"
#> 
#> 
#> [[4]]$disk
#> [1] NA
#> 
#> [[4]]$fields
#> [[4]]$fields$cheese
#> [1] "swiss"
#> 
#> 
#> [[4]]$output
#> [1] NA
#> 
#> [[4]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {cheese: swiss}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[4]]$request
#> <RequestSignature> 
#>   method: POST
#>   uri: https://hb.cran.dev/post
#>   body: 
#>      cheese: swiss
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#>   fields: 
#>      cheese: swiss
#> 
#> [[4]]$count
#> [1] 1
#> 
#> 
#> [[5]]
#> [[5]]$key
#> [1] "GET:  https://hb.cran.dev/get   with headers {Accept: application/json}"
#> 
#> [[5]]$count
#> [1] 1
#> 
#> [[5]]$method
#> [1] "get"
#> 
#> [[5]]$uri
#> [1] "https://hb.cran.dev/get"
#> 
#> [[5]]$body
#> [1] NA
#> 
#> [[5]]$headers
#> [[5]]$headers$Accept
#> [1] "application/json"
#> 
#> 
#> [[5]]$proxies
#> [1] NA
#> 
#> [[5]]$auth
#> [1] NA
#> 
#> [[5]]$url
#> [[5]]$url$url
#> [1] "https://hb.cran.dev/get"
#> 
#> 
#> [[5]]$disk
#> [1] NA
#> 
#> [[5]]$fields
#> [1] NA
#> 
#> [[5]]$output
#> [1] NA
#> 
#> [[5]]$key
#> [1] "GET:  https://hb.cran.dev/get   with headers {Accept: application/json}"
#> 
#> [[5]]$request
#> <RequestSignature> 
#>   method: GET
#>   uri: https://hb.cran.dev/get
#>   headers: 
#>      Accept: application/json
#> 
#> [[5]]$count
#> [1] 1
#> 
#> 
request_registry_filter(method="get")
#> [[1]]
#> [[1]]$key
#> [1] "GET:  http://example.com   with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$count
#> [1] 1
#> 
#> [[1]]$method
#> [1] "get"
#> 
#> [[1]]$uri
#> [1] "http://example.com"
#> 
#> [[1]]$body
#> [1] NA
#> 
#> [[1]]$headers
#> [[1]]$headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
#> [[1]]$proxies
#> [1] NA
#> 
#> [[1]]$auth
#> [1] NA
#> 
#> [[1]]$url
#> [[1]]$url$url
#> [1] "http://example.com"
#> 
#> 
#> [[1]]$disk
#> [1] NA
#> 
#> [[1]]$fields
#> [1] NA
#> 
#> [[1]]$output
#> [1] NA
#> 
#> [[1]]$key
#> [1] "GET:  http://example.com   with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$request
#> <RequestSignature> 
#>   method: GET
#>   uri: http://example.com
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#> 
#> [[1]]$count
#> [1] 1
#> 
#> 
#> [[2]]
#> [[2]]$key
#> [1] "GET:  https://hb.cran.dev/get   with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[2]]$count
#> [1] 1
#> 
#> [[2]]$method
#> [1] "get"
#> 
#> [[2]]$uri
#> [1] "https://hb.cran.dev/get"
#> 
#> [[2]]$body
#> [1] NA
#> 
#> [[2]]$headers
#> [[2]]$headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
#> [[2]]$proxies
#> [1] NA
#> 
#> [[2]]$auth
#> [1] NA
#> 
#> [[2]]$url
#> [[2]]$url$url
#> [1] "https://hb.cran.dev/get"
#> 
#> 
#> [[2]]$disk
#> [1] NA
#> 
#> [[2]]$fields
#> [1] NA
#> 
#> [[2]]$output
#> [1] NA
#> 
#> [[2]]$key
#> [1] "GET:  https://hb.cran.dev/get   with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[2]]$request
#> <RequestSignature> 
#>   method: GET
#>   uri: https://hb.cran.dev/get
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#> 
#> [[2]]$count
#> [1] 1
#> 
#> 
#> [[3]]
#> [[3]]$key
#> [1] "GET:  https://hb.cran.dev/get   with headers {Accept: application/json}"
#> 
#> [[3]]$count
#> [1] 1
#> 
#> [[3]]$method
#> [1] "get"
#> 
#> [[3]]$uri
#> [1] "https://hb.cran.dev/get"
#> 
#> [[3]]$body
#> [1] NA
#> 
#> [[3]]$headers
#> [[3]]$headers$Accept
#> [1] "application/json"
#> 
#> 
#> [[3]]$proxies
#> [1] NA
#> 
#> [[3]]$auth
#> [1] NA
#> 
#> [[3]]$url
#> [[3]]$url$url
#> [1] "https://hb.cran.dev/get"
#> 
#> 
#> [[3]]$disk
#> [1] NA
#> 
#> [[3]]$fields
#> [1] NA
#> 
#> [[3]]$output
#> [1] NA
#> 
#> [[3]]$key
#> [1] "GET:  https://hb.cran.dev/get   with headers {Accept: application/json}"
#> 
#> [[3]]$request
#> <RequestSignature> 
#>   method: GET
#>   uri: https://hb.cran.dev/get
#>   headers: 
#>      Accept: application/json
#> 
#> [[3]]$count
#> [1] 1
#> 
#> 
request_registry_filter(method="post")
#> [[1]]
#> [[1]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {fruit: apple}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$count
#> [1] 1
#> 
#> [[1]]$method
#> [1] "post"
#> 
#> [[1]]$uri
#> [1] "https://hb.cran.dev/post"
#> 
#> [[1]]$body
#> [[1]]$body$fruit
#> [1] "apple"
#> 
#> 
#> [[1]]$headers
#> [[1]]$headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
#> [[1]]$proxies
#> [1] NA
#> 
#> [[1]]$auth
#> [1] NA
#> 
#> [[1]]$url
#> [[1]]$url$url
#> [1] "https://hb.cran.dev/post"
#> 
#> 
#> [[1]]$disk
#> [1] NA
#> 
#> [[1]]$fields
#> [[1]]$fields$fruit
#> [1] "apple"
#> 
#> 
#> [[1]]$output
#> [1] NA
#> 
#> [[1]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {fruit: apple}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$request
#> <RequestSignature> 
#>   method: POST
#>   uri: https://hb.cran.dev/post
#>   body: 
#>      fruit: apple
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#>   fields: 
#>      fruit: apple
#> 
#> [[1]]$count
#> [1] 1
#> 
#> 
#> [[2]]
#> [[2]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {cheese: swiss}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[2]]$count
#> [1] 1
#> 
#> [[2]]$method
#> [1] "post"
#> 
#> [[2]]$uri
#> [1] "https://hb.cran.dev/post"
#> 
#> [[2]]$body
#> [[2]]$body$cheese
#> [1] "swiss"
#> 
#> 
#> [[2]]$headers
#> [[2]]$headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
#> [[2]]$proxies
#> [1] NA
#> 
#> [[2]]$auth
#> [1] NA
#> 
#> [[2]]$url
#> [[2]]$url$url
#> [1] "https://hb.cran.dev/post"
#> 
#> 
#> [[2]]$disk
#> [1] NA
#> 
#> [[2]]$fields
#> [[2]]$fields$cheese
#> [1] "swiss"
#> 
#> 
#> [[2]]$output
#> [1] NA
#> 
#> [[2]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {cheese: swiss}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[2]]$request
#> <RequestSignature> 
#>   method: POST
#>   uri: https://hb.cran.dev/post
#>   body: 
#>      cheese: swiss
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#>   fields: 
#>      cheese: swiss
#> 
#> [[2]]$count
#> [1] 1
#> 
#> 
request_registry_filter(method="get", url="http://example.com")
#> [[1]]
#> [[1]]$key
#> [1] "GET:  http://example.com   with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$count
#> [1] 1
#> 
#> [[1]]$method
#> [1] "get"
#> 
#> [[1]]$uri
#> [1] "http://example.com"
#> 
#> [[1]]$body
#> [1] NA
#> 
#> [[1]]$headers
#> [[1]]$headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
#> [[1]]$proxies
#> [1] NA
#> 
#> [[1]]$auth
#> [1] NA
#> 
#> [[1]]$url
#> [[1]]$url$url
#> [1] "http://example.com"
#> 
#> 
#> [[1]]$disk
#> [1] NA
#> 
#> [[1]]$fields
#> [1] NA
#> 
#> [[1]]$output
#> [1] NA
#> 
#> [[1]]$key
#> [1] "GET:  http://example.com   with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$request
#> <RequestSignature> 
#>   method: GET
#>   uri: http://example.com
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#> 
#> [[1]]$count
#> [1] 1
#> 
#> 
request_registry_filter(method="post", body=list(fruit = "apple"))
#> [[1]]
#> [[1]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {fruit: apple}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$count
#> [1] 1
#> 
#> [[1]]$method
#> [1] "post"
#> 
#> [[1]]$uri
#> [1] "https://hb.cran.dev/post"
#> 
#> [[1]]$body
#> [[1]]$body$fruit
#> [1] "apple"
#> 
#> 
#> [[1]]$headers
#> [[1]]$headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
#> [[1]]$proxies
#> [1] NA
#> 
#> [[1]]$auth
#> [1] NA
#> 
#> [[1]]$url
#> [[1]]$url$url
#> [1] "https://hb.cran.dev/post"
#> 
#> 
#> [[1]]$disk
#> [1] NA
#> 
#> [[1]]$fields
#> [[1]]$fields$fruit
#> [1] "apple"
#> 
#> 
#> [[1]]$output
#> [1] NA
#> 
#> [[1]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {fruit: apple}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$request
#> <RequestSignature> 
#>   method: POST
#>   uri: https://hb.cran.dev/post
#>   body: 
#>      fruit: apple
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#>   fields: 
#>      fruit: apple
#> 
#> [[1]]$count
#> [1] 1
#> 
#> 
request_registry_filter(method="post", body=list(cheese = "swiss"))
#> [[1]]
#> [[1]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {cheese: swiss}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$count
#> [1] 1
#> 
#> [[1]]$method
#> [1] "post"
#> 
#> [[1]]$uri
#> [1] "https://hb.cran.dev/post"
#> 
#> [[1]]$body
#> [[1]]$body$cheese
#> [1] "swiss"
#> 
#> 
#> [[1]]$headers
#> [[1]]$headers$Accept
#> [1] "application/json, text/xml, application/xml, */*"
#> 
#> 
#> [[1]]$proxies
#> [1] NA
#> 
#> [[1]]$auth
#> [1] NA
#> 
#> [[1]]$url
#> [[1]]$url$url
#> [1] "https://hb.cran.dev/post"
#> 
#> 
#> [[1]]$disk
#> [1] NA
#> 
#> [[1]]$fields
#> [[1]]$fields$cheese
#> [1] "swiss"
#> 
#> 
#> [[1]]$output
#> [1] NA
#> 
#> [[1]]$key
#> [1] "POST:  https://hb.cran.dev/post  with body {cheese: swiss}  with headers {Accept: application/json, text/xml, application/xml, */*}"
#> 
#> [[1]]$request
#> <RequestSignature> 
#>   method: POST
#>   uri: https://hb.cran.dev/post
#>   body: 
#>      cheese: swiss
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#>   fields: 
#>      cheese: swiss
#> 
#> [[1]]$count
#> [1] 1
#> 
#> 
request_registry_filter(method="post", body=list(cheese = "cheddar"))
#> list()
request_registry_filter(method="get", headers=list(Accept = "application/json"))
#> [[1]]
#> [[1]]$key
#> [1] "GET:  https://hb.cran.dev/get   with headers {Accept: application/json}"
#> 
#> [[1]]$count
#> [1] 1
#> 
#> [[1]]$method
#> [1] "get"
#> 
#> [[1]]$uri
#> [1] "https://hb.cran.dev/get"
#> 
#> [[1]]$body
#> [1] NA
#> 
#> [[1]]$headers
#> [[1]]$headers$Accept
#> [1] "application/json"
#> 
#> 
#> [[1]]$proxies
#> [1] NA
#> 
#> [[1]]$auth
#> [1] NA
#> 
#> [[1]]$url
#> [[1]]$url$url
#> [1] "https://hb.cran.dev/get"
#> 
#> 
#> [[1]]$disk
#> [1] NA
#> 
#> [[1]]$fields
#> [1] NA
#> 
#> [[1]]$output
#> [1] NA
#> 
#> [[1]]$key
#> [1] "GET:  https://hb.cran.dev/get   with headers {Accept: application/json}"
#> 
#> [[1]]$request
#> <RequestSignature> 
#>   method: GET
#>   uri: https://hb.cran.dev/get
#>   headers: 
#>      Accept: application/json
#> 
#> [[1]]$count
#> [1] 1
#> 
#> 

match <- request_registry_filter(method="post")[[1]]
match$request
#> <RequestSignature> 
#>   method: POST
#>   uri: https://hb.cran.dev/post
#>   body: 
#>      fruit: apple
#>   headers: 
#>      Accept: application/json, text/xml, application/xml, */*
#>   fields: 
#>      fruit: apple
match$request$to_s()
#> [1] "POST:  https://hb.cran.dev/post  with body {fruit: apple}  with headers {Accept: application/json, text/xml, application/xml, */*}"
match$count
#> [1] 1

disable()
#> CrulAdapter disabled!
#> HttrAdapter disabled!
#> Httr2Adapter disabled!
```
