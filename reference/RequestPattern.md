# RequestPattern class

Class handling all request matchers

## See also

pattern classes for HTTP method
[MethodPattern](https://docs.ropensci.org/webmockr/reference/MethodPattern.md),
headers
[HeadersPattern](https://docs.ropensci.org/webmockr/reference/HeadersPattern.md),
body
[BodyPattern](https://docs.ropensci.org/webmockr/reference/BodyPattern.md),
and URI/URL
[UriPattern](https://docs.ropensci.org/webmockr/reference/UriPattern.md)

## Public fields

- `method_pattern`:

  xxx

- `uri_pattern`:

  xxx

- `body_pattern`:

  xxx

- `headers_pattern`:

  xxx

## Methods

### Public methods

- [`RequestPattern$new()`](#method-RequestPattern-initialize)

- [`RequestPattern$matches()`](#method-RequestPattern-matches)

- [`RequestPattern$to_s()`](#method-RequestPattern-to_s)

- [`RequestPattern$clone()`](#method-RequestPattern-clone)

------------------------------------------------------------------------

### `RequestPattern$new()`

Create a new `RequestPattern` object

#### Usage

    RequestPattern$new(
      method,
      uri = NULL,
      uri_regex = NULL,
      query = NULL,
      body = NULL,
      headers = NULL,
      basic_auth = NULL
    )

#### Arguments

- `method`:

  the HTTP method (any, head, options, get, post, put, patch, trace, or
  delete). "any" matches any HTTP method. required.

- `uri`:

  (character) request URI. required or uri_regex

- `uri_regex`:

  (character) request URI as regex. required or uri

- `query`:

  (list) query parameters, optional

- `body`:

  (list) body request, optional

- `headers`:

  (list) headers, optional

- `basic_auth`:

  (list) vector of length 2 (username, password), optional

#### Returns

A new `RequestPattern` object

------------------------------------------------------------------------

### `RequestPattern$matches()`

does a request signature match the selected matchers?

#### Usage

    RequestPattern$matches(request_signature)

#### Arguments

- `request_signature`:

  a
  [RequestSignature](https://docs.ropensci.org/webmockr/reference/RequestSignature.md)
  object

#### Returns

a boolean

------------------------------------------------------------------------

### `RequestPattern$to_s()`

Print pattern for easy human consumption

#### Usage

    RequestPattern$to_s()

#### Returns

a string

------------------------------------------------------------------------

### `RequestPattern$clone()`

The objects of this class are cloneable with this method.

#### Usage

    RequestPattern$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
