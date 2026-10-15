# HeadersPattern

headers matcher

## Details

`webmockr` normalises headers and treats all forms of same headers as
equal: i.e the following two sets of headers are equal:
`list(Header1 = "value1", content_length = 123, X_CuStOm_hEAder = "foo")`
and
`list(header1 = "value1", "Content-Length" = 123, "x-cuSTOM-HeAder" = "foo")`

## Public fields

- `pattern`:

  a list

## Methods

### Public methods

- [`HeadersPattern$new()`](#method-HeadersPattern-initialize)

- [`HeadersPattern$matches()`](#method-HeadersPattern-matches)

- [`HeadersPattern$empty_headers()`](#method-HeadersPattern-empty_headers)

- [`HeadersPattern$to_s()`](#method-HeadersPattern-to_s)

- [`HeadersPattern$clone()`](#method-HeadersPattern-clone)

------------------------------------------------------------------------

### `HeadersPattern$new()`

Create a new `HeadersPattern` object

#### Usage

    HeadersPattern$new(pattern)

#### Arguments

- `pattern`:

  (list) a pattern, as a named list, must be named, e.g,.
  `list(a = 5, b = 6)`

#### Returns

A new `HeadersPattern` object

------------------------------------------------------------------------

### `HeadersPattern$matches()`

Match a list of headers against that stored

#### Usage

    HeadersPattern$matches(headers)

#### Arguments

- `headers`:

  (list) named list of headers, e.g,. `list(a = 5, b = 6)`

#### Returns

a boolean

------------------------------------------------------------------------

### `HeadersPattern$empty_headers()`

Are headers empty? tests if null or length==0

#### Usage

    HeadersPattern$empty_headers(headers)

#### Arguments

- `headers`:

  named list of headers

#### Returns

a boolean

------------------------------------------------------------------------

### `HeadersPattern$to_s()`

Print pattern for easy human consumption

#### Usage

    HeadersPattern$to_s()

#### Returns

a string

------------------------------------------------------------------------

### `HeadersPattern$clone()`

The objects of this class are cloneable with this method.

#### Usage

    HeadersPattern$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
