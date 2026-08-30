# Import Data from DB1B files

Imports data from BTS/RITA/Transtats files

## Usage

``` r
import_db1b(c, t, zip = FALSE, auto = TRUE)
```

## Arguments

- c:

  Coupon csv file to be imported, in case of DB1B database

- t:

  Ticket csv file to be imported, in case of DB1B database

- zip:

  Should equal TRUE if original file comes from the BTS prezipped
  option.

- auto:

  Automatically assigns object

## Details

Coupon files can be found at
<https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FLM>. Ticket files
can be found at <https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FKF>.
Both files should belong to the same year and same quarter. **Note**: We
do recommend sparklyr to be used for larger sets of data. More
information on variables to select and type of files to use can be found
[here](https://github.com/ropensci/skynet)

## Examples

``` r
if (FALSE) { # \dontrun{

import_db1b(skynet_example("Coupon_2001Q1.csv"), skynet_example("Ticket_2001Q1.csv"))

} # }
```
