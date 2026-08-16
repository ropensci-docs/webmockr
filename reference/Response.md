# Response

custom webmockr http response class

## Public fields

- `url`:

  (character) a url

- `body`:

  (various) list, character, etc

- `content`:

  (various) response content/body

- `request_headers`:

  (list) a named list

- `response_headers`:

  (list) a named list

- `options`:

  (character) list

- `status_code`:

  (integer) an http status code

- `exception`:

  (character) an exception message

- `should_timeout`:

  (logical) should the response timeout?

## Methods

### Public methods

- [`Response$new()`](#method-Response-initialize)

- [`Response$print()`](#method-Response-print)

- [`Response$set_url()`](#method-Response-set_url)

- [`Response$get_url()`](#method-Response-get_url)

- [`Response$set_request_headers()`](#method-Response-set_request_headers)

- [`Response$get_request_headers()`](#method-Response-get_request_headers)

- [`Response$set_response_headers()`](#method-Response-set_response_headers)

- [`Response$get_respone_headers()`](#method-Response-get_respone_headers)

- [`Response$set_body()`](#method-Response-set_body)

- [`Response$get_body()`](#method-Response-get_body)

- [`Response$set_status()`](#method-Response-set_status)

- [`Response$get_status()`](#method-Response-get_status)

- [`Response$set_exception()`](#method-Response-set_exception)

- [`Response$get_exception()`](#method-Response-get_exception)

- [`Response$clone()`](#method-Response-clone)

------------------------------------------------------------------------

### `Response$new()`

Create a new `Response` object

#### Usage

    Response$new(options = list())

#### Arguments

- `options`:

  (list) a list of options

#### Returns

A new `Response` object

------------------------------------------------------------------------

### `Response$print()`

print method for the `Response` class

#### Usage

    Response$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### `Response$set_url()`

set the url for the response

#### Usage

    Response$set_url(url)

#### Arguments

- `url`:

  (character) a url

#### Returns

nothing returned; sets url

------------------------------------------------------------------------

### `Response$get_url()`

get the url for the response

#### Usage

    Response$get_url()

#### Returns

(character) a url

------------------------------------------------------------------------

### `Response$set_request_headers()`

set the request headers for the response

#### Usage

    Response$set_request_headers(headers, capitalize = TRUE)

#### Arguments

- `headers`:

  (list) named list

- `capitalize`:

  (logical) whether to capitalize first letters of each header; default:
  `TRUE`

#### Returns

nothing returned; sets request headers on the response

------------------------------------------------------------------------

### `Response$get_request_headers()`

get the request headers for the response

#### Usage

    Response$get_request_headers()

#### Returns

(list) request headers, a named list

------------------------------------------------------------------------

### `Response$set_response_headers()`

set the response headers for the response

#### Usage

    Response$set_response_headers(headers, capitalize = TRUE)

#### Arguments

- `headers`:

  (list) named list

- `capitalize`:

  (logical) whether to capitalize first letters of each header; default:
  `TRUE`

#### Returns

nothing returned; sets response headers on the response

------------------------------------------------------------------------

### `Response$get_respone_headers()`

get the response headers for the response

#### Usage

    Response$get_respone_headers()

#### Returns

(list) response headers, a named list

------------------------------------------------------------------------

### `Response$set_body()`

set the body of the response

#### Usage

    Response$set_body(body, disk = FALSE)

#### Arguments

- `body`:

  (various types)

- `disk`:

  (logical) whether its on disk; default: `FALSE`

#### Returns

nothing returned; sets body on the response

------------------------------------------------------------------------

### `Response$get_body()`

get the body of the response

#### Usage

    Response$get_body()

#### Returns

various

------------------------------------------------------------------------

### `Response$set_status()`

set the http status of the response

#### Usage

    Response$set_status(status)

#### Arguments

- `status`:

  (integer) the http status

#### Returns

nothing returned; sets the http status of the response

------------------------------------------------------------------------

### `Response$get_status()`

get the http status of the response

#### Usage

    Response$get_status()

#### Returns

(integer) the http status

------------------------------------------------------------------------

### `Response$set_exception()`

set an exception

#### Usage

    Response$set_exception(exception)

#### Arguments

- `exception`:

  (character) an exception string

#### Returns

nothing returned; sets an exception

------------------------------------------------------------------------

### `Response$get_exception()`

get the exception, if set

#### Usage

    Response$get_exception()

#### Returns

(character) an exception

------------------------------------------------------------------------

### `Response$clone()`

The objects of this class are cloneable with this method.

#### Usage

    Response$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
(x <- Response$new())
#> <webmockr response> 
#>   url: 
#>   status: 200
#>   headers: 
#>     request headers: 
#>     response headers: 
#>   exception: 
#>   body length: 0

x$set_url("https://httpbin.org/get")
x
#> <webmockr response> 
#>   url: https://httpbin.org/get
#>   status: 200
#>   headers: 
#>     request headers: 
#>     response headers: 
#>   exception: 
#>   body length: 0

x$set_request_headers(list("Content-Type" = "application/json"))
x
#> <webmockr response> 
#>   url: https://httpbin.org/get
#>   status: 200
#>   headers: 
#>     request headers: 
#>      Content-Type: application/json
#>     response headers: 
#>   exception: 
#>   body length: 0
x$request_headers
#> $`Content-Type`
#> [1] "application/json"
#> 

x$set_response_headers(list("Host" = "httpbin.org"))
x
#> <webmockr response> 
#>   url: https://httpbin.org/get
#>   status: 200
#>   headers: 
#>     request headers: 
#>      Content-Type: application/json
#>     response headers: 
#>      Host: httpbin.org
#>   exception: 
#>   body length: 0
x$response_headers
#> $Host
#> [1] "httpbin.org"
#> 

x$set_status(404)
x
#> <webmockr response> 
#>   url: https://httpbin.org/get
#>   status: 404
#>   headers: 
#>     request headers: 
#>      Content-Type: application/json
#>     response headers: 
#>      Host: httpbin.org
#>   exception: 
#>   body length: 0
x$get_status()
#> [1] 404

x$set_body("hello world")
x
#> <webmockr response> 
#>   url: https://httpbin.org/get
#>   status: 404
#>   headers: 
#>     request headers: 
#>      Content-Type: application/json
#>     response headers: 
#>      Host: httpbin.org
#>   exception: 
#>   body length: 11
x$get_body()
#>  [1] 68 65 6c 6c 6f 20 77 6f 72 6c 64
# raw body
x$set_body(charToRaw("hello world"))
x
#> <webmockr response> 
#>   url: https://httpbin.org/get
#>   status: 404
#>   headers: 
#>     request headers: 
#>      Content-Type: application/json
#>     response headers: 
#>      Host: httpbin.org
#>   exception: 
#>   body length: 11
x$get_body()
#>  [1] 68 65 6c 6c 6f 20 77 6f 72 6c 64

x$set_exception("exception")
x
#> <webmockr response> 
#>   url: https://httpbin.org/get
#>   status: 404
#>   headers: 
#>     request headers: 
#>      Content-Type: application/json
#>     response headers: 
#>      Host: httpbin.org
#>   exception: exception
#>   body length: 11
x$get_exception()
#> [1] "exception"
```
