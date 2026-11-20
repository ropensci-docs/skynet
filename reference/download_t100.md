# Download Data from T100 files

Downloads data from BTS/RITA/Transtats and imports it into R

## Usage

``` r
download_t100(y = NULL, type = NULL)
```

## Arguments

- y:

  year to be imported

- type:

  "mkt" for Market, "seg" for Segment databases respectively

## Value

Called mainly for its side effect: the T-100 data frame, with one row
per route and carrier (see
[`import_t100`](https://docs.ropensci.org/skynet/reference/import_t100.md)),
is assigned to the global environment as `T100_year_mkt` or
`T100_year_seg` (e.g. `T100_2010_mkt`) and returned invisibly.

## Details

Note: The BTS often changes the way we can access these files. So please
be warned that this is still an experimental feature.

## Examples

``` r
# \donttest{
# Downloads a large file from the BTS website
if(interactive()){
download_t100(2010, "mkt")
}
# }
```
