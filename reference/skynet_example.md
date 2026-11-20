# Get path to skynet examples

To access csv examples from SKYNET

## Usage

``` r
skynet_example(path = NULL)
```

## Arguments

- path:

  File name.

## Value

A character vector with the names of the example files when `path` is
`NULL`, otherwise the full path to the requested file.

## Examples

``` r
skynet_example()
#> [1] "Coupon_2001Q1.csv"                                  
#> [2] "Ontime_2011_1.csv"                                  
#> [3] "Origin_and_Destination_Survey_DB1BCoupon_2001_1.csv"
#> [4] "Origin_and_Destination_Survey_DB1BTicket_2001_1.csv"
#> [5] "T100_2011_int.csv"                                  
#> [6] "T100_2011_mkt.csv"                                  
#> [7] "Ticket_2001Q1.csv"                                  
skynet_example("Coupon_2001Q1.csv")
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/skynet/extdata/Coupon_2001Q1.csv"
```
