# Path and OD Network

Generates an OD network and a Leg Count data frame(on demand)

## Usage

``` r
make_net_path(x, leg = FALSE, zero = FALSE, carrier = FALSE)
```

## Arguments

- x:

  Data frame

- leg:

  Generates Leg Count Data frame, based on Path taken.

- zero:

  Displays percentage of 0 usd tickets

- carrier:

  Groups data per airline

  For example, all passengers doing the BOS-ATL-LAX path, are summed by
  Air Carrier.

## Value

With `leg = FALSE`, a data frame (data.table) with one row per origin
and destination pair: passengers, average fare and its standard
deviation, yield, mean number of stops, mean distance, city information,
year and quarter (plus the percentage of 0 usd tickets with
`zero = TRUE`). With `leg = TRUE`, an object of class `skynet`: a list
with `netOD`, the data frame above, and `netLegCount`, a data frame
(data.table) with the passengers per `path` taken, its carriers and its
number of legs (`legCount`).

## Examples

``` r
make_net_path(OD_Sample)
#> This code might take longer than usual to execute
#>       origin   dest passengers fare_sd itin_fare itin_yield mean_stops
#>       <char> <char>      <int>   <num>     <num>      <num>      <num>
#>    1:    ABE    IAD          1    0.00    271.00      1.694          1
#>    2:    ABI    DFW          1    0.00    364.50      0.224          1
#>    3:    ABQ    ATL          1    0.00      5.00      0.002          1
#>    4:    ABQ    BWI          1    0.00    124.50      0.047          1
#>    5:    ABQ    DFW          4   25.75    178.67      0.170          1
#>   ---                                                                 
#> 2178:    VPS    IAH          1    0.00    172.00      0.135          1
#> 2179:    XNA    DEN          1    0.00    175.00      0.126          1
#> 2180:    XNA    DFW          2    0.00      5.00      0.005          1
#> 2181:    XNA    ORD          1    0.00    112.50      0.100          1
#> 2182:    YUM    PHX          2   33.59    303.75      0.140          1
#>       mean_distance origin_city_mkt_id                    origin_city
#>               <num>              <int>                         <char>
#>    1:           160              30135 Allentown/Bethlehem/Easton, PA
#>    2:           158              30136                    Abilene, TX
#>    3:          1269              30140                Albuquerque, NM
#>    4:          1670              30140                Albuquerque, NM
#>    5:           569              30140                Albuquerque, NM
#>   ---                                                                
#> 2178:           528              31504                 Valparaiso, FL
#> 2179:           616              31834               Fayetteville, AR
#> 2180:           281              31834               Fayetteville, AR
#> 2181:           522              31834               Fayetteville, AR
#> 2182:           160              33785                       Yuma, AZ
#>       dest_city_mkt_id                          dest_city  year quarter
#>                  <int>                             <char> <int>   <int>
#>    1:            30852 Washington, DC (Metropolitan Area)  2011       1
#>    2:            30194              Dallas/Fort Worth, TX  2011       1
#>    3:            30397    Atlanta, GA (Metropolitan Area)  2011       1
#>    4:            30852 Washington, DC (Metropolitan Area)  2011       1
#>    5:            30194              Dallas/Fort Worth, TX  2011       1
#>   ---                                                                  
#> 2178:            31453                        Houston, TX  2011       1
#> 2179:            30325                         Denver, CO  2011       1
#> 2180:            30194              Dallas/Fort Worth, TX  2011       1
#> 2181:            30977                        Chicago, IL  2011       1
#> 2182:            30466                        Phoenix, AZ  2011       1

# Generate Leg Count
make_net_path(OD_Sample, leg = TRUE)
#> This code might take longer than usual to execute
#> $netOD
#>       origin   dest passengers fare_sd itin_fare itin_yield mean_stops
#>       <char> <char>      <int>   <num>     <num>      <num>      <num>
#>    1:    ABE    IAD          1    0.00    271.00      1.694          1
#>    2:    ABI    DFW          1    0.00    364.50      0.224          1
#>    3:    ABQ    ATL          1    0.00      5.00      0.002          1
#>    4:    ABQ    BWI          1    0.00    124.50      0.047          1
#>    5:    ABQ    DFW          4   25.75    178.67      0.170          1
#>   ---                                                                 
#> 2178:    VPS    IAH          1    0.00    172.00      0.135          1
#> 2179:    XNA    DEN          1    0.00    175.00      0.126          1
#> 2180:    XNA    DFW          2    0.00      5.00      0.005          1
#> 2181:    XNA    ORD          1    0.00    112.50      0.100          1
#> 2182:    YUM    PHX          2   33.59    303.75      0.140          1
#>       mean_distance origin_city_mkt_id                    origin_city
#>               <num>              <int>                         <char>
#>    1:           160              30135 Allentown/Bethlehem/Easton, PA
#>    2:           158              30136                    Abilene, TX
#>    3:          1269              30140                Albuquerque, NM
#>    4:          1670              30140                Albuquerque, NM
#>    5:           569              30140                Albuquerque, NM
#>   ---                                                                
#> 2178:           528              31504                 Valparaiso, FL
#> 2179:           616              31834               Fayetteville, AR
#> 2180:           281              31834               Fayetteville, AR
#> 2181:           522              31834               Fayetteville, AR
#> 2182:           160              33785                       Yuma, AZ
#>       dest_city_mkt_id                          dest_city  year quarter
#>                  <int>                             <char> <int>   <int>
#>    1:            30852 Washington, DC (Metropolitan Area)  2011       1
#>    2:            30194              Dallas/Fort Worth, TX  2011       1
#>    3:            30397    Atlanta, GA (Metropolitan Area)  2011       1
#>    4:            30852 Washington, DC (Metropolitan Area)  2011       1
#>    5:            30194              Dallas/Fort Worth, TX  2011       1
#>   ---                                                                  
#> 2178:            31453                        Houston, TX  2011       1
#> 2179:            30325                         Denver, CO  2011       1
#> 2180:            30194              Dallas/Fort Worth, TX  2011       1
#> 2181:            30977                        Chicago, IL  2011       1
#> 2182:            30466                        Phoenix, AZ  2011       1
#> 
#> $netLegCount
#>       origin   dest    path op_carrier carrier_list passengers legCount
#>       <char> <char>  <char>     <char>       <char>      <int>    <num>
#>    1:    CLT    SFO CLT SFO         US           US          2        1
#>    2:    CLT    AVL CLT AVL         16           16          2        1
#>    3:    PHX    FAT PHX FAT         YV           YV          2        1
#>    4:    CLT    BTR CLT BTR         16           16          1        1
#>    5:    CLT    BUF CLT BUF         16           16          1        1
#>   ---                                                                  
#> 2745:    LGA    RDU LGA RDU         ZW           ZW          1        1
#> 2746:    RIC    LGA RIC LGA         ZW           ZW          1        1
#> 2747:    CLT    ROC CLT ROC         16           16          1        1
#> 2748:    ROC    PHL ROC PHL         ZW           ZW          2        1
#> 2749:    PHL    SWF PHL SWF         17           17          1        1
#> 
#> attr(,"class")
#> [1] "skynet"
```
