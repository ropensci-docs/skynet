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

## Details

Coupon files can be found at
<https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FLM>. Ticket files
can be found at <https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FKF>.

Note: The BTS often changes the way we can access these files. So please
be warned that this is still an experimental feature.

## Examples

``` r
if (FALSE) { # \dontrun{

download_db1b(2010, 1)

} # }
```
