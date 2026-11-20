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

## Value

A data frame (data.table) with one row per flight: origin and
destination airports and city market ids, date, carrier, tail and flight
numbers, scheduled and actual departure and arrival times, delays (by
cause), taxi and air times, cancellations, diversions and distance. With
`auto = TRUE` it is assigned to the global environment as
`ontime_year_month` (e.g. `ontime_2011_1`) and returned invisibly,
otherwise it is returned.

## Details

Files can be found here
<https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FGJ>. More
information on variables to select and type of files to use can be found
[here](https://github.com/ropensci/skynet)

## Examples

``` r
import_ontime(skynet_example("Ontime_2011_1.csv"), auto = FALSE)
#>     origin   dest  year month flightdate tail_number flight_number op_carrier
#>     <char> <char> <int> <int>     <IDat>      <char>         <int>     <char>
#>  1:    GEG    PDX  2011     1 2011-01-14      N483WN           888         WN
#>  2:    ORD    MSP  2011     1 2011-01-24      N0EGMQ          3748         MQ
#>  3:    ATL    DEN  2011     1 2011-01-03      N174AT           309         FL
#>  4:    PHX    SJC  2011     1 2011-01-11      N817AW           281         US
#>  5:    ORD    EWR  2011     1 2011-01-28      N9EAMQ          3736         MQ
#>  6:    RDU    DEN  2011     1 2011-01-16      N403WN           659         WN
#>  7:    SNA    EWR  2011     1 2011-01-12      N21723          1686         CO
#>  8:    PHX    SEA  2011     1 2011-01-16      N234WN          2644         WN
#>  9:    ATL    MLB  2011     1 2011-01-16      N719EV          5082         EV
#> 10:    PVD    ATL  2011     1 2011-01-23      N906DL          1952         DL
#> 11:    SNA    DFW  2011     1 2011-01-24      N3GFAA          2256         AA
#> 12:    PHX    JFK  2011     1 2011-01-23      N621JB           180         B6
#> 13:    ATL    PHF  2011     1 2011-01-07      N907DE          1204         DL
#> 14:    ITO    HNL  2011     1 2011-01-30      N485HA           201         HA
#> 15:    PHX    SBA  2011     1 2011-01-25      N7291Z          2926         YV
#> 16:    ATL    CAK  2011     1 2011-01-17      N924EV          5598         EV
#> 17:    ORD    MKE  2011     1 2011-01-14      N593ML          7012         OO
#> 18:    IAH    MSY  2011     1 2011-01-03      N33286           323         CO
#> 19:    MCO    ALB  2011     1 2011-01-15      N660SW          3185         WN
#> 20:    LAS    LAX  2011     1 2011-01-18      N4XRAA           776         AA
#> 21:    OGG    HNL  2011     1 2011-01-26      N489HA           155         HA
#> 22:    MCO    ATL  2011     1 2011-01-30      N954AT           808         FL
#> 23:    SFO    LAX  2011     1 2011-01-26      N658SW          1321         WN
#> 24:    SAV    IAD  2011     1 2011-01-24      N877AS          7147         EV
#> 25:    LGA    MDW  2011     1 2011-01-13      N494WN          1194         WN
#> 26:    GEG    MSP  2011     1 2011-01-06      N302NB          1864         DL
#> 27:    SLC    SEA  2011     1 2011-01-14       N3752          2157         DL
#> 28:    TPA    FLL  2011     1 2011-01-18      N905WN          3200         WN
#> 29:    MCO    MIA  2011     1 2011-01-04      N5ELAA          1873         AA
#> 30:    DTW    MEM  2011     1 2011-01-15      N344NB           486         DL
#> 31:    DAL    AUS  2011     1 2011-01-10      N930WN           799         WN
#> 32:    STL    ORD  2011     1 2011-01-11      N537AA          1982         AA
#> 33:    PHL    ORD  2011     1 2011-01-05      N107US           707         US
#> 34:    DCA    MIA  2011     1 2011-01-18      N324NB          1564         DL
#> 35:    TPA    DTW  2011     1 2011-01-28      N976DL          1892         DL
#> 36:    MCI    IAH  2011     1 2011-01-21      N706SK          1130         OO
#> 37:    HNL    LIH  2011     1 2011-01-29      N490HA           313         HA
#> 38:    LAX    TUS  2011     1 2011-01-16      N941SW          6487         OO
#> 39:    JFK    LAS  2011     1 2011-01-12      N613DL           187         DL
#> 40:    ORD    EVV  2011     1 2011-01-10      N806MQ          4336         MQ
#> 41:    SAN    OAK  2011     1 2011-01-26      N235WN           615         WN
#> 42:    ATL    PHX  2011     1 2011-01-15      N344AT           540         FL
#> 43:    GEG    PDX  2011     1 2011-01-18      N242WN           761         WN
#> 44:    LAX    JFK  2011     1 2011-01-21      N335AA            32         AA
#> 45:    PHX    SMF  2011     1 2011-01-14      N362SW           455         WN
#> 46:    SLC    DEN  2011     1 2011-01-24      N805SK          4590         OO
#> 47:    LAS    CVG  2011     1 2011-01-07      N345NW          2344         DL
#> 48:    BDL    ORD  2011     1 2011-01-15      N933MQ          4372         MQ
#> 49:    DEN    BIS  2011     1 2011-01-30      N952SW          6896         OO
#> 50:    PHX    FLL  2011     1 2011-01-04      N652AW           184         US
#>     origin   dest  year month flightdate tail_number flight_number op_carrier
#>     <char> <char> <int> <int>     <IDat>      <char>         <int>     <char>
#>     origin_mkt_id dest_mkt_id sch_dep dep_time dep_delay taxi_out taxi_in
#>             <int>       <int>   <int>    <int>     <int>    <int>   <int>
#>  1:         31884       34057    1150     1148        -2       17       4
#>  2:         30977       31650     600      645        45       66       4
#>  3:         30397       30325    2220     2217        -3       12      10
#>  4:         30466       32457    1435     1434        -1       12       4
#>  5:         30977       31703     600      601         1       16       8
#>  6:         34492       30325     905      904        -1        6       5
#>  7:         32575       31703    2125     2126         1       17       7
#>  8:         30466       30559    1500     1552        52        6       5
#>  9:         30397       33360    1614     1631        17       29       3
#> 10:         30721       30397    1251     1247        -4       13      12
#> 11:         32575       30194    1320     1315        -5        8      15
#> 12:         30466       31703    2320     2322         2        8       6
#> 13:         30397       33667    1635     1630        -5       30       8
#> 14:         32402       32134     713      707        -6        8       6
#> 15:         30466       34689     830      834         4       14       4
#> 16:         30397       30647    1758     1752        -6       21       9
#> 17:         30977       33342    1658     1754        56       20       5
#> 18:         31453       33495    1315     1323         8       12       3
#> 19:         31454       30257    1140     1136        -4        9       3
#> 20:         32211       32575    1850     1841        -9       29       8
#> 21:         33830       32134     839      832        -7        6       5
#> 22:         31454       30397    1645     1644        -1       17      11
#> 23:         32457       32575    1125     1123        -2       12       6
#> 24:         34685       30852    1004     1221       137        7       4
#> 25:         31703       30977    1925     1930         5       51       7
#> 26:         31884       31650     720      720         0       15       8
#> 27:         34614       30559    1105     1106         1       17      16
#> 28:         33195       32467     820      818        -2       11       5
#> 29:         31454       32467    2020     2017        -3       13       5
#> 30:         31295       33244     710      706        -4       32       6
#> 31:         30194       30423    1020     1022         2       12       3
#> 32:         31123       30977    1835       NA        NA       NA      NA
#> 33:         34100       30977    1755     1754        -1       21       9
#> 34:         30852       32467    1535     1608        33       20      10
#> 35:         33195       31295    1143       NA        NA       NA      NA
#> 36:         33198       31453    1805     1805         0       21      14
#> 37:         32134       32982    1731     1730        -1       14       7
#> 38:         32575       30436    1153     1149        -4       23       5
#> 39:         31703       32211    1800       NA        NA       NA      NA
#> 40:         30977       31612     850      846        -4       13       1
#> 41:         33570       32457    1030     1027        -3       10       5
#> 42:         30397       30466    1040     1038        -2       19       3
#> 43:         31884       34057    1000      957        -3        7       3
#> 44:         32575       31703    1345     1442        57       27       5
#> 45:         30466       33192    2040     2039        -1       10       4
#> 46:         34614       30325     830      841        11       18       7
#> 47:         32211       33105      10        5        -5       11       8
#> 48:         30529       30977     710      724        14       19      11
#> 49:         30325       30627    1606     1629        23       14       6
#> 50:         30466       32467    1615     1609        -6       16       4
#>     origin_mkt_id dest_mkt_id sch_dep dep_time dep_delay taxi_out taxi_in
#>             <int>       <int>   <int>    <int>     <int>    <int>   <int>
#>     sch_arr arr_time arr_delay cancelled diverted airtime distance
#>       <int>    <int>     <int>     <int>    <int>   <int>    <int>
#>  1:    1255     1306        11         0        0      57      279
#>  2:     725      908       103         0        0      73      334
#>  3:    2355     2343       -12         0        0     184     1199
#>  4:    1530     1527        -3         0        0      97      622
#>  5:     900      859        -1         0        0      94      719
#>  6:    1120     1046       -34         0        0     211     1437
#>  7:     511      542        31         0        0     292     2433
#>  8:    1705     1802        57         0        0     179     1107
#>  9:    1742     1806        24         0        0      63      443
#> 10:    1545     1544        -1         0        0     152      903
#> 11:    1810     1805        -5         0        0     147     1205
#> 12:     558      542       -16         0        0     246     2153
#> 13:    1811     1815         4         0        0      67      508
#> 14:     802      758        -4         0        0      37      216
#> 15:     906      901        -5         0        0      69      455
#> 16:    1944     1935        -9         0        0      73      528
#> 17:    1739     1840        61         0        0      21       67
#> 18:    1423     1419        -4         0        0      41      305
#> 19:    1425     1412       -13         0        0     144     1073
#> 20:    2000     1959        -1         0        0      41      236
#> 21:     913      905        -8         0        0      22      100
#> 22:    1820     1818        -2         0        0      66      403
#> 23:    1245     1235       -10         0        0      54      337
#> 24:    1141     1349       128         0        0      77      515
#> 25:    2105     2134        29         0        0     126      725
#> 26:    1218     1159       -19         0        0     136     1175
#> 27:    1220     1234        14         0        0     115      689
#> 28:     920      920         0         0        0      46      197
#> 29:    2125     2115       -10         0        0      40      193
#> 30:     830      816       -14         0        0      92      610
#> 31:    1110     1110         0         0        0      33      189
#> 32:    1955       NA        NA         1        0      NA      258
#> 33:    1921     1910       -11         0        0     106      678
#> 34:    1813     1901        48         0        0     143      920
#> 35:    1430       NA        NA         1        0      NA      983
#> 36:    2009     2014         5         0        0      94      643
#> 37:    1808     1813         5         0        0      22      102
#> 38:    1417     1420         3         0        0      63      451
#> 39:    2103       NA        NA         1        0      NA     2248
#> 40:    1000      949       -11         0        0      49      273
#> 41:    1200     1149       -11         0        0      67      446
#> 42:    1305     1229       -36         0        0     209     1587
#> 43:    1110     1057       -13         0        0      50      279
#> 44:    2205     2304        59         0        0     290     2475
#> 45:    2145     2132       -13         0        0      99      647
#> 46:     958     1006         8         0        0      60      390
#> 47:     642      636        -6         0        0     192     1678
#> 48:     900      917        17         0        0     143      783
#> 49:    1839     1856        17         0        0      67      517
#> 50:    2220     2204       -16         0        0     215     1972
#>     sch_arr arr_time arr_delay cancelled diverted airtime distance
#>       <int>    <int>     <int>     <int>    <int>   <int>    <int>
#>     carrier_delay weather_delay nas_delay security_delay
#>             <int>         <int>     <int>          <int>
#>  1:            NA            NA        NA             NA
#>  2:            45             0        58              0
#>  3:            NA            NA        NA             NA
#>  4:            NA            NA        NA             NA
#>  5:            NA            NA        NA             NA
#>  6:            NA            NA        NA             NA
#>  7:             0             0        31              0
#>  8:            49             0         5              0
#>  9:            17             0         7              0
#> 10:            NA            NA        NA             NA
#> 11:            NA            NA        NA             NA
#> 12:            NA            NA        NA             NA
#> 13:            NA            NA        NA             NA
#> 14:            NA            NA        NA             NA
#> 15:            NA            NA        NA             NA
#> 16:            NA            NA        NA             NA
#> 17:            44             0         5              0
#> 18:            NA            NA        NA             NA
#> 19:            NA            NA        NA             NA
#> 20:            NA            NA        NA             NA
#> 21:            NA            NA        NA             NA
#> 22:            NA            NA        NA             NA
#> 23:            NA            NA        NA             NA
#> 24:           128             0         0              0
#> 25:             0             0        29              0
#> 26:            NA            NA        NA             NA
#> 27:            NA            NA        NA             NA
#> 28:            NA            NA        NA             NA
#> 29:            NA            NA        NA             NA
#> 30:            NA            NA        NA             NA
#> 31:            NA            NA        NA             NA
#> 32:            NA            NA        NA             NA
#> 33:            NA            NA        NA             NA
#> 34:             0             0        15              0
#> 35:            NA            NA        NA             NA
#> 36:            NA            NA        NA             NA
#> 37:            NA            NA        NA             NA
#> 38:            NA            NA        NA             NA
#> 39:            NA            NA        NA             NA
#> 40:            NA            NA        NA             NA
#> 41:            NA            NA        NA             NA
#> 42:            NA            NA        NA             NA
#> 43:            NA            NA        NA             NA
#> 44:             0             0         2              0
#> 45:            NA            NA        NA             NA
#> 46:            NA            NA        NA             NA
#> 47:            NA            NA        NA             NA
#> 48:             0            14         3              0
#> 49:             0             0         0              0
#> 50:            NA            NA        NA             NA
#>     carrier_delay weather_delay nas_delay security_delay
#>             <int>         <int>     <int>          <int>
```
