# UriPattern

uri matcher

## Public fields

- `pattern`:

  (character) pattern holder

- `regex`:

  a logical

- `query_params`:

  a list, or `NULL` if empty

- `partial`:

  bool, default: `FALSE`

- `partial_type`:

  a string, default: NULL

## Methods

### Public methods

- [`UriPattern$new()`](#method-UriPattern-initialize)

- [`UriPattern$matches()`](#method-UriPattern-matches)

- [`UriPattern$pattern_matches()`](#method-UriPattern-pattern_matches)

- [`UriPattern$query_params_matches()`](#method-UriPattern-query_params_matches)

- [`UriPattern$extract_query()`](#method-UriPattern-extract_query)

- [`UriPattern$add_query_params()`](#method-UriPattern-add_query_params)

- [`UriPattern$to_s()`](#method-UriPattern-to_s)

- [`UriPattern$clone()`](#method-UriPattern-clone)

------------------------------------------------------------------------

### `UriPattern$new()`

Create a new `UriPattern` object

#### Usage

    UriPattern$new(pattern = NULL, regex_pattern = NULL)

#### Arguments

- `pattern`:

  (character) a uri, as a character string. if scheme is missing, it is
  added (we assume http)

- `regex_pattern`:

  (character) a uri as a regex character string, see
  [base::regex](https://rdrr.io/r/base/regex.html). if scheme is
  missing, it is added (we assume http)

#### Returns

A new `UriPattern` object

------------------------------------------------------------------------

### `UriPattern$matches()`

Match a uri against a pattern

#### Usage

    UriPattern$matches(uri)

#### Arguments

- `uri`:

  (character) a uri

#### Returns

a boolean

------------------------------------------------------------------------

### `UriPattern$pattern_matches()`

Match a URI

#### Usage

    UriPattern$pattern_matches(uri)

#### Arguments

- `uri`:

  (character) a uri

#### Returns

a boolean

------------------------------------------------------------------------

### `UriPattern$query_params_matches()`

Match query parameters of a URI

#### Usage

    UriPattern$query_params_matches(uri)

#### Arguments

- `uri`:

  (character) a uri

#### Returns

a boolean

------------------------------------------------------------------------

### `UriPattern$extract_query()`

Extract query parameters as a named list

#### Usage

    UriPattern$extract_query(uri)

#### Arguments

- `uri`:

  (character) a uri

#### Returns

named list, or `NULL` if no query parameters

------------------------------------------------------------------------

### `UriPattern$add_query_params()`

Add query parameters to the URI

#### Usage

    UriPattern$add_query_params(query_params)

#### Arguments

- `query_params`:

  (list\|character) list or character

#### Returns

nothing returned, updates uri pattern

------------------------------------------------------------------------

### `UriPattern$to_s()`

Print pattern for easy human consumption

#### Usage

    UriPattern$to_s()

#### Returns

a string

------------------------------------------------------------------------

### `UriPattern$clone()`

The objects of this class are cloneable with this method.

#### Usage

    UriPattern$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
