# Package index

## webmockr

High level overview of package

- [`webmockr`](https://docs.ropensci.org/webmockr/reference/webmockr-package.md)
  [`webmockr-package`](https://docs.ropensci.org/webmockr/reference/webmockr-package.md)
  : webmockr: Stubbing and Setting Expectations on 'HTTP' Requests

- [`webmockr-defunct`](https://docs.ropensci.org/webmockr/reference/webmockr-defunct.md)
  :

  Defunct functions in webmockr

## Stubbing requests

- [`stub_request()`](https://docs.ropensci.org/webmockr/reference/stub_request.md)
  : Stub an http request
- [`remove_request_stub()`](https://docs.ropensci.org/webmockr/reference/remove_request_stub.md)
  : Remove a request stub
- [`to_raise()`](https://docs.ropensci.org/webmockr/reference/to_raise.md)
  : Set raise error condition
- [`to_return()`](https://docs.ropensci.org/webmockr/reference/to_return.md)
  : Expectation for what's returned from a stubbed request
- [`to_timeout()`](https://docs.ropensci.org/webmockr/reference/to_timeout.md)
  : Set timeout as an expected return on a match
- [`wi_th()`](https://docs.ropensci.org/webmockr/reference/wi_th.md) :
  Set additional parts of a stubbed request
- [`including()`](https://docs.ropensci.org/webmockr/reference/including.md)
  [`excluding()`](https://docs.ropensci.org/webmockr/reference/including.md)
  : Partially match request query parameters or request bodies

## Enable/Disable webmockr

- [`enable()`](https://docs.ropensci.org/webmockr/reference/enable.md)
  [`enabled()`](https://docs.ropensci.org/webmockr/reference/enable.md)
  [`disable()`](https://docs.ropensci.org/webmockr/reference/enable.md)
  : Enable or disable webmockr

- [`httr_mock()`](https://docs.ropensci.org/webmockr/reference/httr_mock.md)
  :

  Turn on `httr` mocking

- [`httr2_mock()`](https://docs.ropensci.org/webmockr/reference/httr2_mock.md)
  :

  Turn on `httr2` mocking

## Stub and Request registries

- [`stub_registry()`](https://docs.ropensci.org/webmockr/reference/stub_registry.md)
  : List stubs in the stub registry
- [`stub_registry_clear()`](https://docs.ropensci.org/webmockr/reference/stub_registry_clear.md)
  : stub_registry_clear
- [`request_registry()`](https://docs.ropensci.org/webmockr/reference/request_registry.md)
  [`request_registry_clear()`](https://docs.ropensci.org/webmockr/reference/request_registry.md)
  : List or clear requests in the request registry
- [`request_registry_filter()`](https://docs.ropensci.org/webmockr/reference/request_registry_filter.md)
  : Request registry filter
- [`webmockr_reset()`](https://docs.ropensci.org/webmockr/reference/webmockr_reset.md)
  : webmockr_reset

## Configuration

- [`webmockr_configure()`](https://docs.ropensci.org/webmockr/reference/webmockr_configure.md)
  [`webmockr_configure_reset()`](https://docs.ropensci.org/webmockr/reference/webmockr_configure.md)
  [`webmockr_configuration()`](https://docs.ropensci.org/webmockr/reference/webmockr_configure.md)
  [`webmockr_allow_net_connect()`](https://docs.ropensci.org/webmockr/reference/webmockr_configure.md)
  [`webmockr_disable_net_connect()`](https://docs.ropensci.org/webmockr/reference/webmockr_configure.md)
  [`webmockr_net_connect_allowed()`](https://docs.ropensci.org/webmockr/reference/webmockr_configure.md)
  : webmockr configuration

## Mocking writing to disk

- [`mock_file()`](https://docs.ropensci.org/webmockr/reference/mock_file.md)
  : Mock file
- [`mocking-disk-writing`](https://docs.ropensci.org/webmockr/reference/mocking-disk-writing.md)
  : Mocking writing to disk

## Introspection

- [`last_request()`](https://docs.ropensci.org/webmockr/reference/last_request.md)
  : Get the last HTTP request made
- [`last_stub()`](https://docs.ropensci.org/webmockr/reference/last_stub.md)
  : Get the last stub created
- [`stub_body_diff()`](https://docs.ropensci.org/webmockr/reference/stub_body_diff.md)
  : Get a diff of a stub request body and a request body from an http
  request
