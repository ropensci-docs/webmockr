# Turn on `httr` mocking

Sets a callback that routes `httr` requests through `webmockr`

## Usage

``` r
httr_mock(on = TRUE)
```

## Arguments

- on:

  (logical) set to `TRUE` to turn on, and `FALSE` to turn off. default:
  `TRUE`

## Value

Silently returns `TRUE` when enabled and `FALSE` when disabled.
