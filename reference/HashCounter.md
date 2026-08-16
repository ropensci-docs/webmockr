# HashCounter

hash with counter, to store requests, and count each time it is used

## See also

Other request-registry:
[`RequestRegistry`](https://docs.ropensci.org/webmockr/reference/RequestRegistry.md),
[`request_registry()`](https://docs.ropensci.org/webmockr/reference/request_registry.md)

## Public fields

- `hash`:

  (list) a list for internal use only, with elements `key`, `sig`, and
  `count`

## Methods

### Public methods

- [`HashCounter$put()`](#method-HashCounter-put)

- [`HashCounter$get()`](#method-HashCounter-get)

- [`HashCounter$clone()`](#method-HashCounter-clone)

------------------------------------------------------------------------

### `HashCounter$put()`

Register a request by it's key

#### Usage

    HashCounter$put(req_sig)

#### Arguments

- `req_sig`:

  an object of class `RequestSignature`

#### Returns

nothing returned; registers request and iterates internal counter

------------------------------------------------------------------------

### `HashCounter$get()`

Get a request by key

#### Usage

    HashCounter$get(req_sig)

#### Arguments

- `req_sig`:

  an object of class `RequestSignature`

#### Returns

(integer) the count of how many times the request has been made

------------------------------------------------------------------------

### `HashCounter$clone()`

The objects of this class are cloneable with this method.

#### Usage

    HashCounter$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
