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

## Value

A data frame with one row per route, carrier and month: origin and
destination airports and city market ids, carrier, distance, passengers,
year, quarter and month (plus seats, departures and aircraft type for
segment files). With `auto = TRUE` it is assigned to the global
environment as `T100_year_mkt` or `T100_year_seg` (e.g. `T100_2011_mkt`)
and returned invisibly, otherwise it is returned.

## Details

Files can be found here
<https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FIL>. More
information on variables to select and type of files to use can be found
[here](https://github.com/ropensci/skynet)

## Examples

``` r
import_t100(skynet_example("T100_2011_mkt.csv"), auto = FALSE)
#>    origin_mkt_id origin year quarter dest_mkt_id dest op_carrier distance
#> 1          31995    GSO 2011       1       30397  ATL         EV      306
#> 2          32211    LAS 2011       3       34252  PSC         G4      732
#> 3          33342    MKE 2011       2       30721  BOS         F9      860
#> 4          30194    DAL 2011       4       33495  MSY         WN      436
#> 5          30325    DEN 2011       2       31980  GRI         ZK      344
#> 6          31295    DTW 2011       1       30852  DCA         ZW      405
#> 7          30397    ATL 2011       2       30721  BOS         CO      946
#> 8          30198    PIT 2011       1       34570  RNO         WN     2081
#> 9          30304    ANI 2011       2       30299  ANC         KS      318
#> 10         32337    IND 2011       2       33316  OMA         WN      517
#> 11         33851    OKC 2011       1       31650  MSP         9E      695
#> 12         30529    BDL 2011       3       33495  MSY         WN     1279
#> 13         31057    CLT 2011       4       30868  CAE         OH       88
#> 14         30325    DEN 2011       1       31650  MSP         YX      680
#> 15         34262    PSP 2011       4       32457  SFO         OO      421
#> 16         31650    MSP 2011       1       34108  PIA         XJ      342
#> 17         32087    HCR 2011       2       32676  KGX         H6       50
#> 18         30466    PHX 2011       1       30721  MHT         WN     2279
#> 19         30245    AKN 2011       1       35853  WSN         KS       13
#> 20         30785    BTV 2011       1       31703  JFK         RP      267
#> 21         34689    SBA 2011       4       34570  RNO         OO      350
#> 22         30466    PHX 2011       3       32467  FLL         WN     1972
#> 23         31703    EWR 2011       1       31057  CLT         CO      529
#> 24         30599    BHM 2011       4       30325  DEN         XE     1083
#> 25         30559    SEA 2011       4       33486  MSO         QX      389
#> 26         31295    DTW 2011       1       33667  ORF         RP      529
#> 27         30529    BDL 2011       2       31057  CLT         YX      644
#> 28         30852    DCA 2011       2       30721  MHT         ZW      407
#> 29         31995    GSO 2011       2       34100  PHL         YX      365
#> 30         31650    MSP 2011       1       31898  GFK         XJ      284
#> 31         33195    TPA 2011       2       30325  DEN         F9     1506
#> 32         32575    ONT 2011       2       33195  TPA         WN     2112
#> 33         34268    PTA 2011       1       32321  ILI         V8       37
#> 34         30977    ORD 2011       3       35096  SYR         MQ      607
#> 35         31703    LGA 2011       4       34492  RDU         AX      431
#> 36         30693    BNA 2011       3       31454  MCO         WN      616
#> 37         33105    CVG 2011       1       31650  MSP     OH (1)      596
#> 38         33316    OMA 2011       2       33342  MKE         YX      426
#> 39         34986    SRQ 2011       2       31057  CLT         YV      547
#> 40         31295    DTW 2011       2       33570  SAN         WN     1956
#> 41         31123    STL 2011       1       31703  JFK         MQ      892
#> 42         30325    DEN 2011       2       33198  MCI         WN      533
#> 43         30852    BWI 2011       2       32457  SFO         US     2457
#> 44         30994    CHS 2011       4       31650  MSP         WN     1087
#> 45         30852    DCA 2011       3       31066  CMH         9E      323
#> 46         30436    TUS 2011       4       30140  ABQ         WN      321
#> 47         33195    TPA 2011       3       32457  SFO         WN     2393
#> 48         35721    WBB 2011       3       32769  KOT         H6       52
#> 49         33105    CVG 2011       4       33342  MKE         9E      318
#> 50         31057    CLT 2011       2       31135  MYR         OH      156
#> 51         30559    SEA 2011       4       32457  SFO         VX      679
#> 52         31650    MSP 2011       2       32575  SNA         WN     1522
#> 53         33495    MSY 2011       3       33570  SAN         UA     1599
#> 54         32457    OAK 2011       1       30194  DAL         WN     1468
#> 55         34100    PHL 2011       4       30977  ORD         UA      678
#> 56         31703    EWR 2011       1       34057  PDX         UA     2433
#> 57         32087    HCR 2011       1       30313  ANV         H6       34
#> 58         30397    ATL 2011       1       31453  HOU         9E      696
#> 59         33570    SAN 2011       1       33830  OGG         AS     2541
#> 60         30647    CLE 2011       2       30194  DFW         AA     1021
#> 61         30647    CLE 2011       4       35096  SYR         C5      317
#> 62         30361    ART 2011       3       30257  ALB         9K      141
#> 63         31703    JFK 2011       3       33214  SAT         DL     1587
#> 64         30977    ORD 2011       2       32575  SNA         UA     1726
#> 65         35794    WMO 2011       3       31535  ELI         H6       34
#> 66         32857    KXA 2011       2       31401  WFB         3F       31
#> 67         31646    FRD 2011       4       33968  OTS        WST       17
#> 68         30721    BOS 2011       1       30615  ELP         DL     2067
#> 69         32397    ITH 2011       3       31703  LGA         XJ      179
#> 70         30194    DAL 2011       1       32457  SJC         WN     1450
#> 71         33044    SDF 2011       4       31295  DTW         OO      306
#> 72         31703    LGA 2011       3       30189  COS         F9     1638
#> 73         30140    ABQ 2011       3       30852  DCA         AA     1650
#> 74         30194    DFW 2011       2       34842  SJT         OW      228
#> 75         31453    IAH 2011       3       33192  SMF         US     1609
#> 76         31295    DTW 2011       4       33244  MEM     OH (1)      610
#> 77         33256    MFE 2011       2       32600  LIT         AA      689
#> 78         31454    MCO 2011       1       30721  BOS         B6     1121
#> 79         31721    FNT 2011       1       31650  MSP         XJ      491
#> 80         33715    NNL 2011       1       34268  PTA         V8       24
#> 81         30194    DAL 2011       4       34614  SLC         WN      999
#> 82         31650    MSP 2011       3       30198  PIT         XJ      726
#> 83         32195    HPB 2011       3       30113  BET         GV      153
#> 84         32457    SFO 2011       3       30559  SEA         AS      679
#> 85         32087    HCR 2011       4       30313  ANV         H6       34
#>    passengers month itin_fare itin_yield roundtrip
#> 1        4735     3        NA         NA        NA
#> 2        2565     7        NA         NA        NA
#> 3        1562     5        NA         NA        NA
#> 4       16085    11        NA         NA        NA
#> 5         671     4        NA         NA        NA
#> 6        2557     3        NA         NA        NA
#> 7          15     5        NA         NA        NA
#> 8          70     3        NA         NA        NA
#> 9         125     6        NA         NA        NA
#> 10         48     4        NA         NA        NA
#> 11       2436     3        NA         NA        NA
#> 12         75     9        NA         NA        NA
#> 13       1203    10        NA         NA        NA
#> 14        561     3        NA         NA        NA
#> 15       5731    11        NA         NA        NA
#> 16        632     2        NA         NA        NA
#> 17          6     5        NA         NA        NA
#> 18       3389     2        NA         NA        NA
#> 19          3     2        NA         NA        NA
#> 20       2297     1        NA         NA        NA
#> 21          2    10        NA         NA        NA
#> 22       3478     7        NA         NA        NA
#> 23       3528     2        NA         NA        NA
#> 24        806    12        NA         NA        NA
#> 25       5497    12        NA         NA        NA
#> 26         25     3        NA         NA        NA
#> 27       1894     4        NA         NA        NA
#> 28        193     5        NA         NA        NA
#> 29       1743     6        NA         NA        NA
#> 30         86     1        NA         NA        NA
#> 31       4017     5        NA         NA        NA
#> 32         91     5        NA         NA        NA
#> 33          2     1        NA         NA        NA
#> 34       5855     8        NA         NA        NA
#> 35        843    11        NA         NA        NA
#> 36       8626     8        NA         NA        NA
#> 37       3142     2        NA         NA        NA
#> 38        743     6        NA         NA        NA
#> 39        289     6        NA         NA        NA
#> 40         89     6        NA         NA        NA
#> 41        943     3        NA         NA        NA
#> 42      13991     4        NA         NA        NA
#> 43          5     5        NA         NA        NA
#> 44         16    10        NA         NA        NA
#> 45        619     8        NA         NA        NA
#> 46       3898    10        NA         NA        NA
#> 47        294     8        NA         NA        NA
#> 48         15     9        NA         NA        NA
#> 49        131    11        NA         NA        NA
#> 50       4164     6        NA         NA        NA
#> 51      12184    10        NA         NA        NA
#> 52         15     4        NA         NA        NA
#> 53         96     9        NA         NA        NA
#> 54       2293     1        NA         NA        NA
#> 55      16143    11        NA         NA        NA
#> 56        162     2        NA         NA        NA
#> 57          8     1        NA         NA        NA
#> 58       4152     2        NA         NA        NA
#> 59       4001     1        NA         NA        NA
#> 60       8450     5        NA         NA        NA
#> 61       2273    10        NA         NA        NA
#> 62        228     9        NA         NA        NA
#> 63       2651     9        NA         NA        NA
#> 64      10929     5        NA         NA        NA
#> 65          2     7        NA         NA        NA
#> 66          5     6        NA         NA        NA
#> 67         10    11        NA         NA        NA
#> 68          6     2        NA         NA        NA
#> 69       1052     9        NA         NA        NA
#> 70        362     3        NA         NA        NA
#> 71         49    12        NA         NA        NA
#> 72        159     8        NA         NA        NA
#> 73        240     8        NA         NA        NA
#> 74       4558     5        NA         NA        NA
#> 75         99     9        NA         NA        NA
#> 76        181    12        NA         NA        NA
#> 77          1     6        NA         NA        NA
#> 78      18635     2        NA         NA        NA
#> 79         82     3        NA         NA        NA
#> 80          1     3        NA         NA        NA
#> 81         97    11        NA         NA        NA
#> 82       1532     9        NA         NA        NA
#> 83         51     7        NA         NA        NA
#> 84      25018     9        NA         NA        NA
#> 85          4    11        NA         NA        NA
```
