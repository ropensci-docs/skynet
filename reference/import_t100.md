# Import T-100 Data

Imports T-100 Data directly from BTS/RITA/Transtats website raw data
(prezipped file), for SKYNET's import function.

## Usage

``` r
import_t100(x, nonsch = FALSE, auto = TRUE)
```

## Arguments

- x:

  T-100 csv

- nonsch:

  Should equal TRUE to include non-scheduled flights

- auto:

  Automatically assigns object

## Details

Files can be found here
<https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FIL>. More
information on variables to select and type of files to use can be found
[here](https://github.com/ropensci/skynet)

## Examples

``` r
if (FALSE) { # \dontrun{

import_t100(skynet_example("T100_2011_mkt.csv"))

} # }
```
