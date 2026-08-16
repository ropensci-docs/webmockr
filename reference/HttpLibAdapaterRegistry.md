# HttpLibAdapaterRegistry

http lib adapter registry

## Public fields

- `adapters`:

  list

## Methods

### Public methods

- [`HttpLibAdapaterRegistry$print()`](#method-HttpLibAdapaterRegistry-print)

- [`HttpLibAdapaterRegistry$register()`](#method-HttpLibAdapaterRegistry-register)

- [`HttpLibAdapaterRegistry$clone()`](#method-HttpLibAdapaterRegistry-clone)

------------------------------------------------------------------------

### `HttpLibAdapaterRegistry$print()`

print method for the `HttpLibAdapaterRegistry` class

#### Usage

    HttpLibAdapaterRegistry$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### `HttpLibAdapaterRegistry$register()`

Register an http library adapter

#### Usage

    HttpLibAdapaterRegistry$register(x)

#### Arguments

- `x`:

  an http lib adapter, e.g.,
  [CrulAdapter](https://docs.ropensci.org/webmockr/reference/Adapter.md)

#### Returns

nothing, registers the library adapter

------------------------------------------------------------------------

### `HttpLibAdapaterRegistry$clone()`

The objects of this class are cloneable with this method.

#### Usage

    HttpLibAdapaterRegistry$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
