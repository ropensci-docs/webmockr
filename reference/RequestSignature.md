# RequestSignature

General purpose request signature builder

## Public fields

- `method`:

  (character) an http method

- `uri`:

  (character) a uri

- `body`:

  (various) request body

- `headers`:

  (list) named list of headers

- `proxies`:

  (list) proxies as a named list

- `auth`:

  (list) authentication details, as a named list

- `url`:

  internal use

- `disk`:

  (character) if writing to disk, the path

- `fields`:

  (various) request body details

- `output`:

  (various) request output details, disk, memory, etc

## Methods

### Public methods

- [`RequestSignature$new()`](#method-RequestSignature-initialize)

- [`RequestSignature$print()`](#method-RequestSignature-print)

- [`RequestSignature$as_list()`](#method-RequestSignature-as_list)

- [`RequestSignature$to_s()`](#method-RequestSignature-to_s)

- [`RequestSignature$clone()`](#method-RequestSignature-clone)

------------------------------------------------------------------------

### `RequestSignature$new()`

Create a new `RequestSignature` object

#### Usage

    RequestSignature$new(method, uri, options = list())

#### Arguments

- `method`:

  the HTTP method (any, head, options, get, post, put, patch, trace, or
  delete). "any" matches any HTTP method. required.

- `uri`:

  (character) request URI. required.

- `options`:

  (list) options. optional. See Details.

#### Returns

A new `RequestSignature` object

------------------------------------------------------------------------

### `RequestSignature$print()`

print method for the `RequestSignature` class

#### Usage

    RequestSignature$print()

------------------------------------------------------------------------

### `RequestSignature$as_list()`

Request a named list with all data

#### Usage

    RequestSignature$as_list()

#### Returns

a named list

------------------------------------------------------------------------

### `RequestSignature$to_s()`

Request signature to a string

#### Usage

    RequestSignature$to_s()

#### Returns

a character string representation of the request signature

------------------------------------------------------------------------

### `RequestSignature$clone()`

The objects of this class are cloneable with this method.

#### Usage

    RequestSignature$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
# make request signature
x <- RequestSignature$new(method = "get", uri = "https:/httpbin.org/get")
# method
x$method
#> [1] "get"
# uri
x$uri
#> [1] "https:/httpbin.org/get"
# request signature to string
x$to_s()
#> [1] "GET:  https:/httpbin.org/get"

# headers
w <- RequestSignature$new(
  method = "get",
  uri = "https:/httpbin.org/get",
  options = list(headers = list(`User-Agent` = "foobar", stuff = "things"))
)
w
#> <RequestSignature> 
#>   method: GET
#>   uri: https:/httpbin.org/get
#>   headers: 
#>      User-Agent: foobar
#>      stuff: things
w$headers
#> $`User-Agent`
#> [1] "foobar"
#> 
#> $stuff
#> [1] "things"
#> 
w$to_s()
#> [1] "GET:  https:/httpbin.org/get   with headers {User-Agent: foobar, stuff: things}"

# headers and body
bb <- RequestSignature$new(
  method = "get",
  uri = "https:/httpbin.org/get",
  options = list(
    headers = list(`User-Agent` = "foobar", stuff = "things"),
    body = list(a = "tables")
  )
)
bb
#> <RequestSignature> 
#>   method: GET
#>   uri: https:/httpbin.org/get
#>   body: 
#>      a: tables
#>   headers: 
#>      User-Agent: foobar
#>      stuff: things
bb$headers
#> $`User-Agent`
#> [1] "foobar"
#> 
#> $stuff
#> [1] "things"
#> 
bb$body
#> $a
#> [1] "tables"
#> 
bb$to_s()
#> [1] "GET:  https:/httpbin.org/get  with body {a: tables}  with headers {User-Agent: foobar, stuff: things}"

# with disk path
f <- tempfile()
bb <- RequestSignature$new(
  method = "get",
  uri = "https:/httpbin.org/get",
  options = list(disk = f)
)
bb
#> <RequestSignature> 
#>   method: GET
#>   uri: https:/httpbin.org/get
#>   disk: /tmp/RtmpyaRyHd/file5967ad3c6f8
bb$disk
#> [1] "/tmp/RtmpyaRyHd/file5967ad3c6f8"
bb$to_s()
#> [1] "GET:  https:/httpbin.org/get"
```
