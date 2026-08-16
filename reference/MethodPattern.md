# MethodPattern

method matcher

## Details

Matches regardless of case. e.g., POST will match to post

## Public fields

- `pattern`:

  (character) an http method

## Methods

### Public methods

- [`MethodPattern$new()`](#method-MethodPattern-initialize)

- [`MethodPattern$matches()`](#method-MethodPattern-matches)

- [`MethodPattern$to_s()`](#method-MethodPattern-to_s)

- [`MethodPattern$clone()`](#method-MethodPattern-clone)

------------------------------------------------------------------------

### `MethodPattern$new()`

Create a new `MethodPattern` object

#### Usage

    MethodPattern$new(pattern)

#### Arguments

- `pattern`:

  (character) a HTTP method, lowercase

#### Returns

A new `MethodPattern` object

------------------------------------------------------------------------

### `MethodPattern$matches()`

test if the pattern matches a given http method

#### Usage

    MethodPattern$matches(method)

#### Arguments

- `method`:

  (character) a HTTP method, lowercase

#### Returns

a boolean

------------------------------------------------------------------------

### `MethodPattern$to_s()`

Print pattern for easy human consumption

#### Usage

    MethodPattern$to_s()

#### Returns

a string

------------------------------------------------------------------------

### `MethodPattern$clone()`

The objects of this class are cloneable with this method.

#### Usage

    MethodPattern$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
