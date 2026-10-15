# StubRegistry

stub registry to keep track of
[StubbedRequest](https://docs.ropensci.org/webmockr/reference/StubbedRequest.md)
stubs

## See also

Other stub-registry:
[`remove_request_stub()`](https://docs.ropensci.org/webmockr/reference/remove_request_stub.md),
[`stub_registry()`](https://docs.ropensci.org/webmockr/reference/stub_registry.md),
[`stub_registry_clear()`](https://docs.ropensci.org/webmockr/reference/stub_registry_clear.md)

## Public fields

- `request_stubs`:

  (list) list of request stubs

## Methods

### Public methods

- [`StubRegistry$print()`](#method-StubRegistry-print)

- [`StubRegistry$register_stub()`](#method-StubRegistry-register_stub)

- [`StubRegistry$find_stubbed_request()`](#method-StubRegistry-find_stubbed_request)

- [`StubRegistry$request_stub_for()`](#method-StubRegistry-request_stub_for)

- [`StubRegistry$remove_request_stub()`](#method-StubRegistry-remove_request_stub)

- [`StubRegistry$remove_all_request_stubs()`](#method-StubRegistry-remove_all_request_stubs)

- [`StubRegistry$is_registered()`](#method-StubRegistry-is_registered)

- [`StubRegistry$is_stubbed()`](#method-StubRegistry-is_stubbed)

- [`StubRegistry$clone()`](#method-StubRegistry-clone)

------------------------------------------------------------------------

### `StubRegistry$print()`

print method for the `StubRegistry` class

#### Usage

    StubRegistry$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### `StubRegistry$register_stub()`

Register a stub

#### Usage

    StubRegistry$register_stub(stub)

#### Arguments

- `stub`:

  an object of type
  [StubbedRequest](https://docs.ropensci.org/webmockr/reference/StubbedRequest.md)

#### Returns

nothing returned; registers the stub

------------------------------------------------------------------------

### `StubRegistry$find_stubbed_request()`

Find a stubbed request

#### Usage

    StubRegistry$find_stubbed_request(req)

#### Arguments

- `req`:

  an object of class
  [RequestSignature](https://docs.ropensci.org/webmockr/reference/RequestSignature.md)

#### Returns

an object of type
[StubbedRequest](https://docs.ropensci.org/webmockr/reference/StubbedRequest.md),
if matched

------------------------------------------------------------------------

### `StubRegistry$request_stub_for()`

Find a stubbed request

#### Usage

    StubRegistry$request_stub_for(request_signature, count = TRUE)

#### Arguments

- `request_signature`:

  an object of class
  [RequestSignature](https://docs.ropensci.org/webmockr/reference/RequestSignature.md)

- `count`:

  (bool) iterate counter or not. default: `TRUE`

#### Returns

logical, 1 or more

------------------------------------------------------------------------

### `StubRegistry$remove_request_stub()`

Remove a stubbed request by matching request signature

#### Usage

    StubRegistry$remove_request_stub(stub)

#### Arguments

- `stub`:

  an object of type
  [StubbedRequest](https://docs.ropensci.org/webmockr/reference/StubbedRequest.md)

#### Returns

nothing returned; removes the stub from the registry

------------------------------------------------------------------------

### `StubRegistry$remove_all_request_stubs()`

Remove all request stubs

#### Usage

    StubRegistry$remove_all_request_stubs()

#### Returns

nothing returned; removes all request stubs

------------------------------------------------------------------------

### `StubRegistry$is_registered()`

Find a stubbed request from a request signature

#### Usage

    StubRegistry$is_registered(x)

#### Arguments

- `x`:

  an object of class
  [RequestSignature](https://docs.ropensci.org/webmockr/reference/RequestSignature.md)

#### Returns

nothing returned; registers the stub

------------------------------------------------------------------------

### `StubRegistry$is_stubbed()`

Check if a stubbed request is in the stub registry

#### Usage

    StubRegistry$is_stubbed(stub)

#### Arguments

- `stub`:

  an object of class
  [StubbedRequest](https://docs.ropensci.org/webmockr/reference/StubbedRequest.md)

#### Returns

single boolean, `TRUE` or `FALSE`

------------------------------------------------------------------------

### `StubRegistry$clone()`

The objects of this class are cloneable with this method.

#### Usage

    StubRegistry$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
