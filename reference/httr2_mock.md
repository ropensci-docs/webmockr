# Turn on `httr2` mocking

Sets a callback that routes `httr2` requests through `webmockr`

## Usage

``` r
httr2_mock(on = TRUE)
```

## Arguments

- on:

  (logical) `TRUE` to turn on, `FALSE` to turn off. default: `TRUE`

## Value

Silently returns `TRUE` when enabled and `FALSE` when disabled.
