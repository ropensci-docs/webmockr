# webmockr configuration

webmockr configuration

## Usage

``` r
webmockr_configure(
  allow_net_connect = FALSE,
  allow_localhost = FALSE,
  allow = NULL,
  show_stubbing_instructions = TRUE,
  show_body_diff = FALSE
)

webmockr_configure_reset()

webmockr_configuration()

webmockr_allow_net_connect()

webmockr_disable_net_connect(allow = NULL)

webmockr_net_connect_allowed(uri = NULL)
```

## Arguments

- allow_net_connect:

  (logical) Default: `FALSE`

- allow_localhost:

  (logical) Default: `FALSE`

- allow:

  (character) one or more URI/URL to allow (and by extension all others
  are not allowed)

- show_stubbing_instructions:

  (logical) Default: `TRUE`. If `FALSE`, stubbing instructions are not
  shown

- show_body_diff:

  (logical) Default: `FALSE`. If `TRUE` show's a diff of the stub's
  request body and the http request body. See also
  [`stub_body_diff()`](https://docs.ropensci.org/webmockr/reference/stub_body_diff.md)
  for manually comparing request and stub bodies. Under the hood the
  Suggested package `diffobj` is required to do the comparison.

- uri:

  (character) a URI/URL as a character string - to determine whether or
  not it is allowed

## webmockr_allow_net_connect

If there are stubs found for a request, even if net connections are
allowed (by running `webmockr_allow_net_connect()`) the stubbed response
will be returned. If no stub is found, and net connections are allowed,
then a real HTTP request can be made.

## Examples

``` r
webmockr_configure()
#> <webmockr configuration>
#>   crul enabled?: TRUE
#>   httr enabled?: TRUE
#>   httr2 enabled?: FALSE
#>   allow_net_connect?: FALSE
#>   allow_localhost?: FALSE
#>   allow: 
#>   show_stubbing_instructions: TRUE
#>   show_body_diff: FALSE
webmockr_configure(
  allow_localhost = TRUE
)
#> <webmockr configuration>
#>   crul enabled?: TRUE
#>   httr enabled?: TRUE
#>   httr2 enabled?: FALSE
#>   allow_net_connect?: FALSE
#>   allow_localhost?: TRUE
#>   allow: 
#>   show_stubbing_instructions: TRUE
#>   show_body_diff: FALSE
webmockr_configuration()
#> <webmockr configuration>
#>   crul enabled?: TRUE
#>   httr enabled?: TRUE
#>   httr2 enabled?: FALSE
#>   allow_net_connect?: FALSE
#>   allow_localhost?: TRUE
#>   allow: 
#>   show_stubbing_instructions: TRUE
#>   show_body_diff: FALSE
webmockr_configure_reset()
#> <webmockr configuration>
#>   crul enabled?: TRUE
#>   httr enabled?: TRUE
#>   httr2 enabled?: FALSE
#>   allow_net_connect?: FALSE
#>   allow_localhost?: FALSE
#>   allow: 
#>   show_stubbing_instructions: TRUE
#>   show_body_diff: FALSE

webmockr_allow_net_connect()
#> net connect allowed
webmockr_net_connect_allowed()
#> [1] TRUE

# disable net connect for any URIs
webmockr_disable_net_connect()
#> net connect disabled
### gives NULL with no URI passed
webmockr_net_connect_allowed()
#> [1] FALSE
# disable net connect EXCEPT FOR given URIs
webmockr_disable_net_connect(allow = "google.com")
#> net connect disabled
### is a specific URI allowed?
webmockr_net_connect_allowed("google.com")
#> [1] TRUE

# show body diff
webmockr_configure(show_body_diff = TRUE)
#> <webmockr configuration>
#>   crul enabled?: TRUE
#>   httr enabled?: TRUE
#>   httr2 enabled?: FALSE
#>   allow_net_connect?: FALSE
#>   allow_localhost?: FALSE
#>   allow: 
#>   show_stubbing_instructions: TRUE
#>   show_body_diff: TRUE

# cleanup
webmockr_configure_reset()
#> <webmockr configuration>
#>   crul enabled?: TRUE
#>   httr enabled?: TRUE
#>   httr2 enabled?: FALSE
#>   allow_net_connect?: FALSE
#>   allow_localhost?: FALSE
#>   allow: 
#>   show_stubbing_instructions: TRUE
#>   show_body_diff: FALSE
```
