# Extract the body from an HTTP request

Returns an appropriate representation of the data contained within a
request body based on its encoding.

## Usage

``` r
pluck_body(x)
```

## Arguments

- x:

  an unexecuted crul, httr *or* httr2 request object

## Value

one of the following:

- `NULL` if the request is not associated with a body

- `NULL` if an upload is used not in a list

- list containing the multipart-encoded body

- character vector with the JSON- or raw-encoded body, or upload form
  file
