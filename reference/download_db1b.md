# Download Data from DB1B files

Downloads data from BTS/RITA/Transtats and imports it into R

## Usage

``` r
download_db1b(y = NULL, q = NULL)
```

## Arguments

- y:

  year to be imported

- q:

  quarter to be imported

## Value

Called mainly for its side effect: the merged coupon and ticket data
frame, with one row per coupon (see
[`import_db1b`](https://docs.ropensci.org/skynet/reference/import_db1b.md)),
is assigned to the global environment as `OD_yearQquarter` (e.g.
`OD_2010Q1`) and returned invisibly. If the BTS website can't be reached
a message is shown and `NULL` is returned.

## Details

Coupon files can be found at
<https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FLM>. Ticket files
can be found at <https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FKF>.

Note: The BTS often changes the way we can access these files. So please
be warned that this is still an experimental feature.

## Examples

``` r
# \donttest{
# Downloads a large file from the BTS website
if(interactive()){
download_db1b(2010, 1)
}
# }
```
