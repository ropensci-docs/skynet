# Import Data

Imports data from BTS/RITA/Transtats website File order doesn't matter,
but it is recommended to name the files using the following syntax:
*"Coupon YearQuarter.csv", "Ticket YearQuarter.csv", "T100 Year".* Note:
We do recommend sparklyr to be used for larger sets of data.

## Usage

``` r
netImport(x = NULL, y = NULL)
```

## Arguments

- x:

  First csv file to be imported, in case of DB1B database, or in case of
  using the T-100 database, the only file to be included.

- y:

  Second csv file to be imported.

## Examples

``` r
if (FALSE) { # \dontrun{

netImport(skynet_example("Coupon_2001Q1.csv"), skynet_example("Ticket_2001Q1.csv"))

} # }
```
