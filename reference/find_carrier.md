# Find Carrier function

Searches for airport information based on its IATA code or city name

## Usage

``` r
find_carrier(x)
```

## Arguments

- x:

  Carrier

## Value

A data frame with the carriers whose code or name matches `x`:
`op_carrier` (carrier code), `carrier_name`, and `from` and `to`, the
years in which the code was used by that carrier.

## Examples

``` r
find_carrier("United")
#>    op_carrier                            carrier_name  from    to
#>        <fctr>                                  <fctr> <num> <int>
#> 1:         5X                   United Parcel Service  1988    NA
#> 2:         G7 GoJet Airlines LLC d/b/a United Express  2005    NA
#> 3:         UA                   United Air Lines Inc.  1960    NA
#> 4:        XBE                   United Parcel Service  1981  1988

find_carrier("UA")
#>     op_carrier                                carrier_name  from    to
#>         <fctr>                                      <fctr> <num> <int>
#>  1:         3U                    Sichuan Airlines Co Ltd.  2011    NA
#>  2:        BDQ    Aerotaxis De Aguascalientes S.A. De C.V.  2005    NA
#>  3:        CHA                    Chautauqua Airlines Inc.  1960  2004
#>  4:        EOQ                  Aeroservicios Ecuatorianos  1982  1997
#>  5:         EQ         Tame Linea Aerea del Ecuador Tme EP  2013    NA
#>  6:         EU                 Empresa Ecuatoriana De Avia  1981  1993
#>  7:         EU                     Ecuatoriana De Aviacion  1996  2000
#>  8:         H7 Venture Travel LLC d/b/a Taquan Air Service  2003  2004
#>  9:         K3 Venture Travel LLC d/b/a Taquan Air Service  2004    NA
#> 10:        MUA                        Manu'a Air Transport  1982  2002
#> 11:         NJ                      Vanguard Airlines Inc.  1994  2002
#> 12:         OG                              Air Guadeloupe  1991  1993
#> 13:        OMQ                           Quassar De Mexico  1993  1995
#> 14:        PDQ                    Antigua Paradise Airways  1994  1997
#> 15:         PU  Primeras Lineas Uruguays For International  1990  1991
#> 16:         PZ                    Lineas Aereas Paraguayas  1981  1995
#> 17:        ROQ                                Aero Uruguay  1981  1989
#> 18:         RP                    Chautauqua Airlines Inc.  2004  2014
#> 19:        SJA                      San Juan Airlines Inc.  1960  2002
#> 20:        SUA                           Sunshine Airlines  1995  2002
#> 21:        TAQ                          Taquan Air Service  1988  1999
#> 22:        TGQ                 Tranps Aereos Guatemaltecos  1992  1994
#> 23:        TQA Venture Travel LLC d/b/a Taquan Air Service  2000  2003
#> 24:         TX                 Soc.Nouvelle Air Guadeloupe  1998  2001
#> 25:         UA                       United Air Lines Inc.  1960    NA
#> 26:        UAI                      Universal Airways Inc.  1960  2002
#> 27:        URQ                                Aero Uruguay  1992  2001
#> 28:        UYQ                   Aerolineas Uruguayas S.A.  1993  2002
#> 29:         XL                                 Lan Ecuador  2003    NA
#>     op_carrier                                carrier_name  from    to
#>         <fctr>                                      <fctr> <num> <int>
```
