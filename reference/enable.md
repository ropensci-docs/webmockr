# Enable or disable webmockr

Enable or disable webmockr

## Usage

``` r
enable(adapter = NULL, options = list(), quiet = FALSE)

enabled(adapter = "crul")

disable(adapter = NULL, options = list(), quiet = FALSE)
```

## Arguments

- adapter:

  (character) the adapter name, 'crul', 'httr', or 'httr2'. one or the
  other. if none given, we attempt to enable both adapters

- options:

  list of options - ignored for now.

- quiet:

  (logical) suppress messages? default: `FALSE`

## Value

`enable()` and `disable()` invisibly returns booleans for each adapter,
as a result of running enable or disable, respectively, on each
[HttpLibAdapaterRegistry](https://docs.ropensci.org/webmockr/reference/HttpLibAdapaterRegistry.md)
object. `enabled` returns a single boolean

## Details

- `enable()` enables webmockr for all adapters

- `disable()` disables webmockr for all adapters

- `enabled()` answers whether webmockr is enabled for a given adapter
