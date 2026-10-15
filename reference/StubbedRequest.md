# StubbedRequest

stubbed request class underlying
[`stub_request()`](https://docs.ropensci.org/webmockr/reference/stub_request.md)

## See also

[`stub_request()`](https://docs.ropensci.org/webmockr/reference/stub_request.md)

## Public fields

- `method`:

  \(xx\) xx

- `uri`:

  \(xx\) xx

- `uri_regex`:

  \(xx\) xx

- `regex`:

  a logical

- `uri_parts`:

  \(xx\) xx

- `host`:

  \(xx\) xx

- `query`:

  \(xx\) xx

- `body`:

  \(xx\) xx

- `basic_auth`:

  \(xx\) xx

- `request_headers`:

  \(xx\) xx

- `response_headers`:

  \(xx\) xx

- `responses_sequences`:

  \(xx\) xx

- `status_code`:

  \(xx\) xx

- `counter`:

  a StubCounter object

## Methods

### Public methods

- [`StubbedRequest$new()`](#method-StubbedRequest-initialize)

- [`StubbedRequest$print()`](#method-StubbedRequest-print)

- [`StubbedRequest$with()`](#method-StubbedRequest-with)

- [`StubbedRequest$to_return()`](#method-StubbedRequest-to_return)

- [`StubbedRequest$to_timeout()`](#method-StubbedRequest-to_timeout)

- [`StubbedRequest$to_raise()`](#method-StubbedRequest-to_raise)

- [`StubbedRequest$to_s()`](#method-StubbedRequest-to_s)

- [`StubbedRequest$reset()`](#method-StubbedRequest-reset)

- [`StubbedRequest$clone()`](#method-StubbedRequest-clone)

------------------------------------------------------------------------

### `StubbedRequest$new()`

Create a new `StubbedRequest` object

#### Usage

    StubbedRequest$new(method, uri = NULL, uri_regex = NULL)

#### Arguments

- `method`:

  the HTTP method (any, head, get, post, put, patch, or delete). "any"
  matches any HTTP method. required.

- `uri`:

  (character) request URI. either this or `uri_regex` required. webmockr
  can match uri's without the "http" scheme, but does not match if the
  scheme is "https". required, unless `uri_regex` given. See
  [UriPattern](https://docs.ropensci.org/webmockr/reference/UriPattern.md)
  for more.

- `uri_regex`:

  (character) request URI as regex. either this or `uri` required

#### Returns

A new `StubbedRequest` object

------------------------------------------------------------------------

### `StubbedRequest$print()`

print method for the `StubbedRequest` class

#### Usage

    StubbedRequest$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### `StubbedRequest$with()`

Set expectations for what's given in HTTP request

#### Usage

    StubbedRequest$with(
      query = NULL,
      body = NULL,
      headers = NULL,
      basic_auth = NULL
    )

#### Arguments

- `query`:

  (list) request query params, as a named list. optional

- `body`:

  (list) request body, as a named list. optional

- `headers`:

  (list) request headers as a named list. optional.

- `basic_auth`:

  (character) basic authentication. optional.

#### Returns

nothing returned; sets only

------------------------------------------------------------------------

### `StubbedRequest$to_return()`

Set expectations for what's returned in HTTP response

#### Usage

    StubbedRequest$to_return(status, body, headers)

#### Arguments

- `status`:

  (numeric) an HTTP status code

- `body`:

  (list) response body, one of: `character`, `json`, `list`, `raw`,
  `numeric`, `NULL`, `FALSE`, or a file connection (other connection
  types not supported)

- `headers`:

  (list) named list, response headers. optional.

#### Returns

nothing returned; sets whats to be returned

------------------------------------------------------------------------

### `StubbedRequest$to_timeout()`

Response should time out

#### Usage

    StubbedRequest$to_timeout()

#### Returns

nothing returned

------------------------------------------------------------------------

### `StubbedRequest$to_raise()`

Response should raise an exception `x`

#### Usage

    StubbedRequest$to_raise(x)

#### Arguments

- `x`:

  (character) an exception message

#### Returns

nothing returned

------------------------------------------------------------------------

### `StubbedRequest$to_s()`

Response as a character string

#### Usage

    StubbedRequest$to_s()

#### Returns

(character) the response as a string

------------------------------------------------------------------------

### `StubbedRequest$reset()`

Reset the counter for the stub

#### Usage

    StubbedRequest$reset()

#### Returns

nothing returned; resets stub counter to no requests

------------------------------------------------------------------------

### `StubbedRequest$clone()`

The objects of this class are cloneable with this method.

#### Usage

    StubbedRequest$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
