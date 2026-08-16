# BodyPattern

body matcher

## Public fields

- `pattern`:

  a list

- `partial`:

  bool, default: `FALSE`

- `partial_type`:

  a string, default: NULL

## Methods

### Public methods

- [`BodyPattern$new()`](#method-BodyPattern-initialize)

- [`BodyPattern$matches()`](#method-BodyPattern-matches)

- [`BodyPattern$to_s()`](#method-BodyPattern-to_s)

- [`BodyPattern$clone()`](#method-BodyPattern-clone)

------------------------------------------------------------------------

### `BodyPattern$new()`

Create a new `BodyPattern` object

#### Usage

    BodyPattern$new(pattern)

#### Arguments

- `pattern`:

  (list) a body object - from a request stub (i.e., the mock)

#### Returns

A new `BodyPattern` object

------------------------------------------------------------------------

### `BodyPattern$matches()`

Match a request body pattern against a pattern

#### Usage

    BodyPattern$matches(body, content_type = "")

#### Arguments

- `body`:

  (list) the body, i.e., from the HTTP request

- `content_type`:

  (character) content type

#### Returns

a boolean

------------------------------------------------------------------------

### `BodyPattern$to_s()`

Print pattern for easy human consumption

#### Usage

    BodyPattern$to_s()

#### Returns

a string

------------------------------------------------------------------------

### `BodyPattern$clone()`

The objects of this class are cloneable with this method.

#### Usage

    BodyPattern$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
