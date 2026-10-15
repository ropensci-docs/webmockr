# StubCounter

hash with counter to store requests and count number of requests made
against the stub

## Public fields

- `hash`:

  (list) a list for internal use only, with elements `key`, `sig`, and
  `count`

## Methods

### Public methods

- [`StubCounter$put()`](#method-StubCounter-put)

- [`StubCounter$count()`](#method-StubCounter-count)

- [`StubCounter$clone()`](#method-StubCounter-clone)

------------------------------------------------------------------------

### `StubCounter$put()`

Register a request by it's key

#### Usage

    StubCounter$put(x)

#### Arguments

- `x`:

  an object of class `RequestSignature`

#### Returns

nothing returned; registers request & iterates internal counter

------------------------------------------------------------------------

### `StubCounter$count()`

Get the count of number of times any matching request has been made
against this stub

#### Usage

    StubCounter$count()

------------------------------------------------------------------------

### `StubCounter$clone()`

The objects of this class are cloneable with this method.

#### Usage

    StubCounter$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
