# RequestRegistry

keeps track of HTTP requests

## See also

[`stub_registry()`](https://docs.ropensci.org/webmockr/reference/stub_registry.md)
and
[StubRegistry](https://docs.ropensci.org/webmockr/reference/StubRegistry.md)

Other request-registry:
[`HashCounter`](https://docs.ropensci.org/webmockr/reference/HashCounter.md),
[`request_registry()`](https://docs.ropensci.org/webmockr/reference/request_registry.md)

## Public fields

- `request_signatures`:

  a HashCounter object

## Methods

### Public methods

- [`RequestRegistry$print()`](#method-RequestRegistry-print)

- [`RequestRegistry$reset()`](#method-RequestRegistry-reset)

- [`RequestRegistry$register_request()`](#method-RequestRegistry-register_request)

- [`RequestRegistry$times_executed()`](#method-RequestRegistry-times_executed)

- [`RequestRegistry$clone()`](#method-RequestRegistry-clone)

------------------------------------------------------------------------

### `RequestRegistry$print()`

print method for the `RequestRegistry` class

#### Usage

    RequestRegistry$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### `RequestRegistry$reset()`

Reset the registry to no registered requests

#### Usage

    RequestRegistry$reset()

#### Returns

nothing returned; resets registry to no requests

------------------------------------------------------------------------

### `RequestRegistry$register_request()`

Register a request

#### Usage

    RequestRegistry$register_request(request)

#### Arguments

- `request`:

  a character string of the request, serialized from a
  `RequestSignature$new(...)$to_s()`

#### Returns

nothing returned; registers the request

------------------------------------------------------------------------

### `RequestRegistry$times_executed()`

How many times has a request been made

#### Usage

    RequestRegistry$times_executed(request_pattern)

#### Arguments

- `request_pattern`:

  an object of class `RequestPattern`

#### Details

if no match is found for the request pattern, 0 is returned

#### Returns

integer, the number of times the request has been made

------------------------------------------------------------------------

### `RequestRegistry$clone()`

The objects of this class are cloneable with this method.

#### Usage

    RequestRegistry$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
