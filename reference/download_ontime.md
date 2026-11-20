# Download On-Time

Download On-Time Performance Data directly from BTS/RITA/Transtats
website raw data (prezipped file), for SKYNET's import function.

## Usage

``` r
download_ontime(y, m, auto = TRUE)
```

## Arguments

- y:

  year to be imported

- m:

  month to be imported

- auto:

  Automatically assigns object

## Value

A data frame with one row per flight (see
[`import_ontime`](https://docs.ropensci.org/skynet/reference/import_ontime.md)).
With `auto = TRUE` it is assigned to the global environment as
`ontime_year_month` (e.g. `ontime_2011_1`) and returned invisibly,
otherwise it is returned. If the BTS website can't be reached a message
is shown and `NULL` is returned.

## Examples

``` r
# \donttest{
# Downloads a large file from the BTS website
if(interactive()){
download_ontime(2011, 1, auto = FALSE)
}
# }
```
