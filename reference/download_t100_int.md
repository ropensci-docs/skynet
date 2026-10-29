# Download Data from T100 international files

Downloads data from BTS/RITA/Transtats and imports it into R

## Usage

``` r
download_t100_int(y = NULL, type = NULL)
```

## Arguments

- y:

  year to be imported

- type:

  "mkt" for Market, "seg" for Segment databases respectively

## Details

Note: The BTS often changes the way we can access these files. So please
be warned that this is still an experimental feature.

## Examples

``` r
if (FALSE) { # \dontrun{

download_t100_int(2010, "mkt")

} # }
```
