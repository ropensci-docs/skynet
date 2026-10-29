# Import on-time Data

Imports on-time Data directly from BTS/RITA/Transtats website raw data
(prezipped file), for SKYNET's import function.

## Usage

``` r
import_ontime(x, auto = TRUE)
```

## Arguments

- x:

  On-time csv (from zipped file)

- auto:

  Automatically assigns object

## Details

Files can be found here
<https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FGJ>. More
information on variables to select and type of files to use can be found
[here](https://github.com/ropensci/skynet)

## Examples

``` r
if (FALSE) { # \dontrun{

import_ontime(skynet_example("Ontime_2011_1.csv"))

} # }
```
