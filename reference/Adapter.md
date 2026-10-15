# Adapters for Modifying HTTP Requests

`Adapter` is the base parent class used to implement webmockr support
for different HTTP clients. It should not be used directly. Instead, use
one of the client-specific adapters that webmockr currently provides:

- `CrulAdapter` for crul

- `HttrAdapter` for httr

- `Httr2Adapter` for httr2

## Details

Note that the documented fields and methods are the same across all
client-specific adapters.

## Super class

`Adapter` -\> `CrulAdapter`

## Public fields

- `client`:

  HTTP client package name

- `name`:

  adapter name

## Methods

### Public methods

- [`CrulAdapter$clone()`](#method-CrulAdapter-clone)

Inherited methods

- [`Adapter$disable()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-disable)
- [`Adapter$enable()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-enable)
- [`Adapter$handle_request()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-handle_request)
- [`Adapter$initialize()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-initialize)
- [`Adapter$remove_stubs()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-remove_stubs)

------------------------------------------------------------------------

### `CrulAdapter$clone()`

The objects of this class are cloneable with this method.

#### Usage

    CrulAdapter$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Super class

`Adapter` -\> `HttrAdapter`

## Public fields

- `client`:

  HTTP client package name

- `name`:

  adapter name

## Methods

### Public methods

- [`HttrAdapter$clone()`](#method-HttrAdapter-clone)

Inherited methods

- [`Adapter$disable()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-disable)
- [`Adapter$enable()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-enable)
- [`Adapter$handle_request()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-handle_request)
- [`Adapter$initialize()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-initialize)
- [`Adapter$remove_stubs()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-remove_stubs)

------------------------------------------------------------------------

### `HttrAdapter$clone()`

The objects of this class are cloneable with this method.

#### Usage

    HttrAdapter$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Super class

`Adapter` -\> `Httr2Adapter`

## Public fields

- `client`:

  HTTP client package name

- `name`:

  adapter name

## Methods

### Public methods

- [`Httr2Adapter$clone()`](#method-Httr2Adapter-clone)

Inherited methods

- [`Adapter$disable()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-disable)
- [`Adapter$enable()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-enable)
- [`Adapter$handle_request()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-handle_request)
- [`Adapter$initialize()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-initialize)
- [`Adapter$remove_stubs()`](https://docs.ropensci.org/webmockr/reference/Adapter.html#method-remove_stubs)

------------------------------------------------------------------------

### `Httr2Adapter$clone()`

The objects of this class are cloneable with this method.

#### Usage

    Httr2Adapter$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Public fields

- `client`:

  HTTP client package name

- `name`:

  adapter name

## Methods

### Public methods

- [`Adapter$new()`](#method-Adapter-initialize)

- [`Adapter$enable()`](#method-Adapter-enable)

- [`Adapter$disable()`](#method-Adapter-disable)

- [`Adapter$handle_request()`](#method-Adapter-handle_request)

- [`Adapter$remove_stubs()`](#method-Adapter-remove_stubs)

- [`Adapter$clone()`](#method-Adapter-clone)

------------------------------------------------------------------------

### `Adapter$new()`

Create a new Adapter object

#### Usage

    Adapter$new()

------------------------------------------------------------------------

### `Adapter$enable()`

Enable the adapter

#### Usage

    Adapter$enable(quiet = FALSE)

#### Arguments

- `quiet`:

  (logical) suppress messages? default: `FALSE`

#### Returns

`TRUE`, invisibly

------------------------------------------------------------------------

### `Adapter$disable()`

Disable the adapter

#### Usage

    Adapter$disable(quiet = FALSE)

#### Arguments

- `quiet`:

  (logical) suppress messages? default: `FALSE`

#### Returns

`FALSE`, invisibly

------------------------------------------------------------------------

### `Adapter$handle_request()`

All logic for handling a request

#### Usage

    Adapter$handle_request(req)

#### Arguments

- `req`:

  a request

#### Returns

various outcomes

------------------------------------------------------------------------

### `Adapter$remove_stubs()`

Remove all stubs

#### Usage

    Adapter$remove_stubs()

#### Returns

nothing returned; removes all request stubs

------------------------------------------------------------------------

### `Adapter$clone()`

The objects of this class are cloneable with this method.

#### Usage

    Adapter$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
