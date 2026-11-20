# Directed network

Generates Directed Network with an iGraph **gDir** object, a Data Frame
**netDir** and a Data Frame with Airport/Nodes statistics **nodes**.

## Usage

``` r
make_net_dir(
  x,
  disp = FALSE,
  alpha = 0.003,
  cap = FALSE,
  pct = 10,
  carrier = FALSE,
  metro = FALSE
)
```

## Arguments

- x:

  Data frame

- disp:

  Uses the Serrano's disparity filter
  (<https://en.wikipedia.org/wiki/Disparity_filter_algorithm_of_weighted_network>)
  to extract the backbone of the network.

- alpha:

  Argument for disparity filter.

- cap:

  Filters original data based on the edge weight.

- pct:

  Argument for cap filter. Value should be imput as percentage.

- carrier:

  Groups data per carrier and OD

- metro:

  Groups data by metropolitan area

## Value

An object of class `skynet`: a list with `gDir`, the igraph directed
network weighted by passengers, `netDir`, a data frame with one row per
route (origin, destination, passengers, average fare and its standard
deviation, yield, distance, year, quarter and city information), and
`nodes`, a data frame with the airport/node statistics (see
[`node_stats`](https://docs.ropensci.org/skynet/reference/node_stats.md)).
With `disp = TRUE` or `cap = TRUE` the first two elements are named
`gDir_disp` and `netDir_disp`, or `gDir_cap` and `netDir_cap`.

## Examples

``` r
make_net_dir(OD_Sample)
#> $gDir
#> IGRAPH 6989987 DNW- 251 2182 -- 
#> + attr: name (v/c), pass_dep (v/n), pass_arr (v/n), pass_tr (v/n),
#> | city_mkt_id (v/n), city (v/c), latitude (v/n), longitude (v/n),
#> | airport_city_name (v/c), airport_country_code (v/c), airport_state
#> | (v/c), airport_id (v/n), freq (v/n), weight (e/n), fare_sd (e/n),
#> | itin_fare (e/n), itin_yield (e/n), distance (e/n), year (e/n),
#> | quarter (e/n)
#> + edges from 6989987 (vertex names):
#>  [1] ABE->IAD ABI->DFW ABQ->ATL ABQ->BWI ABQ->DFW ABQ->IAH ABQ->LBB ABQ->MDW
#>  [9] ABQ->MSP ABQ->ORD ABQ->PHX ABQ->SAN ABQ->SEA ABQ->SLC ABQ->STL ABY->ATL
#> [17] ACT->DFW ACY->FLL ACY->MYR AEX->ATL AGS->ATL AGS->CLT ALB->CLT ALB->LAS
#> + ... omitted several edges
#> 
#> $netDir
#> # A tibble: 2,182 × 13
#> # Groups:   origin, dest, year [2,182]
#>    origin dest  passengers fare_sd itin_fare itin_yield distance  year quarter
#>    <chr>  <chr>      <int>   <dbl>     <dbl>      <dbl>    <dbl> <int>   <int>
#>  1 ABE    IAD            1     0      271.       1.69        160  2011       1
#>  2 ABI    DFW            1     0       35.4      0.224       158  2011       1
#>  3 ABQ    ATL            1     0        2.66     0.0021     1269  2011       1
#>  4 ABQ    BWI            1     0       78.5      0.047      1670  2011       1
#>  5 ABQ    DFW            4    12.3     96.5      0.170       569  2011       1
#>  6 ABQ    IAH            1     0      117.       0.157       744  2011       1
#>  7 ABQ    LBB            1     0       65.2      0.226       289  2011       1
#>  8 ABQ    MDW            2     0      170.       0.151      1121  2011       1
#>  9 ABQ    MSP            1     0      413.       0.422       981  2011       1
#> 10 ABQ    ORD            2     0      175.       0.156      1118  2011       1
#> # ℹ 2,172 more rows
#> # ℹ 4 more variables: origin_city_mkt_id <int>, origin_city <chr>,
#> #   dest_city_mkt_id <int>, dest_city <chr>
#> 
#> $nodes
#>     airport pass_dep pass_arr pass_tr city_mkt_id
#> 1       ABE        1        6       0       30135
#> 2       ABI        1        2       0       30136
#> 3       ABQ       22       24       4       30140
#> 4       ABY        1        0       0       30146
#> 5       ACT        1        0       0       30155
#> 6       ACV        0        1       0       30157
#> 7       ACY        2        0       0       30158
#> 8       AEX        2        0       0       30185
#> 9       AGS        3        7       0       30208
#> 10      ALB        4        6       0       30257
#> 11      AMA        6        1       0       30279
#> 12      ANC       12       10       4       30299
#> 13      ASE        4        5       1       30372
#> 14      ATL      395      321     229       30397
#> 15      ATW        5        0       0       30408
#> 16      AUG        1        0       0       30414
#> 17      AUS       27       40       4       30423
#> 18      AVL        1        5       0       30431
#> 19      AVP        3        0       0       30434
#> 20      AZO        0        1       0       30469
#> 21      BDL       34       28       1       30529
#> 22      BET        0        2       0       30113
#> 23      BGM        1        3       0       30577
#> 24      BGR        3        3       0       30581
#> 25      BHM       13       12       1       30599
#> 26      BIL        2        2       0       30620
#> 27      BIS        1        1       0       30627
#> 28      BLI        4       14       3       30666
#> 29      BMI        5        1       0       30685
#> 30      BNA       62       45      10       30693
#> 31      BOI       19        9       1       30713
#> 32      BOS      213      106       4       30721
#> 33      BQK        0        1       0       30731
#> 34      BRO        2        0       0       30747
#> 35      BTR        4        2       0       30781
#> 36      BTV        2        5       0       30785
#> 37      BUF       24       21       1       30792
#> 38      BUR       11       12       3       32575
#> 39      BWI       94       76      22       30852
#> 40      BZN        3        1       0       30849
#> 41      CAE        5        8       0       30868
#> 42      CAK       28       12       1       30647
#> 43      CEC        2        0       0       30930
#> 44      CHA        3        3       1       30980
#> 45      CHO        1        3       0       30990
#> 46      CHS       13       12       0       30994
#> 47      CIC        0        1       0       31002
#> 48      CID        1        8       0       31003
#> 49      CKB        0        1       0       31027
#> 50      CLE       19       42      14       30647
#> 51      CLT      186      170     138       31057
#> 52      CMH       20       25       1       31066
#> 53      CMX        0        1       0       31076
#> 54      COS        5        7       0       30189
#> 55      CPR        1        1       0       31122
#> 56      CRP        1        4       0       31140
#> 57      CRW        6        6       0       31146
#> 58      CSG        0        1       0       31150
#> 59      CVG       31       28       6       33105
#> 60      CWA        0        3       1       30424
#> 61      DAB        3        4       0       31252
#> 62      DAL       42       27      14       30194
#> 63      DAY       24        8       0       31267
#> 64      DCA       97      113      24       30852
#> 65      DEN      256      253     123       30325
#> 66      DFW      277      250     145       30194
#> 67      DLH        1        0       0       31337
#> 68      DSM       10       10       0       31423
#> 69      DTW      120      127      68       31295
#> 70      DVL        0        2       0       31447
#> 71      EAT        0        1       0       31470
#> 72      ECP        3        3       0       31481
#> 73      EGE        7        3       0       31503
#> 74      ELM        1        2       0       31537
#> 75      ELP       16        6       1       30615
#> 76      ERI        1        1       0       31577
#> 77      EUG        1        5       0       31603
#> 78      EWN        0        2       0       31617
#> 79      EWR       88       72      17       31703
#> 80      EYW        4        4       1       31624
#> 81      FAI        1        6       1       31517
#> 82      FAR        3        4       0       31637
#> 83      FAT        5        5       1       31638
#> 84      FAY        4        3       0       31641
#> 85      FCA        0        5       0       31648
#> 86      FLG        0        1       0       31695
#> 87      FLL       98      127       8       32467
#> 88      FLO        1        1       0       31699
#> 89      FNT        4       27       0       31721
#> 90      FSD        1        2       0       31775
#> 91      FSM        2        1       0       31778
#> 92      FWA        3        5       0       31823
#> 93      GCC        1        0       0       31865
#> 94      GEG       10       14       0       31884
#> 95      GFK        1        1       0       31898
#> 96      GJT        3        7       0       31921
#> 97      GNV        2        1       0       31953
#> 98      GPT        1        1       0       31973
#> 99      GRB        5        2       0       31977
#> 100     GRK        0        1       0       31982
#> 101     GRR       13       11       0       31986
#> 102     GSO        4        6       0       31995
#> 103     GSP        3       12       0       31871
#> 104     GTF        2        0       0       31895
#> 105     HDN        3        1       0       34699
#> 106     HLN        0        2       0       32156
#> 107     HNL       57       29      10       32134
#> 108     HOU       35       65      23       31453
#> 109     HPN       26       24       0       31703
#> 110     HRL        1        6       0       32206
#> 111     HSV        6        9       1       30255
#> 112     HYS        0        1       0       32255
#> 113     IAD       66       52      23       30852
#> 114     IAH      143      121      73       31453
#> 115     ICT        5        5       0       30928
#> 116     IDA        1        0       0       32280
#> 117     ILM        2        4       0       32323
#> 118     IND       39       41       3       32337
#> 119     ISN        1        0       0       32389
#> 120     ISP        4       21       0       31703
#> 121     ITH        3        0       0       32397
#> 122     ITO        0        3       0       32402
#> 123     JAC        0        6       0       32441
#> 124     JAN        7        4       1       32448
#> 125     JAX       25       14       0       31136
#> 126     JFK       78      267      15       31703
#> 127     JNU        2        2       0       32523
#> 128     KOA        5       13       2       32758
#> 129     LAN        7        1       0       32884
#> 130     LAS      235      137      25       32211
#> 131     LAW        0        1       0       32891
#> 132     LAX      286      136      48       32575
#> 133     LBB        6        3       0       32896
#> 134     LEX        6        3       0       32945
#> 135     LFT        2        0       0       32951
#> 136     LGA      136      106      13       31703
#> 137     LGB        7        8       3       32575
#> 138     LIH       15        9       0       32982
#> 139     LIT       11       20       0       32600
#> 140     LMT        2        0       0       33024
#> 141     LRD        2        1       0       33038
#> 142     LSE        0        4       0       33076
#> 143     LWS        1        0       0       33127
#> 144     MAF        3        2       0       33158
#> 145     MBS        4        4       0       33184
#> 146     MCI       53       34       1       33198
#> 147     MCO      200      111      12       31454
#> 148     MCW        0        1       0       33211
#> 149     MDT        9        9       0       32070
#> 150     MDW       68      109      49       30977
#> 151     MEI        1        1       0       33241
#> 152     MEM       65       36      23       33244
#> 153     MFE        6        2       0       33256
#> 154     MFR        3        1       0       33264
#> 155     MGM        0        1       0       33277
#> 156     MHT       10       41       1       30721
#> 157     MIA       91       59      20       32467
#> 158     MKE       33       56       4       33342
#> 159     MLB        1        6       0       33360
#> 160     MLI        0        1       0       33367
#> 161     MLU        2        1       0       33377
#> 162     MMH        0        2       0       33388
#> 163     MOB        1        8       0       30562
#> 164     MOD        0        1       0       33424
#> 165     MOT        1        1       0       33304
#> 166     MQT        1        3       0       33459
#> 167     MRY        3        2       1       34922
#> 168     MSN        8        7       0       33485
#> 169     MSO        1        0       0       33486
#> 170     MSP      109      176      63       31650
#> 171     MSY       63       64       2       33495
#> 172     MTJ        1        1       0       33502
#> 173     MYR        3        1       0       31135
#> 174     OAJ        3        4       0       33795
#> 175     OAK       33       28       4       32457
#> 176     OGG       17       16       2       33830
#> 177     OKC       25       20       2       33851
#> 178     OMA       23       24       1       33316
#> 179     ONT       16       20       1       32575
#> 180     ORD      213      288     106       30977
#> 181     ORF       10       14       1       33667
#> 182     OTH        2        0       0       33964
#> 183     PBI       24       16       0       34027
#> 184     PDX       42      100       6       34057
#> 185     PGV        2        3       0       34092
#> 186     PHF        3        9       0       33667
#> 187     PHL      115      119      55       34100
#> 188     PHX      201      172      68       30466
#> 189     PIA        2        1       0       34108
#> 190     PIE        8        0       0       33195
#> 191     PIH        0        2       0       34113
#> 192     PIR        1        1       0       34120
#> 193     PIT       18       39       1       30198
#> 194     PNS       11        5       0       33728
#> 195     PSC        2        1       0       34252
#> 196     PSE        4        0       0       34254
#> 197     PSP       14        7       3       34262
#> 198     PUW        1        0       0       34303
#> 199     PVD       16       12       0       30721
#> 200     PWM        4       11       0       34321
#> 201     RAP        1        1       0       34457
#> 202     RDM        1        2       1       34489
#> 203     RDU       29       45       2       34492
#> 204     RHI        2        0       0       34520
#> 205     RIC       12       14       1       34524
#> 206     RNO       21       29       3       34570
#> 207     ROA        3        1       0       34574
#> 208     ROC       11       14       0       34576
#> 209     RST        5        2       0       32547
#> 210     RSW       48       71       2       31714
#> 211     SAN       54       50       2       33570
#> 212     SAT       37       33       1       33214
#> 213     SAV        4       10       0       34685
#> 214     SBA        2        1       0       34689
#> 215     SBN        1        0       0       34696
#> 216     SBP        5        2       0       34236
#> 217     SCE        1        1       0       34711
#> 218     SDF       12        6       1       33044
#> 219     SEA      121      135      35       30559
#> 220     SFB        0        2       0       34761
#> 221     SFO      121      215      27       32457
#> 222     SGF        4        4       0       34783
#> 223     SHV        1       10       0       30476
#> 224     SIT        0        1       0       34828
#> 225     SJC       17       14       1       32457
#> 226     SJU       30       39       5       34819
#> 227     SLC      100       88      35       34614
#> 228     SMF       25       25       5       33192
#> 229     SMX        0        2       0       34905
#> 230     SNA       37       52       0       32575
#> 231     SRQ        3        5       0       34986
#> 232     STL       60       49      15       31123
#> 233     STT        6        7       0       34945
#> 234     STX        5        4       1       34992
#> 235     SWF        1        2       0       31703
#> 236     SYR        5        8       0       35096
#> 237     TBN        0        1       0       35138
#> 238     TLH        1        2       0       35249
#> 239     TOL        2        0       0       35165
#> 240     TPA       76       98       9       33195
#> 241     TRI        1        1       0       35323
#> 242     TUL       10        8       1       34653
#> 243     TUS       10       21       1       30436
#> 244     TVC        3        0       0       35380
#> 245     TVF        1        0       0       35381
#> 246     TXK        1        0       0       35401
#> 247     TYS       11        8       0       35412
#> 248     VLD        0        2       0       35550
#> 249     VPS        2        5       0       31504
#> 250     XNA        4        4       1       31834
#> 251     YUM        2        1       0       33785
#>                                      city latitude  longitude
#> 1          Allentown/Bethlehem/Easton, PA 40.65472  -75.43833
#> 2                             Abilene, TX 32.40944  -99.67972
#> 3                         Albuquerque, NM 35.04167 -106.60639
#> 4                              Albany, GA 31.53222  -84.19611
#> 5                                Waco, TX 31.61139  -97.22861
#> 6                       Eureka/Arcata, CA 40.97917 -124.10750
#> 7                       Atlantic City, NJ 39.45611  -74.57806
#> 8                          Alexandria, LA 31.32417  -92.54694
#> 9                             Augusta, GA 33.36917  -81.96444
#> 10                             Albany, NY 42.74583  -73.80528
#> 11                           Amarillo, TX 35.22722 -101.72194
#> 12                          Anchorage, AK 61.16917 -149.98528
#> 13                              Aspen, CO 39.22417 -106.86889
#> 14        Atlanta, GA (Metropolitan Area) 33.64083  -84.42722
#> 15                           Appleton, WI 44.25778  -88.52000
#> 16                 Augusta/Waterville, ME 44.31806  -69.79667
#> 17                             Austin, TX 30.19444  -97.67000
#> 18                          Asheville, NC 35.43500  -82.54111
#> 19              Scranton/Wilkes-Barre, PA 41.33917  -75.72583
#> 20                          Kalamazoo, MI 42.23639  -85.55361
#> 21                           Hartford, CT 41.93861  -72.68333
#> 22                             Bethel, AK 60.78444 -161.83139
#> 23                         Binghamton, NY 42.20139  -75.96917
#> 24                             Bangor, ME 44.80778  -68.82778
#> 25                         Birmingham, AL 33.56306  -86.75556
#> 26                           Billings, MT 45.80694 -108.54278
#> 27                    Bismarck/Mandan, ND 46.77889 -100.75250
#> 28                         Bellingham, WA 48.79444 -122.53472
#> 29                 Bloomington/Normal, IL 40.48194  -88.92750
#> 30                          Nashville, TN 36.12667  -86.68194
#> 31                              Boise, ID 43.56528 -116.22500
#> 32         Boston, MA (Metropolitan Area) 42.36361  -71.00611
#> 33                          Brunswick, GA 31.25889  -81.46639
#> 34                        Brownsville, TX 25.90639  -97.42556
#> 35                        Baton Rouge, LA 30.53167  -91.15056
#> 36                         Burlington, VT 44.47278  -73.15306
#> 37                            Buffalo, NY 42.94111  -78.73639
#> 38    Los Angeles, CA (Metropolitan Area) 34.20000 -118.35778
#> 39     Washington, DC (Metropolitan Area) 39.17500  -76.67000
#> 40                            Bozeman, MT 45.78028 -111.15944
#> 41                           Columbia, SC 33.93639  -81.11583
#> 42      Cleveland, OH (Metropolitan Area) 40.91389  -81.44167
#> 43                      Crescent City, CA 41.78000 -124.23583
#> 44                        Chattanooga, TN 35.03639  -85.20361
#> 45                    Charlottesville, VA 38.14139  -78.45306
#> 46                         Charleston, SC 32.89917  -80.03889
#> 47                              Chico, CA 39.79583 -121.85667
#> 48             Cedar Rapids/Iowa City, IA 41.88444  -91.70611
#> 49                Clarksburg/Fairmont, WV 39.29556  -80.22944
#> 50      Cleveland, OH (Metropolitan Area) 41.41083  -81.84944
#> 51                          Charlotte, NC 35.21917  -80.93583
#> 52                           Columbus, OH 39.99111  -82.87833
#> 53                   Hancock/Houghton, MI 47.16778  -88.48639
#> 54                   Colorado Springs, CO 38.80889 -104.70917
#> 55                             Casper, WY 42.90861 -106.46250
#> 56                     Corpus Christi, TX 27.77000  -97.50083
#> 57                  Charleston/Dunbar, WV 38.37278  -81.59306
#> 58                           Columbus, GA 32.51611  -84.93889
#> 59                         Cincinnati, OH 39.04778  -84.66861
#> 60       Wausau/Mosinee/Stevens Point, WI 44.78222  -89.65917
#> 61                      Daytona Beach, FL 29.18250  -81.05278
#> 62                  Dallas/Fort Worth, TX 32.84694  -96.85333
#> 63                             Dayton, OH 39.90111  -84.22000
#> 64     Washington, DC (Metropolitan Area) 38.85167  -77.03694
#> 65                             Denver, CO 39.77444 -104.87972
#> 66                  Dallas/Fort Worth, TX 32.89444  -97.02972
#> 67                             Duluth, MN 46.84250  -92.19028
#> 68                         Des Moines, IA 41.53389  -93.65667
#> 69                            Detroit, MI 42.21667  -83.34444
#> 70                        Devils Lake, ND 48.11306  -98.90750
#> 71                          Wenatchee, WA 47.39972 -120.20778
#> 72                        Panama City, FL 30.35778  -85.79889
#> 73                              Eagle, CO 39.64361 -106.91389
#> 74                     Elmira/Corning, NY 42.16083  -76.89528
#> 75                            El Paso, TX 31.80667 -106.37722
#> 76                               Erie, PA 42.08000  -80.17861
#> 77                             Eugene, OR 44.12083 -123.21750
#> 78         New Bern/Morehead/Beaufort, NC 35.07361  -77.04250
#> 79  New York City, NY (Metropolitan Area) 40.69583  -74.17167
#> 80                           Key West, FL 24.55556  -81.75972
#> 81                          Fairbanks, AK 64.81444 -147.86278
#> 82                              Fargo, ND 46.91556  -96.81472
#> 83                             Fresno, CA 36.77667 -119.71722
#> 84                       Fayetteville, NC 34.99139  -78.88028
#> 85                          Kalispell, MT 48.31278 -114.25111
#> 86                          Flagstaff, AZ 35.13778 -111.67167
#> 87          Miami, FL (Metropolitan Area) 26.07417  -80.15167
#> 88                           Florence, SC 34.18889  -79.72444
#> 89                              Flint, MI 42.96667  -83.74167
#> 90                        Sioux Falls, SD 43.57889  -96.74083
#> 91                         Fort Smith, AR 35.33667  -94.36750
#> 92                         Fort Wayne, IN 40.97833  -85.18806
#> 93                           Gillette, WY 44.35139 -105.52500
#> 94                            Spokane, WA 47.62000 -117.53278
#> 95                        Grand Forks, ND 47.95194  -97.17861
#> 96                     Grand Junction, CO 39.11861 -108.51389
#> 97                        Gainesville, FL 29.68972  -82.27583
#> 98                    Gulfport/Biloxi, MS 30.40611  -89.07028
#> 99                          Green Bay, WI 44.48806  -88.13056
#> 100                           Killeen, TX 31.06472  -97.82750
#> 101                      Grand Rapids, MI 42.88111  -85.52417
#> 102             Greensboro/High Point, NC 36.09194  -79.94278
#> 103            Greenville/Spartanburg, SC 34.89889  -82.21389
#> 104                       Great Falls, MT 47.48556 -111.36694
#> 105                 Steamboat Springs, CO 40.48167 -107.22000
#> 106                            Helena, MT 46.60667 -111.98194
#> 107                          Honolulu, HI 21.31861 -157.92250
#> 108                           Houston, TX 29.64500  -95.27861
#> 109 New York City, NY (Metropolitan Area) 41.06889  -73.70778
#> 110              Harlingen/San Benito, TX 26.22806  -97.65222
#> 111                        Huntsville, AL 34.64278  -86.77556
#> 112                              Hays, KS 38.84611  -99.27417
#> 113    Washington, DC (Metropolitan Area) 38.94167  -77.45750
#> 114                           Houston, TX 29.98333  -95.34000
#> 115                           Wichita, KS 37.65000  -97.43278
#> 116                       Idaho Falls, ID 43.51611 -112.06472
#> 117                        Wilmington, NC 34.26694  -77.90389
#> 118                      Indianapolis, IN 39.72889  -86.28167
#> 119                         Williston, ND 48.17611 -103.63611
#> 120 New York City, NY (Metropolitan Area) 40.79667  -73.10083
#> 121                   Ithaca/Cortland, NY 42.49028  -76.45806
#> 122                              Hilo, HI 19.72361 -155.05806
#> 123                           Jackson, WY 43.60667 -110.73694
#> 124                 Jackson/Vicksburg, MS 32.30972  -90.07583
#> 125                      Jacksonville, FL 30.48472  -81.68778
#> 126 New York City, NY (Metropolitan Area) 40.63861  -73.77694
#> 127                            Juneau, AK 58.35556 -134.57472
#> 128                              Kona, HI 19.73889 -156.04556
#> 129                           Lansing, MI 42.77917  -84.58833
#> 130                         Las Vegas, NV 36.08000 -115.15222
#> 131                  Lawton/Fort Sill, OK 34.56972  -98.41611
#> 132   Los Angeles, CA (Metropolitan Area) 33.94250 -118.40806
#> 133                           Lubbock, TX 33.66222 -101.82278
#> 134                         Lexington, KY 38.03972  -84.60222
#> 135                         Lafayette, LA 30.20472  -91.98750
#> 136 New York City, NY (Metropolitan Area) 40.77944  -73.87583
#> 137   Los Angeles, CA (Metropolitan Area) 33.81750 -118.15111
#> 138                             Lihue, HI 21.97917 -159.34583
#> 139                       Little Rock, AR 34.72917  -92.23444
#> 140                     Klamath Falls, OR 42.16306 -121.73583
#> 141                            Laredo, TX 27.54472  -99.46111
#> 142                         La Crosse, WI 43.87722  -91.25639
#> 143                          Lewiston, ID 46.37472 -117.01444
#> 144                    Midland/Odessa, TX 31.94083 -102.20139
#> 145          Saginaw/Bay City/Midland, MI 43.53167  -84.08167
#> 146                       Kansas City, MO 39.29750  -94.71389
#> 147                           Orlando, FL 28.43167  -81.32472
#> 148                        Mason City, IA 43.15694  -93.32944
#> 149                        Harrisburg, PA 40.19306  -76.76222
#> 150                           Chicago, IL 41.78500  -87.75194
#> 151                          Meridian, MS 32.33722  -88.74917
#> 152                           Memphis, TN 35.04972  -89.97861
#> 153          Mission/McAllen/Edinburg, TX 26.17694  -98.23972
#> 154                           Medford, OR 42.37361 -122.87222
#> 155                        Montgomery, AL 32.30000  -86.39111
#> 156        Boston, MA (Metropolitan Area) 42.93833  -71.43889
#> 157         Miami, FL (Metropolitan Area) 25.79250  -80.28611
#> 158                         Milwaukee, WI 42.95028  -87.89722
#> 159                         Melbourne, FL 28.10250  -80.64306
#> 160   Quad Cities, IL (Metropolitan Area) 41.44889  -90.50500
#> 161                            Monroe, LA 32.51111  -92.03889
#> 162                     Mammoth Lakes, CA 37.63111 -118.85139
#> 163                            Mobile, AL 30.68833  -88.24083
#> 164                           Modesto, CA 37.62694 -120.95528
#> 165                             Minot, ND 48.25944 -101.28083
#> 166                         Marquette, MI 46.35361  -87.39528
#> 167                  Salinas/Monterey, CA 36.58806 -121.84806
#> 168                           Madison, WI 43.14194  -89.33694
#> 169                          Missoula, MT 46.91556 -114.08750
#> 170              Minneapolis/St. Paul, MN 44.88611  -93.21778
#> 171                       New Orleans, LA 29.99111  -90.25139
#> 172                    Montrose/Delta, CO 38.50056 -107.89472
#> 173                      Myrtle Beach, SC 33.67917  -78.92972
#> 174         Jacksonville/Camp Lejeune, NC 34.83028  -77.61167
#> 175 San Francisco, CA (Metropolitan Area) 37.72139 -122.22083
#> 176                           Kahului, HI 20.90056 -156.43361
#> 177                     Oklahoma City, OK 35.39222  -97.60167
#> 178                             Omaha, NE 41.30194  -95.89333
#> 179   Los Angeles, CA (Metropolitan Area) 34.05611 -117.60111
#> 180                           Chicago, IL 41.97806  -87.90611
#> 181       Norfolk, VA (Metropolitan Area) 36.89583  -76.20139
#> 182               North Bend/Coos Bay, OR 43.41889 -124.24000
#> 183        West Palm Beach/Palm Beach, FL 26.68222  -80.09417
#> 184                          Portland, OR 45.58917 -122.59500
#> 185                        Greenville, NC 35.63333  -77.38528
#> 186       Norfolk, VA (Metropolitan Area) 37.13167  -76.49333
#> 187                      Philadelphia, PA 39.86806  -75.24861
#> 188                           Phoenix, AZ 33.43611 -112.00944
#> 189                            Peoria, IL 40.66139  -89.68722
#> 190         Tampa, FL (Metropolitan Area) 27.90722  -82.68556
#> 191                         Pocatello, ID 42.91333 -112.59444
#> 192                            Pierre, SD 44.38361 -100.28417
#> 193                        Pittsburgh, PA 40.49667  -80.23583
#> 194                         Pensacola, FL 30.47333  -87.18750
#> 195          Pasco/Kennewick/Richland, WA 46.26389 -119.11472
#> 196                    Ponce, Puerto Rico 18.01083  -66.56361
#> 197                      Palm Springs, CA 33.82667 -116.50500
#> 198                           Pullman, WA 46.74472 -117.10500
#> 199        Boston, MA (Metropolitan Area) 41.72833  -71.42611
#> 200                          Portland, ME 43.64444  -70.30361
#> 201                        Rapid City, SD 44.04528 -103.05694
#> 202                      Bend/Redmond, OR 44.25444 -121.15139
#> 203                    Raleigh/Durham, NC 35.87528  -78.78194
#> 204                       Rhinelander, WI 45.63139  -89.45750
#> 205                          Richmond, VA 37.50528  -77.31972
#> 206                              Reno, NV 39.49778 -119.76750
#> 207                           Roanoke, VA 37.32472  -79.97639
#> 208                         Rochester, NY 43.12139  -77.67083
#> 209                         Rochester, MN 43.91028  -92.49639
#> 210                        Fort Myers, FL 26.53611  -81.75500
#> 211                         San Diego, CA 32.73278 -117.18722
#> 212                       San Antonio, TX 29.53333  -98.46944
#> 213                          Savannah, GA 32.12750  -81.20250
#> 214                     Santa Barbara, CA 34.42778 -119.83944
#> 215                        South Bend, IN 41.70444  -86.31250
#> 216       Paso Robles/San Luis Obispo, CA 35.23667 -120.63917
#> 217         Philipsburg/State College, PA 40.77083  -77.88139
#> 218                        Louisville, KY 38.17972  -85.73861
#> 219                           Seattle, WA 47.44722 -122.30556
#> 220                           Sanford, FL 28.77500  -81.24028
#> 221 San Francisco, CA (Metropolitan Area) 37.61889 -122.37500
#> 222                       Springfield, MO 37.24000  -93.38500
#> 223                        Shreveport, LA 32.44694  -93.82556
#> 224                             Sitka, AK 57.04861 -135.36167
#> 225 San Francisco, CA (Metropolitan Area) 37.36278 -121.94056
#> 226                 San Juan, Puerto Rico 18.44000  -66.00222
#> 227                    Salt Lake City, UT 40.78417 -111.96694
#> 228                        Sacramento, CA 38.69556 -121.58972
#> 229                       Santa Maria, CA 34.90500 -120.45778
#> 230   Los Angeles, CA (Metropolitan Area) 33.67556 -117.86694
#> 231                Sarasota/Bradenton, FL 27.39389  -82.55417
#> 232                         St. Louis, MO 38.74722  -90.36444
#> 233      Charlotte Amalie, Virgin Islands 18.33722  -64.97333
#> 234         Christiansted, Virgin Islands 17.70389  -64.79889
#> 235 New York City, NY (Metropolitan Area) 41.50583  -74.09722
#> 236                          Syracuse, NY 43.11056  -76.10250
#> 237                 Fort Leonard Wood, MO 37.74139  -92.14056
#> 238                       Tallahassee, FL 30.39972  -84.35194
#> 239                            Toledo, OH 41.59083  -83.80083
#> 240         Tampa, FL (Metropolitan Area) 27.97306  -82.53528
#> 241    Bristol/Johnson City/Kingsport, TN 36.47611  -82.40639
#> 242                             Tulsa, OK 36.19778  -95.88972
#> 243                            Tucson, AZ 32.11611 -110.94056
#> 244                     Traverse City, MI 44.74000  -85.58583
#> 245                 Thief River Falls, MN 48.06611  -96.18500
#> 246                         Texarkana, AR 33.45639  -93.98917
#> 247                         Knoxville, TN 35.81222  -83.99250
#> 248                          Valdosta, GA 30.78222  -83.27694
#> 249                        Valparaiso, FL 30.48333  -86.52528
#> 250                      Fayetteville, AR 36.28194  -94.30694
#> 251                              Yuma, AZ 32.65667 -114.60583
#>                      airport_city_name airport_country_code airport_state
#> 1       Allentown/Bethlehem/Easton, PA                   US            PA
#> 2                          Abilene, TX                   US            TX
#> 3                      Albuquerque, NM                   US            NM
#> 4                           Albany, GA                   US            GA
#> 5                             Waco, TX                   US            TX
#> 6                    Arcata/Eureka, CA                   US            CA
#> 7                    Atlantic City, NJ                   US            NJ
#> 8                       Alexandria, LA                   US            LA
#> 9                          Augusta, GA                   US            GA
#> 10                          Albany, NY                   US            NY
#> 11                        Amarillo, TX                   US            TX
#> 12                       Anchorage, AK                   US            AK
#> 13                           Aspen, CO                   US            CO
#> 14                         Atlanta, GA                   US            GA
#> 15                        Appleton, WI                   US            WI
#> 16              Augusta/Waterville, ME                   US            ME
#> 17                          Austin, TX                   US            TX
#> 18                       Asheville, NC                   US            NC
#> 19           Scranton/Wilkes-Barre, PA                   US            PA
#> 20                       Kalamazoo, MI                   US            MI
#> 21                        Hartford, CT                   US            CT
#> 22                          Bethel, AK                   US            AK
#> 23                      Binghamton, NY                   US            NY
#> 24                          Bangor, ME                   US            ME
#> 25                      Birmingham, AL                   US            AL
#> 26                        Billings, MT                   US            MT
#> 27                 Bismarck/Mandan, ND                   US            ND
#> 28                      Bellingham, WA                   US            WA
#> 29              Bloomington/Normal, IL                   US            IL
#> 30                       Nashville, TN                   US            TN
#> 31                           Boise, ID                   US            ID
#> 32                          Boston, MA                   US            MA
#> 33                       Brunswick, GA                   US            GA
#> 34                     Brownsville, TX                   US            TX
#> 35                     Baton Rouge, LA                   US            LA
#> 36                      Burlington, VT                   US            VT
#> 37                         Buffalo, NY                   US            NY
#> 38                         Burbank, CA                   US            CA
#> 39                       Baltimore, MD                   US            MD
#> 40                         Bozeman, MT                   US            MT
#> 41                        Columbia, SC                   US            SC
#> 42                           Akron, OH                   US            OH
#> 43                   Crescent City, CA                   US            CA
#> 44                     Chattanooga, TN                   US            TN
#> 45                 Charlottesville, VA                   US            VA
#> 46                      Charleston, SC                   US            SC
#> 47                           Chico, CA                   US            CA
#> 48          Cedar Rapids/Iowa City, IA                   US            IA
#> 49             Clarksburg/Fairmont, WV                   US            WV
#> 50                       Cleveland, OH                   US            OH
#> 51                       Charlotte, NC                   US            NC
#> 52                        Columbus, OH                   US            OH
#> 53                Hancock/Houghton, MI                   US            MI
#> 54                Colorado Springs, CO                   US            CO
#> 55                          Casper, WY                   US            WY
#> 56                  Corpus Christi, TX                   US            TX
#> 57               Charleston/Dunbar, WV                   US            WV
#> 58                        Columbus, GA                   US            GA
#> 59                      Cincinnati, OH                   US            KY
#> 60                         Mosinee, WI                   US            WI
#> 61                   Daytona Beach, FL                   US            FL
#> 62                          Dallas, TX                   US            TX
#> 63                          Dayton, OH                   US            OH
#> 64                      Washington, DC                   US            VA
#> 65                          Denver, CO                   US            CO
#> 66               Dallas/Fort Worth, TX                   US            TX
#> 67                          Duluth, MN                   US            MN
#> 68                      Des Moines, IA                   US            IA
#> 69                         Detroit, MI                   US            MI
#> 70                     Devils Lake, ND                   US            ND
#> 71                       Wenatchee, WA                   US            WA
#> 72                     Panama City, FL                   US            FL
#> 73                           Eagle, CO                   US            CO
#> 74                  Elmira/Corning, NY                   US            NY
#> 75                         El Paso, TX                   US            TX
#> 76                            Erie, PA                   US            PA
#> 77                          Eugene, OR                   US            OR
#> 78      New Bern/Morehead/Beaufort, NC                   US            NC
#> 79                          Newark, NJ                   US            NJ
#> 80                        Key West, FL                   US            FL
#> 81                       Fairbanks, AK                   US            AK
#> 82                           Fargo, ND                   US            ND
#> 83                          Fresno, CA                   US            CA
#> 84                    Fayetteville, NC                   US            NC
#> 85                       Kalispell, MT                   US            MT
#> 86                       Flagstaff, AZ                   US            AZ
#> 87                 Fort Lauderdale, FL                   US            FL
#> 88                        Florence, SC                   US            SC
#> 89                           Flint, MI                   US            MI
#> 90                     Sioux Falls, SD                   US            SD
#> 91                      Fort Smith, AR                   US            AR
#> 92                      Fort Wayne, IN                   US            IN
#> 93                        Gillette, WY                   US            WY
#> 94                         Spokane, WA                   US            WA
#> 95                     Grand Forks, ND                   US            ND
#> 96                  Grand Junction, CO                   US            CO
#> 97                     Gainesville, FL                   US            FL
#> 98                 Gulfport/Biloxi, MS                   US            MS
#> 99                       Green Bay, WI                   US            WI
#> 100                        Killeen, TX                   US            TX
#> 101                   Grand Rapids, MI                   US            MI
#> 102          Greensboro/High Point, NC                   US            NC
#> 103                          Greer, SC                   US            SC
#> 104                    Great Falls, MT                   US            MT
#> 105                         Hayden, CO                   US            CO
#> 106                         Helena, MT                   US            MT
#> 107                       Honolulu, HI                   US            HI
#> 108                        Houston, TX                   US            TX
#> 109                   White Plains, NY                   US            NY
#> 110           Harlingen/San Benito, TX                   US            TX
#> 111                     Huntsville, AL                   US            AL
#> 112                           Hays, KS                   US            KS
#> 113                     Washington, DC                   US            VA
#> 114                        Houston, TX                   US            TX
#> 115                        Wichita, KS                   US            KS
#> 116                    Idaho Falls, ID                   US            ID
#> 117                     Wilmington, NC                   US            NC
#> 118                   Indianapolis, IN                   US            IN
#> 119                      Williston, ND                   US            ND
#> 120                          Islip, NY                   US            NY
#> 121                Ithaca/Cortland, NY                   US            NY
#> 122                           Hilo, HI                   US            HI
#> 123                        Jackson, WY                   US            WY
#> 124              Jackson/Vicksburg, MS                   US            MS
#> 125                   Jacksonville, FL                   US            FL
#> 126                       New York, NY                   US            NY
#> 127                         Juneau, AK                   US            AK
#> 128                           Kona, HI                   US            HI
#> 129                        Lansing, MI                   US            MI
#> 130                      Las Vegas, NV                   US            NV
#> 131               Lawton/Fort Sill, OK                   US            OK
#> 132                    Los Angeles, CA                   US            CA
#> 133                        Lubbock, TX                   US            TX
#> 134                      Lexington, KY                   US            KY
#> 135                      Lafayette, LA                   US            LA
#> 136                       New York, NY                   US            NY
#> 137                     Long Beach, CA                   US            CA
#> 138                          Lihue, HI                   US            HI
#> 139                    Little Rock, AR                   US            AR
#> 140                  Klamath Falls, OR                   US            OR
#> 141                         Laredo, TX                   US            TX
#> 142                      La Crosse, WI                   US            WI
#> 143                       Lewiston, ID                   US            ID
#> 144                 Midland/Odessa, TX                   US            TX
#> 145       Saginaw/Bay City/Midland, MI                   US            MI
#> 146                    Kansas City, MO                   US            MO
#> 147                        Orlando, FL                   US            FL
#> 148                     Mason City, IA                   US            IA
#> 149                     Harrisburg, PA                   US            PA
#> 150                        Chicago, IL                   US            IL
#> 151                       Meridian, MS                   US            MS
#> 152                        Memphis, TN                   US            TN
#> 153       Mission/McAllen/Edinburg, TX                   US            TX
#> 154                        Medford, OR                   US            OR
#> 155                     Montgomery, AL                   US            AL
#> 156                     Manchester, NH                   US            NH
#> 157                          Miami, FL                   US            FL
#> 158                      Milwaukee, WI                   US            WI
#> 159                      Melbourne, FL                   US            FL
#> 160                         Moline, IL                   US            IL
#> 161                         Monroe, LA                   US            LA
#> 162                  Mammoth Lakes, CA                   US            CA
#> 163                         Mobile, AL                   US            AL
#> 164                        Modesto, CA                   US            CA
#> 165                          Minot, ND                   US            ND
#> 166                      Marquette, MI                   US            MI
#> 167                       Monterey, CA                   US            CA
#> 168                        Madison, WI                   US            WI
#> 169                       Missoula, MT                   US            MT
#> 170                    Minneapolis, MN                   US            MN
#> 171                    New Orleans, LA                   US            LA
#> 172                 Montrose/Delta, CO                   US            CO
#> 173                   Myrtle Beach, SC                   US            SC
#> 174      Jacksonville/Camp Lejeune, NC                   US            NC
#> 175                        Oakland, CA                   US            CA
#> 176                        Kahului, HI                   US            HI
#> 177                  Oklahoma City, OK                   US            OK
#> 178                          Omaha, NE                   US            NE
#> 179                        Ontario, CA                   US            CA
#> 180                        Chicago, IL                   US            IL
#> 181                        Norfolk, VA                   US            VA
#> 182            North Bend/Coos Bay, OR                   US            OR
#> 183     West Palm Beach/Palm Beach, FL                   US            FL
#> 184                       Portland, OR                   US            OR
#> 185                     Greenville, NC                   US            NC
#> 186      Newport News/Williamsburg, VA                   US            VA
#> 187                   Philadelphia, PA                   US            PA
#> 188                        Phoenix, AZ                   US            AZ
#> 189                         Peoria, IL                   US            IL
#> 190                 St. Petersburg, FL                   US            FL
#> 191                      Pocatello, ID                   US            ID
#> 192                         Pierre, SD                   US            SD
#> 193                     Pittsburgh, PA                   US            PA
#> 194                      Pensacola, FL                   US            FL
#> 195       Pasco/Kennewick/Richland, WA                   US            WA
#> 196                 Ponce, Puerto Rico                   PR              
#> 197                   Palm Springs, CA                   US            CA
#> 198                        Pullman, WA                   US            WA
#> 199                     Providence, RI                   US            RI
#> 200                       Portland, ME                   US            ME
#> 201                     Rapid City, SD                   US            SD
#> 202                   Bend/Redmond, OR                   US            OR
#> 203                 Raleigh/Durham, NC                   US            NC
#> 204                    Rhinelander, WI                   US            WI
#> 205                       Richmond, VA                   US            VA
#> 206                           Reno, NV                   US            NV
#> 207                        Roanoke, VA                   US            VA
#> 208                      Rochester, NY                   US            NY
#> 209                      Rochester, MN                   US            MN
#> 210                     Fort Myers, FL                   US            FL
#> 211                      San Diego, CA                   US            CA
#> 212                    San Antonio, TX                   US            TX
#> 213                       Savannah, GA                   US            GA
#> 214                  Santa Barbara, CA                   US            CA
#> 215                     South Bend, IN                   US            IN
#> 216                San Luis Obispo, CA                   US            CA
#> 217                  State College, PA                   US            PA
#> 218                     Louisville, KY                   US            KY
#> 219                        Seattle, WA                   US            WA
#> 220                        Sanford, FL                   US            FL
#> 221                  San Francisco, CA                   US            CA
#> 222                    Springfield, MO                   US            MO
#> 223                     Shreveport, LA                   US            LA
#> 224                          Sitka, AK                   US            AK
#> 225                       San Jose, CA                   US            CA
#> 226              San Juan, Puerto Rico                   PR              
#> 227                 Salt Lake City, UT                   US            UT
#> 228                     Sacramento, CA                   US            CA
#> 229                    Santa Maria, CA                   US            CA
#> 230                      Santa Ana, CA                   US            CA
#> 231             Sarasota/Bradenton, FL                   US            FL
#> 232                      St. Louis, MO                   US            MO
#> 233   Charlotte Amalie, Virgin Islands                   VI              
#> 234      Christiansted, Virgin Islands                   VI              
#> 235          Newburgh/Poughkeepsie, NY                   US            NY
#> 236                       Syracuse, NY                   US            NY
#> 237              Fort Leonard Wood, MO                   US            MO
#> 238                    Tallahassee, FL                   US            FL
#> 239                         Toledo, OH                   US            OH
#> 240                          Tampa, FL                   US            FL
#> 241 Bristol/Johnson City/Kingsport, TN                   US            TN
#> 242                          Tulsa, OK                   US            OK
#> 243                         Tucson, AZ                   US            AZ
#> 244                  Traverse City, MI                   US            MI
#> 245              Thief River Falls, MN                   US            MN
#> 246                      Texarkana, AR                   US            AR
#> 247                      Knoxville, TN                   US            TN
#> 248                       Valdosta, GA                   US            GA
#> 249                     Valparaiso, FL                   US            FL
#> 250                   Fayetteville, AR                   US            AR
#> 251                           Yuma, AZ                   US            AZ
#>     airport_id freq
#> 1        10135    7
#> 2        10136    3
#> 3        10140   42
#> 4        10146    1
#> 5        10155    1
#> 6        10157    1
#> 7        10158    2
#> 8        10185    2
#> 9        10208   10
#> 10       10257   10
#> 11       10279    7
#> 12       10299   18
#> 13       10372    8
#> 14       10397  487
#> 15       10408    5
#> 16       10414    1
#> 17       10423   63
#> 18       10431    6
#> 19       10434    3
#> 20       10469    1
#> 21       10529   61
#> 22       10551    2
#> 23       10577    4
#> 24       10581    6
#> 25       10599   24
#> 26       10620    4
#> 27       10627    2
#> 28       10666   15
#> 29       10685    6
#> 30       10693   97
#> 31       10713   27
#> 32       10721  315
#> 33       10731    1
#> 34       10747    2
#> 35       10781    6
#> 36       10785    7
#> 37       10792   44
#> 38       10800   20
#> 39       10821  148
#> 40       10849    4
#> 41       10868   13
#> 42       10874   39
#> 43       10930    2
#> 44       10980    5
#> 45       10990    4
#> 46       10994   25
#> 47       11002    1
#> 48       11003    9
#> 49       11027    1
#> 50       11042   47
#> 51       11057  218
#> 52       11066   44
#> 53       11076    1
#> 54       11109   12
#> 55       11122    2
#> 56       11140    5
#> 57       11146   12
#> 58       11150    1
#> 59       11193   53
#> 60       11203    2
#> 61       11252    7
#> 62       11259   55
#> 63       11267   32
#> 64       11278  186
#> 65       11292  386
#> 66       11298  382
#> 67       11337    1
#> 68       11423   20
#> 69       11433  179
#> 70       11447    2
#> 71       11470    1
#> 72       11481    6
#> 73       11503   10
#> 74       11537    3
#> 75       11540   21
#> 76       11577    2
#> 77       11603    6
#> 78       11617    2
#> 79       11618  143
#> 80       11624    7
#> 81       11630    6
#> 82       11637    7
#> 83       11638    9
#> 84       11641    7
#> 85       11648    5
#> 86       11695    1
#> 87       11697  217
#> 88       11699    2
#> 89       11721   31
#> 90       11775    3
#> 91       11778    3
#> 92       11823    8
#> 93       11865    1
#> 94       11884   24
#> 95       11898    2
#> 96       11921   10
#> 97       11953    3
#> 98       11973    2
#> 99       11977    7
#> 100      11982    1
#> 101      11986   24
#> 102      11995   10
#> 103      11996   15
#> 104      12003    2
#> 105      12094    4
#> 106      12156    2
#> 107      12173   76
#> 108      12191   77
#> 109      12197   50
#> 110      12206    7
#> 111      12217   14
#> 112      12255    1
#> 113      12264   95
#> 114      12266  191
#> 115      12278   10
#> 116      12280    1
#> 117      12323    6
#> 118      12339   77
#> 119      12389    1
#> 120      12391   25
#> 121      12397    3
#> 122      12402    3
#> 123      12441    6
#> 124      12448   10
#> 125      12451   39
#> 126      12478  330
#> 127      12523    4
#> 128      12758   16
#> 129      12884    8
#> 130      12889  347
#> 131      12891    1
#> 132      12892  374
#> 133      12896    9
#> 134      12945    9
#> 135      12951    2
#> 136      12953  229
#> 137      12954   12
#> 138      12982   24
#> 139      12992   31
#> 140      13024    2
#> 141      13061    3
#> 142      13076    4
#> 143      13127    1
#> 144      13158    5
#> 145      13184    8
#> 146      13198   86
#> 147      13204  299
#> 148      13211    1
#> 149      13230   18
#> 150      13232  128
#> 151      13241    2
#> 152      13244   78
#> 153      13256    8
#> 154      13264    4
#> 155      13277    1
#> 156      13296   50
#> 157      13303  130
#> 158      13342   85
#> 159      13360    7
#> 160      13367    1
#> 161      13377    3
#> 162      13388    2
#> 163      13422    9
#> 164      13424    1
#> 165      13433    2
#> 166      13459    4
#> 167      13476    4
#> 168      13485   15
#> 169      13486    1
#> 170      13487  222
#> 171      13495  125
#> 172      13502    2
#> 173      13577    4
#> 174      13795    7
#> 175      13796   57
#> 176      13830   31
#> 177      13851   43
#> 178      13871   46
#> 179      13891   35
#> 180      13930  395
#> 181      13931   23
#> 182      13964    2
#> 183      14027   40
#> 184      14057  136
#> 185      14092    5
#> 186      14098   12
#> 187      14100  179
#> 188      14107  305
#> 189      14108    3
#> 190      14112    8
#> 191      14113    2
#> 192      14120    2
#> 193      14122   56
#> 194      14193   16
#> 195      14252    3
#> 196      14254    4
#> 197      14262   18
#> 198      14303    1
#> 199      14307   28
#> 200      14321   15
#> 201      14457    2
#> 202      14489    2
#> 203      14492   72
#> 204      14520    2
#> 205      14524   25
#> 206      14570   47
#> 207      14574    4
#> 208      14576   25
#> 209      14633    7
#> 210      14635  117
#> 211      14679  102
#> 212      14683   69
#> 213      14685   14
#> 214      14689    3
#> 215      14696    1
#> 216      14698    7
#> 217      14711    2
#> 218      14730   17
#> 219      14747  221
#> 220      14761    2
#> 221      14771  309
#> 222      14783    8
#> 223      14814   11
#> 224      14828    1
#> 225      14831   30
#> 226      14843   64
#> 227      14869  153
#> 228      14893   45
#> 229      14905    2
#> 230      14908   89
#> 231      14986    8
#> 232      15016   94
#> 233      15024   13
#> 234      15027    8
#> 235      15070    3
#> 236      15096   13
#> 237      15138    1
#> 238      15249    3
#> 239      15295    2
#> 240      15304  165
#> 241      15323    2
#> 242      15370   17
#> 243      15376   30
#> 244      15380    3
#> 245      15381    1
#> 246      15401    1
#> 247      15412   19
#> 248      15607    2
#> 249      15624    7
#> 250      15919    7
#> 251      16218    3
#> 
#> attr(,"class")
#> [1] "skynet"

# Apply Disparity Filter
make_net_dir(OD_Sample, disp = TRUE, alpha = 0.05)
#> $gDir_disp
#> IGRAPH 8a9231f DNW- 64 120 -- 
#> + attr: name (v/c), pass_dep (v/n), pass_arr (v/n), pass_tr (v/n),
#> | city_mkt_id (v/n), city (v/c), latitude (v/n), longitude (v/n),
#> | airport_city_name (v/c), airport_country_code (v/c), airport_state
#> | (v/c), airport_id (v/n), freq (v/n), weight (e/n), fare_sd (e/n),
#> | itin_fare (e/n), itin_yield (e/n), distance (e/n), year (e/n),
#> | quarter (e/n), alpha (e/n)
#> + edges from 8a9231f (vertex names):
#>  [1] ABQ->SLC ATL->DEN ATL->FLL ATL->JAX ATL->LAS ATL->MCO ATL->MKE ATL->MSY
#>  [9] ATL->PHF ATL->PIT ATL->TPA AUS->DFW BNA->LGA BOS->ATL BOS->DFW BOS->ORD
#> [17] BOS->PHL BOS->SFO BWI->BOS BWI->CLT BWI->MDW BWI->MHT CAK->ATL CLT->LGA
#> + ... omitted several edges
#> 
#> $netDir_disp
#>     origin dest passengers fare_sd itin_fare itin_yield distance year quarter
#> 1      ABQ  SLC          5    0.00    123.50 0.25050000      493 2011       1
#> 2      ATL  DEN         12   99.20    135.21 0.11277143     1199 2011       1
#> 3      ATL  FLL         37   78.55     89.72 0.15441667      581 2011       1
#> 4      ATL  JAX          4   32.77     90.77 0.33620000      270 2011       1
#> 5      ATL  LAS         13  240.35    253.56 0.14514000     1747 2011       1
#> 6      ATL  MCO         13   48.96     70.12 0.17398750      403 2011       1
#> 7      ATL  MKE         14  114.92    103.25 0.15433333      669 2011       1
#> 8      ATL  MSY         24   13.31    113.90 0.26800000      425 2011       1
#> 9      ATL  PHF          7   31.94     73.41 0.14450000      508 2011       1
#> 10     ATL  PIT          7   48.54     34.32 0.06525000      526 2011       1
#> 11     ATL  TPA         14  109.36    112.67 0.27750000      406 2011       1
#> 12     AUS  DFW          9   14.37     31.44 0.16548000      190 2011       1
#> 13     BNA  LGA         21    0.00      2.52 0.00330000      764 2011       1
#> 14     BOS  ATL         12   39.68     97.31 0.10286667      946 2011       1
#> 15     BOS  DFW         11  114.54    224.50 0.14372500     1562 2011       1
#> 16     BOS  ORD         19   66.28    183.41 0.21155000      867 2011       1
#> 17     BOS  PHL         10   19.94     24.93 0.08903333      280 2011       1
#> 18     BOS  SFO        115   91.78    224.43 0.08300000     2704 2011       1
#> 19     BWI  BOS          7   55.65     89.49 0.24186000      370 2011       1
#> 20     BWI  CLT          7   37.98     73.14 0.20260000      361 2011       1
#> 21     BWI  MDW          8  103.47    125.74 0.20580000      611 2011       1
#> 22     BWI  MHT          9    1.81     72.80 0.19310000      377 2011       1
#> 23     CAK  ATL         21   41.92     62.32 0.11803333      528 2011       1
#> 24     CLT  LGA          9   52.18    106.62 0.19600000      544 2011       1
#> 25     DAL  DEN          9  139.52    177.36 0.27245000      651 2011       1
#> 26     DAL  HOU          7   53.66     97.58 0.40828000      239 2011       1
#> 27     DAY  TPA          8    0.00     79.49 0.09600000      828 2011       1
#> 28     DCA  DEN         25   15.45    188.63 0.12780000     1476 2011       1
#> 29     DEN  LAS         20   91.43    120.12 0.19097500      629 2011       1
#> 30     DEN  MDW         17    4.60     97.58 0.10903333      895 2011       1
#> 31     DEN  MKE         13   16.85    113.88 0.12710000      896 2011       1
#> 32     DEN  OMA          8   41.42     67.77 0.14358000      472 2011       1
#> 33     DEN  PHX         28   52.77    102.50 0.17026000      602 2011       1
#> 34     DEN  SAN          8   64.91    165.45 0.19396000      853 2011       1
#> 35     DEN  SMF          6   93.13    183.82 0.20222500      909 2011       1
#> 36     DFW  BNA          6  130.68    121.42 0.19242000      631 2011       1
#> 37     DFW  CLT          8   76.79    174.94 0.18690000      936 2011       1
#> 38     DFW  DCA         44   25.45    128.97 0.10820000     1192 2011       1
#> 39     DFW  LAX         10   93.09    214.37 0.17357500     1235 2011       1
#> 40     DFW  ONT          5   57.76    164.72 0.13865000     1188 2011       1
#> 41     DFW  ORD         12  189.69    184.54 0.23010000      802 2011       1
#> 42     DFW  PHL         11  403.34    409.67 0.31465000     1302 2011       1
#> 43     DFW  SNA         11   43.09    109.86 0.09116667     1205 2011       1
#> 44     DTW  IAH          7    0.00    153.55 0.14270000     1076 2011       1
#> 45     DTW  MSP          7   18.29     55.49 0.10510000      528 2011       1
#> 46     ELP  DFW          6   63.06    117.99 0.21413333      551 2011       1
#> 47     EWR  BOS         21  249.80    149.61 0.74803333      200 2011       1
#> 48     EWR  MCO         13   47.56    114.86 0.12245000      938 2011       1
#> 49     FLL  CLE         10   48.23    234.35 0.22066667     1062 2011       1
#> 50     FLL  JFK         26   80.62    160.67 0.15030000     1069 2011       1
#> 51     HNL  LAX         10  126.31    193.43 0.07567500     2556 2011       1
#> 52     HPN  RSW         22    0.00    140.95 0.12790000     1102 2011       1
#> 53     IAD  DEN          6   92.07    176.03 0.12123333     1452 2011       1
#> 54     IAD  SLC         12    0.00    214.49 0.11740000     1827 2011       1
#> 55     IAH  LAS         20  123.56    241.47 0.19760000     1222 2011       1
#> 56     IAH  MSY         12  140.36    123.68 0.40550000      305 2011       1
#> 57     IAH  ORD         16  329.13    232.73 0.25160000      925 2011       1
#> 58     IND  ATL          9   65.69     80.64 0.18667500      432 2011       1
#> 59     JFK  TPA         13    0.00    191.45 0.19050000     1005 2011       1
#> 60     LAS  DEN         22  110.73    124.76 0.19835000      629 2011       1
#> 61     LAS  DTW         10   75.12    258.00 0.14742857     1750 2011       1
#> 62     LAS  EWR         20    0.00    224.04 0.10060000     2227 2011       1
#> 63     LAS  LAX         13   84.84    102.13 0.43273333      236 2011       1
#> 64     LAS  MDW         16   63.24    163.81 0.10770000     1521 2011       1
#> 65     LAS  MSP         12  225.21    298.74 0.22980000     1300 2011       1
#> 66     LAS  PDX         20    0.00     94.03 0.12340000      762 2011       1
#> 67     LAX  ATL         16  163.62    181.35 0.09319286     1946 2011       1
#> 68     LAX  JFK        137  203.64    322.86 0.13045000     2475 2011       1
#> 69     LAX  SEA         17  116.76    201.34 0.21105000      954 2011       1
#> 70     LGA  CLT         10   33.67     86.18 0.15842500      544 2011       1
#> 71     LGA  ORD         55   85.24     80.87 0.11033333      733 2011       1
#> 72     MCO  ATL         12  148.40    114.22 0.28342500      403 2011       1
#> 73     MCO  DTW          7  100.08     77.76 0.08125000      957 2011       1
#> 74     MCO  FNT         20    0.00     84.52 0.08360000     1011 2011       1
#> 75     MCO  HPN         17    0.00    120.04 0.12350000      972 2011       1
#> 76     MCO  IAH          8   34.21     97.48 0.11428000      853 2011       1
#> 77     MCO  MHT         17    0.00    164.45 0.14400000     1142 2011       1
#> 78     MCO  MSP         18   41.13    188.84 0.14415000     1310 2011       1
#> 79     MDW  ISP         12  141.08    221.77 0.28990000      765 2011       1
#> 80     MEM  ATL         15   38.44     66.61 0.20063333      332 2011       1
#> 81     MIA  CVG          5    0.00    182.49 0.19250000      948 2011       1
#> 82     MIA  JFK         28  111.79    213.35 0.19573333     1090 2011       1
#> 83     MKE  DFW          7  142.17    226.00 0.26495000      853 2011       1
#> 84     MSP  DFW          7  141.11    240.69 0.28250000      852 2011       1
#> 85     MSP  DTW          7   11.96     76.03 0.14400000      528 2011       1
#> 86     MSP  MCO          7   29.08    152.57 0.11646667     1310 2011       1
#> 87     MSY  HOU         18   37.13    117.82 0.38883333      303 2011       1
#> 88     OAK  ABQ          9    0.00    135.48 0.15240000      889 2011       1
#> 89     OGG  LAX          7  104.76     71.43 0.02873333     2486 2011       1
#> 90     ORD  EWR          8  263.96    274.74 0.38212000      719 2011       1
#> 91     ORD  RSW         16   82.88    229.29 0.20472500     1120 2011       1
#> 92     ORD  STL          5   16.80     54.65 0.21182000      258 2011       1
#> 93     PDX  SEA          8   66.46     59.36 0.46015000      129 2011       1
#> 94     PHL  DEN          9  170.78    216.82 0.13925556     1557 2011       1
#> 95     PHL  RDU         17    0.00      2.02 0.00600000      336 2011       1
#> 96     PHX  PDX         35   60.36     86.61 0.08583333     1009 2011       1
#> 97     PHX  SEA         14   75.69    317.89 0.28716667     1107 2011       1
#> 98     PHX  SLC          8   54.40     80.82 0.15941667      507 2011       1
#> 99     RDU  ATL          7   80.20    102.78 0.28870000      356 2011       1
#> 100    RNO  LAS          7    0.00    200.51 0.58120000      345 2011       1
#> 101    RSW  BWI         10    0.00    161.47 0.17570000      919 2011       1
#> 102    SAN  MSP         13    0.00    242.52 0.15830000     1532 2011       1
#> 103    SAN  PHX         11   30.69     48.27 0.15876667      304 2011       1
#> 104    SAT  DAL          6    0.60     98.43 0.39690000      248 2011       1
#> 105    SEA  ANC          6  229.46    253.38 0.17486667     1449 2011       1
#> 106    SEA  JFK         33   23.53    185.29 0.07653333     2421 2011       1
#> 107    SEA  RNO         13   58.86     90.86 0.16110000      564 2011       1
#> 108    SEA  SAN          8  101.28     88.10 0.08390000     1050 2011       1
#> 109    SFO  BOS         14  136.93    249.58 0.09230000     2704 2011       1
#> 110    SFO  ORD         18  126.64    203.56 0.11027000     1846 2011       1
#> 111    SFO  SNA         14   61.98    125.80 0.33818000      372 2011       1
#> 112    SLC  DEN          9   32.67     43.89 0.11253333      390 2011       1
#> 113    SLC  IAD          6  217.04    407.97 0.22330000     1827 2011       1
#> 114    SLC  PDX         14   28.02     74.69 0.11855000      630 2011       1
#> 115    SMF  DEN          9   37.05    149.24 0.16418000      909 2011       1
#> 116    SNA  SEA         15   37.10    196.63 0.20105000      978 2011       1
#> 117    STL  DFW         18  166.92    114.18 0.20722500      551 2011       1
#> 118    STL  LIT         10   70.45    117.69 0.39760000      296 2011       1
#> 119    TPA  FLL         14    0.00     39.50 0.20050000      197 2011       1
#> 120    TPA  MIA         12    0.00     83.50 0.40930000      204 2011       1
#>            alpha origin_city_mkt_id                           origin_city
#> 1   4.532261e-02              30140                       Albuquerque, NM
#> 2   2.613600e-02              30397       Atlanta, GA (Metropolitan Area)
#> 3   2.309949e-05              30397       Atlanta, GA (Metropolitan Area)
#> 4   4.840026e-02              30397       Atlanta, GA (Metropolitan Area)
#> 5   1.374511e-02              30397       Atlanta, GA (Metropolitan Area)
#> 6   1.639843e-02              30397       Atlanta, GA (Metropolitan Area)
#> 7   5.637710e-03              30397       Atlanta, GA (Metropolitan Area)
#> 8   5.421011e-04              30397       Atlanta, GA (Metropolitan Area)
#> 9   4.938272e-02              30397       Atlanta, GA (Metropolitan Area)
#> 10  2.331428e-02              30397       Atlanta, GA (Metropolitan Area)
#> 11  7.206141e-03              30397       Atlanta, GA (Metropolitan Area)
#> 12  5.138231e-03              30423                            Austin, TX
#> 13  1.118479e-04              30693                         Nashville, TN
#> 14  2.483044e-02              30721        Boston, MA (Metropolitan Area)
#> 15  3.271898e-02              30721        Boston, MA (Metropolitan Area)
#> 16  6.859064e-03              30721        Boston, MA (Metropolitan Area)
#> 17  1.479850e-02              30721        Boston, MA (Metropolitan Area)
#> 18  4.978430e-12              30721        Boston, MA (Metropolitan Area)
#> 19  4.889501e-02              30852    Washington, DC (Metropolitan Area)
#> 20  4.889501e-02              30852    Washington, DC (Metropolitan Area)
#> 21  3.114966e-02              30852    Washington, DC (Metropolitan Area)
#> 22  1.974021e-02              30852    Washington, DC (Metropolitan Area)
#> 23  1.411801e-03              30647     Cleveland, OH (Metropolitan Area)
#> 24  2.676724e-02              31057                         Charlotte, NC
#> 25  1.657674e-02              30194                 Dallas/Fort Worth, TX
#> 26  4.507324e-02              30194                 Dallas/Fort Worth, TX
#> 27  3.901844e-02              31267                            Dayton, OH
#> 28  7.210151e-05              30852    Washington, DC (Metropolitan Area)
#> 29  1.129816e-03              30325                            Denver, CO
#> 30  2.233613e-03              30325                            Denver, CO
#> 31  8.610884e-03              30325                            Denver, CO
#> 32  7.707347e-03              30325                            Denver, CO
#> 33  8.132132e-05              30325                            Denver, CO
#> 34  4.335380e-02              30325                            Denver, CO
#> 35  4.885956e-02              30325                            Denver, CO
#> 36  4.953292e-02              30194                 Dallas/Fort Worth, TX
#> 37  3.263568e-02              30194                 Dallas/Fort Worth, TX
#> 38  1.395278e-07              30194                 Dallas/Fort Worth, TX
#> 39  4.045095e-02              30194                 Dallas/Fort Worth, TX
#> 40  4.223514e-02              30194                 Dallas/Fort Worth, TX
#> 41  2.767289e-02              30194                 Dallas/Fort Worth, TX
#> 42  9.507933e-03              30194                 Dallas/Fort Worth, TX
#> 43  2.829487e-02              30194                 Dallas/Fort Worth, TX
#> 44  4.003612e-02              31295                           Detroit, MI
#> 45  4.391918e-02              31295                           Detroit, MI
#> 46  2.328306e-02              30615                           El Paso, TX
#> 47  1.237486e-04              31703 New York City, NY (Metropolitan Area)
#> 48  5.117920e-03              31703 New York City, NY (Metropolitan Area)
#> 49  1.921834e-03              32467         Miami, FL (Metropolitan Area)
#> 50  4.494284e-04              32467         Miami, FL (Metropolitan Area)
#> 51  2.559983e-02              32134                          Honolulu, HI
#> 52  5.560684e-03              31703 New York City, NY (Metropolitan Area)
#> 53  4.736244e-02              30852    Washington, DC (Metropolitan Area)
#> 54  1.626276e-03              30852    Washington, DC (Metropolitan Area)
#> 55  5.351231e-04              31453                           Houston, TX
#> 56  1.249577e-02              31453                           Houston, TX
#> 57  2.650844e-03              31453                           Houston, TX
#> 58  2.539762e-02              32337                      Indianapolis, IN
#> 59  1.052377e-02              31703 New York City, NY (Metropolitan Area)
#> 60  1.088578e-03              32211                         Las Vegas, NV
#> 61  9.327860e-03              32211                         Las Vegas, NV
#> 62  1.527963e-04              32211                         Las Vegas, NV
#> 63  1.470214e-02              32211                         Las Vegas, NV
#> 64  3.296342e-03              32211                         Las Vegas, NV
#> 65  1.916664e-02              32211                         Las Vegas, NV
#> 66  1.398906e-02              32211                         Las Vegas, NV
#> 67  7.016108e-03              32575   Los Angeles, CA (Metropolitan Area)
#> 68  3.468090e-13              32575   Los Angeles, CA (Metropolitan Area)
#> 69  1.029533e-02              32575   Los Angeles, CA (Metropolitan Area)
#> 70  1.350969e-02              31703 New York City, NY (Metropolitan Area)
#> 71  1.911308e-07              31703 New York City, NY (Metropolitan Area)
#> 72  2.483044e-02              31454                           Orlando, FL
#> 73  3.949289e-02              31454                           Orlando, FL
#> 74  1.330279e-02              31454                           Orlando, FL
#> 75  2.110736e-03              31454                           Orlando, FL
#> 76  2.487860e-02              31454                           Orlando, FL
#> 77  2.765039e-03              31454                           Orlando, FL
#> 78  2.377319e-03              31454                           Orlando, FL
#> 79  1.358595e-03              30977                           Chicago, IL
#> 80  6.082694e-05              33244                           Memphis, TN
#> 81  3.529285e-02              32467         Miami, FL (Metropolitan Area)
#> 82  1.469534e-04              32467         Miami, FL (Metropolitan Area)
#> 83  1.737040e-02              33342                         Milwaukee, WI
#> 84  4.133675e-02              31650              Minneapolis/St. Paul, MN
#> 85  3.949289e-02              31650              Minneapolis/St. Paul, MN
#> 86  4.133675e-02              31650              Minneapolis/St. Paul, MN
#> 87  2.111084e-03              33495                       New Orleans, LA
#> 88  9.094947e-03              32457 San Francisco, CA (Metropolitan Area)
#> 89  4.142919e-02              33830                           Kahului, HI
#> 90  4.157975e-02              30977                           Chicago, IL
#> 91  1.936109e-03              30977                           Chicago, IL
#> 92  4.410027e-02              30977                           Chicago, IL
#> 93  2.229119e-02              34057                          Portland, OR
#> 94  3.007081e-02              34100                      Philadelphia, PA
#> 95  3.141042e-04              34100                      Philadelphia, PA
#> 96  2.692537e-05              30466                           Phoenix, AZ
#> 97  1.885842e-02              30466                           Phoenix, AZ
#> 98  4.305676e-02              30466                           Phoenix, AZ
#> 99  3.633258e-02              34492                    Raleigh/Durham, NC
#> 100 3.901844e-02              34570                              Reno, NV
#> 101 1.181149e-02              31714                        Fort Myers, FL
#> 102 9.260441e-03              33570                         San Diego, CA
#> 103 2.080989e-02              33570                         San Diego, CA
#> 104 4.900793e-02              33214                       San Antonio, TX
#> 105 2.560000e-02              30559                           Seattle, WA
#> 106 7.094455e-05              30559                           Seattle, WA
#> 107 8.585703e-03              30559                           Seattle, WA
#> 108 4.335380e-02              30559                           Seattle, WA
#> 109 1.528783e-02              32457 San Francisco, CA (Metropolitan Area)
#> 110 4.185651e-03              32457 San Francisco, CA (Metropolitan Area)
#> 111 9.051151e-03              32457 San Francisco, CA (Metropolitan Area)
#> 112 2.299618e-02              34614                    Salt Lake City, UT
#> 113 2.235574e-02              34614                    Salt Lake City, UT
#> 114 2.398491e-03              34614                    Salt Lake City, UT
#> 115 1.801440e-02              33192                        Sacramento, CA
#> 116 5.523439e-03              32575   Los Angeles, CA (Metropolitan Area)
#> 117 1.628414e-03              31123                         St. Louis, MO
#> 118 7.812500e-03              31123                         St. Louis, MO
#> 119 9.253291e-03              33195         Tampa, FL (Metropolitan Area)
#> 120 1.059051e-02              33195         Tampa, FL (Metropolitan Area)
#>     dest_city_mkt_id                             dest_city
#> 1              34614                    Salt Lake City, UT
#> 2              30325                            Denver, CO
#> 3              32467         Miami, FL (Metropolitan Area)
#> 4              31136                      Jacksonville, FL
#> 5              32211                         Las Vegas, NV
#> 6              31454                           Orlando, FL
#> 7              33342                         Milwaukee, WI
#> 8              33495                       New Orleans, LA
#> 9              33667       Norfolk, VA (Metropolitan Area)
#> 10             30198                        Pittsburgh, PA
#> 11             33195         Tampa, FL (Metropolitan Area)
#> 12             30194                 Dallas/Fort Worth, TX
#> 13             31703 New York City, NY (Metropolitan Area)
#> 14             30397       Atlanta, GA (Metropolitan Area)
#> 15             30194                 Dallas/Fort Worth, TX
#> 16             30977                           Chicago, IL
#> 17             34100                      Philadelphia, PA
#> 18             32457 San Francisco, CA (Metropolitan Area)
#> 19             30721        Boston, MA (Metropolitan Area)
#> 20             31057                         Charlotte, NC
#> 21             30977                           Chicago, IL
#> 22             30721        Boston, MA (Metropolitan Area)
#> 23             30397       Atlanta, GA (Metropolitan Area)
#> 24             31703 New York City, NY (Metropolitan Area)
#> 25             30325                            Denver, CO
#> 26             31453                           Houston, TX
#> 27             33195         Tampa, FL (Metropolitan Area)
#> 28             30325                            Denver, CO
#> 29             32211                         Las Vegas, NV
#> 30             30977                           Chicago, IL
#> 31             33342                         Milwaukee, WI
#> 32             33316                             Omaha, NE
#> 33             30466                           Phoenix, AZ
#> 34             33570                         San Diego, CA
#> 35             33192                        Sacramento, CA
#> 36             30693                         Nashville, TN
#> 37             31057                         Charlotte, NC
#> 38             30852    Washington, DC (Metropolitan Area)
#> 39             32575   Los Angeles, CA (Metropolitan Area)
#> 40             32575   Los Angeles, CA (Metropolitan Area)
#> 41             30977                           Chicago, IL
#> 42             34100                      Philadelphia, PA
#> 43             32575   Los Angeles, CA (Metropolitan Area)
#> 44             31453                           Houston, TX
#> 45             31650              Minneapolis/St. Paul, MN
#> 46             30194                 Dallas/Fort Worth, TX
#> 47             30721        Boston, MA (Metropolitan Area)
#> 48             31454                           Orlando, FL
#> 49             30647     Cleveland, OH (Metropolitan Area)
#> 50             31703 New York City, NY (Metropolitan Area)
#> 51             32575   Los Angeles, CA (Metropolitan Area)
#> 52             31714                        Fort Myers, FL
#> 53             30325                            Denver, CO
#> 54             34614                    Salt Lake City, UT
#> 55             32211                         Las Vegas, NV
#> 56             33495                       New Orleans, LA
#> 57             30977                           Chicago, IL
#> 58             30397       Atlanta, GA (Metropolitan Area)
#> 59             33195         Tampa, FL (Metropolitan Area)
#> 60             30325                            Denver, CO
#> 61             31295                           Detroit, MI
#> 62             31703 New York City, NY (Metropolitan Area)
#> 63             32575   Los Angeles, CA (Metropolitan Area)
#> 64             30977                           Chicago, IL
#> 65             31650              Minneapolis/St. Paul, MN
#> 66             34057                          Portland, OR
#> 67             30397       Atlanta, GA (Metropolitan Area)
#> 68             31703 New York City, NY (Metropolitan Area)
#> 69             30559                           Seattle, WA
#> 70             31057                         Charlotte, NC
#> 71             30977                           Chicago, IL
#> 72             30397       Atlanta, GA (Metropolitan Area)
#> 73             31295                           Detroit, MI
#> 74             31721                             Flint, MI
#> 75             31703 New York City, NY (Metropolitan Area)
#> 76             31453                           Houston, TX
#> 77             30721        Boston, MA (Metropolitan Area)
#> 78             31650              Minneapolis/St. Paul, MN
#> 79             31703 New York City, NY (Metropolitan Area)
#> 80             30397       Atlanta, GA (Metropolitan Area)
#> 81             33105                        Cincinnati, OH
#> 82             31703 New York City, NY (Metropolitan Area)
#> 83             30194                 Dallas/Fort Worth, TX
#> 84             30194                 Dallas/Fort Worth, TX
#> 85             31295                           Detroit, MI
#> 86             31454                           Orlando, FL
#> 87             31453                           Houston, TX
#> 88             30140                       Albuquerque, NM
#> 89             32575   Los Angeles, CA (Metropolitan Area)
#> 90             31703 New York City, NY (Metropolitan Area)
#> 91             31714                        Fort Myers, FL
#> 92             31123                         St. Louis, MO
#> 93             30559                           Seattle, WA
#> 94             30325                            Denver, CO
#> 95             34492                    Raleigh/Durham, NC
#> 96             34057                          Portland, OR
#> 97             30559                           Seattle, WA
#> 98             34614                    Salt Lake City, UT
#> 99             30397       Atlanta, GA (Metropolitan Area)
#> 100            32211                         Las Vegas, NV
#> 101            30852    Washington, DC (Metropolitan Area)
#> 102            31650              Minneapolis/St. Paul, MN
#> 103            30466                           Phoenix, AZ
#> 104            30194                 Dallas/Fort Worth, TX
#> 105            30299                         Anchorage, AK
#> 106            31703 New York City, NY (Metropolitan Area)
#> 107            34570                              Reno, NV
#> 108            33570                         San Diego, CA
#> 109            30721        Boston, MA (Metropolitan Area)
#> 110            30977                           Chicago, IL
#> 111            32575   Los Angeles, CA (Metropolitan Area)
#> 112            30325                            Denver, CO
#> 113            30852    Washington, DC (Metropolitan Area)
#> 114            34057                          Portland, OR
#> 115            30325                            Denver, CO
#> 116            30559                           Seattle, WA
#> 117            30194                 Dallas/Fort Worth, TX
#> 118            32600                       Little Rock, AR
#> 119            32467         Miami, FL (Metropolitan Area)
#> 120            32467         Miami, FL (Metropolitan Area)
#> 
#> $nodes
#>    airport pass_dep pass_arr pass_tr city_mkt_id
#> 1      ABQ       22       24       4       30140
#> 2      ANC       12       10       4       30299
#> 3      ATL      395      321     229       30397
#> 4      AUS       27       40       4       30423
#> 5      BNA       62       45      10       30693
#> 6      BOS      213      106       4       30721
#> 7      BWI       94       76      22       30852
#> 8      CAK       28       12       1       30647
#> 9      CLE       19       42      14       30647
#> 10     CLT      186      170     138       31057
#> 11     CVG       31       28       6       33105
#> 12     DAL       42       27      14       30194
#> 13     DAY       24        8       0       31267
#> 14     DCA       97      113      24       30852
#> 15     DEN      256      253     123       30325
#> 16     DFW      277      250     145       30194
#> 17     DTW      120      127      68       31295
#> 18     ELP       16        6       1       30615
#> 19     EWR       88       72      17       31703
#> 20     FLL       98      127       8       32467
#> 21     FNT        4       27       0       31721
#> 22     HNL       57       29      10       32134
#> 23     HOU       35       65      23       31453
#> 24     HPN       26       24       0       31703
#> 25     IAD       66       52      23       30852
#> 26     IAH      143      121      73       31453
#> 27     IND       39       41       3       32337
#> 28     ISP        4       21       0       31703
#> 29     JAX       25       14       0       31136
#> 30     JFK       78      267      15       31703
#> 31     LAS      235      137      25       32211
#> 32     LAX      286      136      48       32575
#> 33     LGA      136      106      13       31703
#> 34     LIT       11       20       0       32600
#> 35     MCO      200      111      12       31454
#> 36     MDW       68      109      49       30977
#> 37     MEM       65       36      23       33244
#> 38     MHT       10       41       1       30721
#> 39     MIA       91       59      20       32467
#> 40     MKE       33       56       4       33342
#> 41     MSP      109      176      63       31650
#> 42     MSY       63       64       2       33495
#> 43     OAK       33       28       4       32457
#> 44     OGG       17       16       2       33830
#> 45     OMA       23       24       1       33316
#> 46     ONT       16       20       1       32575
#> 47     ORD      213      288     106       30977
#> 48     PDX       42      100       6       34057
#> 49     PHF        3        9       0       33667
#> 50     PHL      115      119      55       34100
#> 51     PHX      201      172      68       30466
#> 52     PIT       18       39       1       30198
#> 53     RDU       29       45       2       34492
#> 54     RNO       21       29       3       34570
#> 55     RSW       48       71       2       31714
#> 56     SAN       54       50       2       33570
#> 57     SAT       37       33       1       33214
#> 58     SEA      121      135      35       30559
#> 59     SFO      121      215      27       32457
#> 60     SLC      100       88      35       34614
#> 61     SMF       25       25       5       33192
#> 62     SNA       37       52       0       32575
#> 63     STL       60       49      15       31123
#> 64     TPA       76       98       9       33195
#>                                     city latitude  longitude
#> 1                        Albuquerque, NM 35.04167 -106.60639
#> 2                          Anchorage, AK 61.16917 -149.98528
#> 3        Atlanta, GA (Metropolitan Area) 33.64083  -84.42722
#> 4                             Austin, TX 30.19444  -97.67000
#> 5                          Nashville, TN 36.12667  -86.68194
#> 6         Boston, MA (Metropolitan Area) 42.36361  -71.00611
#> 7     Washington, DC (Metropolitan Area) 39.17500  -76.67000
#> 8      Cleveland, OH (Metropolitan Area) 40.91389  -81.44167
#> 9      Cleveland, OH (Metropolitan Area) 41.41083  -81.84944
#> 10                         Charlotte, NC 35.21917  -80.93583
#> 11                        Cincinnati, OH 39.04778  -84.66861
#> 12                 Dallas/Fort Worth, TX 32.84694  -96.85333
#> 13                            Dayton, OH 39.90111  -84.22000
#> 14    Washington, DC (Metropolitan Area) 38.85167  -77.03694
#> 15                            Denver, CO 39.77444 -104.87972
#> 16                 Dallas/Fort Worth, TX 32.89444  -97.02972
#> 17                           Detroit, MI 42.21667  -83.34444
#> 18                           El Paso, TX 31.80667 -106.37722
#> 19 New York City, NY (Metropolitan Area) 40.69583  -74.17167
#> 20         Miami, FL (Metropolitan Area) 26.07417  -80.15167
#> 21                             Flint, MI 42.96667  -83.74167
#> 22                          Honolulu, HI 21.31861 -157.92250
#> 23                           Houston, TX 29.64500  -95.27861
#> 24 New York City, NY (Metropolitan Area) 41.06889  -73.70778
#> 25    Washington, DC (Metropolitan Area) 38.94167  -77.45750
#> 26                           Houston, TX 29.98333  -95.34000
#> 27                      Indianapolis, IN 39.72889  -86.28167
#> 28 New York City, NY (Metropolitan Area) 40.79667  -73.10083
#> 29                      Jacksonville, FL 30.48472  -81.68778
#> 30 New York City, NY (Metropolitan Area) 40.63861  -73.77694
#> 31                         Las Vegas, NV 36.08000 -115.15222
#> 32   Los Angeles, CA (Metropolitan Area) 33.94250 -118.40806
#> 33 New York City, NY (Metropolitan Area) 40.77944  -73.87583
#> 34                       Little Rock, AR 34.72917  -92.23444
#> 35                           Orlando, FL 28.43167  -81.32472
#> 36                           Chicago, IL 41.78500  -87.75194
#> 37                           Memphis, TN 35.04972  -89.97861
#> 38        Boston, MA (Metropolitan Area) 42.93833  -71.43889
#> 39         Miami, FL (Metropolitan Area) 25.79250  -80.28611
#> 40                         Milwaukee, WI 42.95028  -87.89722
#> 41              Minneapolis/St. Paul, MN 44.88611  -93.21778
#> 42                       New Orleans, LA 29.99111  -90.25139
#> 43 San Francisco, CA (Metropolitan Area) 37.72139 -122.22083
#> 44                           Kahului, HI 20.90056 -156.43361
#> 45                             Omaha, NE 41.30194  -95.89333
#> 46   Los Angeles, CA (Metropolitan Area) 34.05611 -117.60111
#> 47                           Chicago, IL 41.97806  -87.90611
#> 48                          Portland, OR 45.58917 -122.59500
#> 49       Norfolk, VA (Metropolitan Area) 37.13167  -76.49333
#> 50                      Philadelphia, PA 39.86806  -75.24861
#> 51                           Phoenix, AZ 33.43611 -112.00944
#> 52                        Pittsburgh, PA 40.49667  -80.23583
#> 53                    Raleigh/Durham, NC 35.87528  -78.78194
#> 54                              Reno, NV 39.49778 -119.76750
#> 55                        Fort Myers, FL 26.53611  -81.75500
#> 56                         San Diego, CA 32.73278 -117.18722
#> 57                       San Antonio, TX 29.53333  -98.46944
#> 58                           Seattle, WA 47.44722 -122.30556
#> 59 San Francisco, CA (Metropolitan Area) 37.61889 -122.37500
#> 60                    Salt Lake City, UT 40.78417 -111.96694
#> 61                        Sacramento, CA 38.69556 -121.58972
#> 62   Los Angeles, CA (Metropolitan Area) 33.67556 -117.86694
#> 63                         St. Louis, MO 38.74722  -90.36444
#> 64         Tampa, FL (Metropolitan Area) 27.97306  -82.53528
#>                airport_city_name airport_country_code airport_state airport_id
#> 1                Albuquerque, NM                   US            NM      10140
#> 2                  Anchorage, AK                   US            AK      10299
#> 3                    Atlanta, GA                   US            GA      10397
#> 4                     Austin, TX                   US            TX      10423
#> 5                  Nashville, TN                   US            TN      10693
#> 6                     Boston, MA                   US            MA      10721
#> 7                  Baltimore, MD                   US            MD      10821
#> 8                      Akron, OH                   US            OH      10874
#> 9                  Cleveland, OH                   US            OH      11042
#> 10                 Charlotte, NC                   US            NC      11057
#> 11                Cincinnati, OH                   US            KY      11193
#> 12                    Dallas, TX                   US            TX      11259
#> 13                    Dayton, OH                   US            OH      11267
#> 14                Washington, DC                   US            VA      11278
#> 15                    Denver, CO                   US            CO      11292
#> 16         Dallas/Fort Worth, TX                   US            TX      11298
#> 17                   Detroit, MI                   US            MI      11433
#> 18                   El Paso, TX                   US            TX      11540
#> 19                    Newark, NJ                   US            NJ      11618
#> 20           Fort Lauderdale, FL                   US            FL      11697
#> 21                     Flint, MI                   US            MI      11721
#> 22                  Honolulu, HI                   US            HI      12173
#> 23                   Houston, TX                   US            TX      12191
#> 24              White Plains, NY                   US            NY      12197
#> 25                Washington, DC                   US            VA      12264
#> 26                   Houston, TX                   US            TX      12266
#> 27              Indianapolis, IN                   US            IN      12339
#> 28                     Islip, NY                   US            NY      12391
#> 29              Jacksonville, FL                   US            FL      12451
#> 30                  New York, NY                   US            NY      12478
#> 31                 Las Vegas, NV                   US            NV      12889
#> 32               Los Angeles, CA                   US            CA      12892
#> 33                  New York, NY                   US            NY      12953
#> 34               Little Rock, AR                   US            AR      12992
#> 35                   Orlando, FL                   US            FL      13204
#> 36                   Chicago, IL                   US            IL      13232
#> 37                   Memphis, TN                   US            TN      13244
#> 38                Manchester, NH                   US            NH      13296
#> 39                     Miami, FL                   US            FL      13303
#> 40                 Milwaukee, WI                   US            WI      13342
#> 41               Minneapolis, MN                   US            MN      13487
#> 42               New Orleans, LA                   US            LA      13495
#> 43                   Oakland, CA                   US            CA      13796
#> 44                   Kahului, HI                   US            HI      13830
#> 45                     Omaha, NE                   US            NE      13871
#> 46                   Ontario, CA                   US            CA      13891
#> 47                   Chicago, IL                   US            IL      13930
#> 48                  Portland, OR                   US            OR      14057
#> 49 Newport News/Williamsburg, VA                   US            VA      14098
#> 50              Philadelphia, PA                   US            PA      14100
#> 51                   Phoenix, AZ                   US            AZ      14107
#> 52                Pittsburgh, PA                   US            PA      14122
#> 53            Raleigh/Durham, NC                   US            NC      14492
#> 54                      Reno, NV                   US            NV      14570
#> 55                Fort Myers, FL                   US            FL      14635
#> 56                 San Diego, CA                   US            CA      14679
#> 57               San Antonio, TX                   US            TX      14683
#> 58                   Seattle, WA                   US            WA      14747
#> 59             San Francisco, CA                   US            CA      14771
#> 60            Salt Lake City, UT                   US            UT      14869
#> 61                Sacramento, CA                   US            CA      14893
#> 62                 Santa Ana, CA                   US            CA      14908
#> 63                 St. Louis, MO                   US            MO      15016
#> 64                     Tampa, FL                   US            FL      15304
#>    freq
#> 1    42
#> 2    18
#> 3   487
#> 4    63
#> 5    97
#> 6   315
#> 7   148
#> 8    39
#> 9    47
#> 10  218
#> 11   53
#> 12   55
#> 13   32
#> 14  186
#> 15  386
#> 16  382
#> 17  179
#> 18   21
#> 19  143
#> 20  217
#> 21   31
#> 22   76
#> 23   77
#> 24   50
#> 25   95
#> 26  191
#> 27   77
#> 28   25
#> 29   39
#> 30  330
#> 31  347
#> 32  374
#> 33  229
#> 34   31
#> 35  299
#> 36  128
#> 37   78
#> 38   50
#> 39  130
#> 40   85
#> 41  222
#> 42  125
#> 43   57
#> 44   31
#> 45   46
#> 46   35
#> 47  395
#> 48  136
#> 49   12
#> 50  179
#> 51  305
#> 52   56
#> 53   72
#> 54   47
#> 55  117
#> 56  102
#> 57   69
#> 58  221
#> 59  309
#> 60  153
#> 61   45
#> 62   89
#> 63   94
#> 64  165
#> 
#> attr(,"class")
#> [1] "skynet"

# Apply Percentage Cap
make_net_dir(OD_Sample, cap = TRUE, pct = 20)
#> $gDir_cap
#> IGRAPH 3db44e5 DNW- 114 418 -- 
#> + attr: name (v/c), pass_dep (v/n), pass_arr (v/n), pass_tr (v/n),
#> | city_mkt_id (v/n), city (v/c), latitude (v/n), longitude (v/n),
#> | airport_city_name (v/c), airport_country_code (v/c), airport_state
#> | (v/c), airport_id (v/n), freq (v/n), weight (e/n), fare_sd (e/n),
#> | itin_fare (e/n), itin_yield (e/n), distance (e/n), year (e/n),
#> | quarter (e/n)
#> + edges from 3db44e5 (vertex names):
#>  [1] ABQ->DFW ABQ->SLC ANC->FAI ANC->SEA ATL->BDL ATL->BOS ATL->BWI ATL->CAE
#>  [9] ATL->CHS ATL->CLT ATL->CVG ATL->DEN ATL->DFW ATL->FLL ATL->FNT ATL->GSP
#> [17] ATL->IAD ATL->IAH ATL->IND ATL->JAX ATL->LAS ATL->LAX ATL->MCO ATL->MKE
#> + ... omitted several edges
#> 
#> $netDir_cap
#>     origin dest passengers fare_sd itin_fare itin_yield distance year quarter
#> 1      ABQ  DFW          4   12.29     96.48 0.16956667      569 2011       1
#> 2      ABQ  SLC          5    0.00    123.50 0.25050000      493 2011       1
#> 3      ANC  FAI          5   34.91     41.38 0.15852500      261 2011       1
#> 4      ANC  SEA          4  154.61    264.77 0.18272500     1449 2011       1
#> 5      ATL  BDL          4  128.04    188.44 0.21937500      859 2011       1
#> 6      ATL  BOS         11  110.84    149.85 0.15840000      946 2011       1
#> 7      ATL  BWI          4   15.84    178.30 0.30955000      576 2011       1
#> 8      ATL  CAE          4   65.18     76.13 0.39860000      191 2011       1
#> 9      ATL  CHS          5   99.34     70.94 0.27390000      259 2011       1
#> 10     ATL  CLT          7   98.21     91.61 0.40355000      227 2011       1
#> 11     ATL  CVG          4   81.28    165.86 0.44466667      373 2011       1
#> 12     ATL  DEN         12   99.20    135.21 0.11277143     1199 2011       1
#> 13     ATL  DFW          4  255.94    290.55 0.39692500      732 2011       1
#> 14     ATL  FLL         37   78.55     89.72 0.15441667      581 2011       1
#> 15     ATL  FNT          7   45.64    100.40 0.15590000      644 2011       1
#> 16     ATL  GSP          4  100.54     88.23 0.57667500      153 2011       1
#> 17     ATL  IAD          4   69.81    177.44 0.33290000      533 2011       1
#> 18     ATL  IAH          4   45.52     84.52 0.12267500      689 2011       1
#> 19     ATL  IND          5  178.98    192.03 0.44452500      432 2011       1
#> 20     ATL  JAX          4   32.77     90.77 0.33620000      270 2011       1
#> 21     ATL  LAS         13  240.35    253.56 0.14514000     1747 2011       1
#> 22     ATL  LAX          5   91.85    202.58 0.10410000     1946 2011       1
#> 23     ATL  MCO         13   48.96     70.12 0.17398750      403 2011       1
#> 24     ATL  MKE         14  114.92    103.25 0.15433333      669 2011       1
#> 25     ATL  MOB          7   25.78     44.40 0.14702500      302 2011       1
#> 26     ATL  MSP          9   87.57    216.84 0.23934000      906 2011       1
#> 27     ATL  MSY         24   13.31    113.90 0.26800000      425 2011       1
#> 28     ATL  ORD          6   49.92    175.66 0.28987500      606 2011       1
#> 29     ATL  PHF          7   31.94     73.41 0.14450000      508 2011       1
#> 30     ATL  PHL          4   80.10    121.66 0.18295000      665 2011       1
#> 31     ATL  PIT          7   48.54     34.32 0.06525000      526 2011       1
#> 32     ATL  RIC          4   28.01     50.19 0.10435000      481 2011       1
#> 33     ATL  ROC          4   75.75     76.66 0.10235000      749 2011       1
#> 34     ATL  RSW          9   36.05     65.11 0.12643333      515 2011       1
#> 35     ATL  SAV          6   32.38     42.84 0.19924000      215 2011       1
#> 36     ATL  SJU          5   75.59    203.51 0.13155000     1547 2011       1
#> 37     ATL  TPA         14  109.36    112.67 0.27750000      406 2011       1
#> 38     ATL  VPS          4   44.37     86.14 0.34456667      250 2011       1
#> 39     AUS  DFW          9   14.37     31.44 0.16548000      190 2011       1
#> 40     BDL  MIA          5    0.00      3.82 0.00320000     1194 2011       1
#> 41     BHM  ATL          5   10.90     38.68 0.28868000      134 2011       1
#> 42     BLI  SEA          4    7.71     30.57 0.32520000       94 2011       1
#> 43     BNA  ATL          5   52.91     73.88 0.34522000      214 2011       1
#> 44     BNA  BWI          4   29.96    126.81 0.21566667      588 2011       1
#> 45     BNA  DFW          4   37.67    116.50 0.18463333      631 2011       1
#> 46     BNA  LGA         21    0.00      2.52 0.00330000      764 2011       1
#> 47     BOI  OAK          4  100.96    202.10 0.39550000      511 2011       1
#> 48     BOI  SEA          4   14.28     44.89 0.11250000      399 2011       1
#> 49     BOS  ATL         12   39.68     97.31 0.10286667      946 2011       1
#> 50     BOS  DCA          4   80.20     98.86 0.24777500      399 2011       1
#> 51     BOS  DFW         11  114.54    224.50 0.14372500     1562 2011       1
#> 52     BOS  JFK         11   66.02     69.95 0.37407500      187 2011       1
#> 53     BOS  MSY          5    0.00    139.02 0.10170000     1367 2011       1
#> 54     BOS  ORD         19   66.28    183.41 0.21155000      867 2011       1
#> 55     BOS  PHL         10   19.94     24.93 0.08903333      280 2011       1
#> 56     BOS  SFO        115   91.78    224.43 0.08300000     2704 2011       1
#> 57     BUF  DTW          4   29.28     39.43 0.16430000      240 2011       1
#> 58     BUF  MCO          5   44.54     79.01 0.07815000     1011 2011       1
#> 59     BWI  ATL          5   11.15     87.11 0.15122500      576 2011       1
#> 60     BWI  BOS          7   55.65     89.49 0.24186000      370 2011       1
#> 61     BWI  CLT          7   37.98     73.14 0.20260000      361 2011       1
#> 62     BWI  MDW          8  103.47    125.74 0.20580000      611 2011       1
#> 63     BWI  MHT          9    1.81     72.80 0.19310000      377 2011       1
#> 64     BWI  ORD          4   84.29     91.40 0.14695000      622 2011       1
#> 65     BWI  PHX          5  165.83    273.26 0.13670000     1999 2011       1
#> 66     CAK  ATL         21   41.92     62.32 0.11803333      528 2011       1
#> 67     CAK  CLT          6    0.00    239.51 0.60790000      394 2011       1
#> 68     CHS  CLT          5   47.93     58.54 0.34842500      168 2011       1
#> 69     CLT  AGS          5   16.39     35.34 0.25243333      140 2011       1
#> 70     CLT  ATL          4   31.28     48.87 0.21530000      227 2011       1
#> 71     CLT  AUS          4    0.00      2.48 0.00240000     1033 2011       1
#> 72     CLT  BUF          4   49.21     59.79 0.10950000      546 2011       1
#> 73     CLT  BWI          5   32.96     69.64 0.19292000      361 2011       1
#> 74     CLT  DCA          4  104.38    139.76 0.42225000      331 2011       1
#> 75     CLT  DFW          4   38.69    167.73 0.17920000      936 2011       1
#> 76     CLT  DTW          4  160.02    221.81 0.44362500      500 2011       1
#> 77     CLT  LGA          9   52.18    106.62 0.19600000      544 2011       1
#> 78     CLT  MCO          4  161.60    120.09 0.25660000      468 2011       1
#> 79     CLT  OAJ          4   10.35     40.71 0.21312500      191 2011       1
#> 80     CLT  ORD          6   94.02    145.01 0.24208000      599 2011       1
#> 81     CLT  ORF          4  166.14    164.99 0.56892500      290 2011       1
#> 82     CLT  PHL          5   87.19     97.35 0.21730000      448 2011       1
#> 83     CLT  PHX          4   80.45    270.67 0.15257500     1774 2011       1
#> 84     CLT  PVD          5   79.67    131.30 0.19224000      683 2011       1
#> 85     CLT  RSW          5  121.12    149.86 0.24976000      600 2011       1
#> 86     CLT  STL          4    8.17    129.70 0.22556667      575 2011       1
#> 87     CLT  TPA          4   44.01     92.60 0.18227500      508 2011       1
#> 88     COS  DEN          4   10.39     25.52 0.34957500       73 2011       1
#> 89     DAL  BNA          4    0.00    312.50 0.50160000      623 2011       1
#> 90     DAL  DEN          9  139.52    177.36 0.27245000      651 2011       1
#> 91     DAL  HOU          7   53.66     97.58 0.40828000      239 2011       1
#> 92     DAY  ATL          6   14.12     64.35 0.14895000      432 2011       1
#> 93     DAY  TPA          8    0.00     79.49 0.09600000      828 2011       1
#> 94     DCA  BOS          5  122.17    201.06 0.50390000      399 2011       1
#> 95     DCA  DEN         25   15.45    188.63 0.12780000     1476 2011       1
#> 96     DCA  DFW          4   64.77    206.19 0.17297500     1192 2011       1
#> 97     DCA  MCO          6   59.08    142.83 0.18818333      759 2011       1
#> 98     DCA  ORD          5   69.35    212.32 0.34693333      612 2011       1
#> 99     DCA  TPA          6   84.50    158.24 0.19440000      814 2011       1
#> 100    DEN  FLL          4   63.73    175.30 0.10293333     1703 2011       1
#> 101    DEN  JAC          4   85.94    121.27 0.29870000      406 2011       1
#> 102    DEN  LAS         20   91.43    120.12 0.19097500      629 2011       1
#> 103    DEN  LAX          4   76.84    147.55 0.17117500      862 2011       1
#> 104    DEN  MCI          4   69.03    107.93 0.20250000      533 2011       1
#> 105    DEN  MCO          4   44.68    150.16 0.09712500     1546 2011       1
#> 106    DEN  MDW         17    4.60     97.58 0.10903333      895 2011       1
#> 107    DEN  MKE         13   16.85    113.88 0.12710000      896 2011       1
#> 108    DEN  MSP          9   94.66    163.74 0.24080000      680 2011       1
#> 109    DEN  OKC          4   19.05     59.39 0.11997500      495 2011       1
#> 110    DEN  OMA          8   41.42     67.77 0.14358000      472 2011       1
#> 111    DEN  ORD          7  246.34    219.89 0.24762500      888 2011       1
#> 112    DEN  PDX          5   52.32     91.54 0.09236667      991 2011       1
#> 113    DEN  PHX         28   52.77    102.50 0.17026000      602 2011       1
#> 114    DEN  SAN          8   64.91    165.45 0.19396000      853 2011       1
#> 115    DEN  SFO          6  116.14    138.78 0.14351667      967 2011       1
#> 116    DEN  SLC          7   40.05     54.03 0.13853333      390 2011       1
#> 117    DEN  SMF          6   93.13    183.82 0.20222500      909 2011       1
#> 118    DEN  SNA          4   55.66    114.40 0.13522500      846 2011       1
#> 119    DEN  TUS          5   39.91     74.75 0.11697500      639 2011       1
#> 120    DFW  ATL          6  119.57    145.88 0.19928333      732 2011       1
#> 121    DFW  BNA          6  130.68    121.42 0.19242000      631 2011       1
#> 122    DFW  CLT          8   76.79    174.94 0.18690000      936 2011       1
#> 123    DFW  DCA         44   25.45    128.97 0.10820000     1192 2011       1
#> 124    DFW  DEN          4  107.72    181.55 0.28322500      641 2011       1
#> 125    DFW  IND          6    0.00     51.28 0.06730000      762 2011       1
#> 126    DFW  LAS          7   41.96    149.45 0.14166000     1055 2011       1
#> 127    DFW  LAX         10   93.09    214.37 0.17357500     1235 2011       1
#> 128    DFW  LGA          6  442.29    547.23 0.39397500     1389 2011       1
#> 129    DFW  OGG          5  267.51    365.41 0.09846667     3711 2011       1
#> 130    DFW  ONT          5   57.76    164.72 0.13865000     1188 2011       1
#> 131    DFW  ORD         12  189.69    184.54 0.23010000      802 2011       1
#> 132    DFW  PHL         11  403.34    409.67 0.31465000     1302 2011       1
#> 133    DFW  PHX          5  130.38    134.92 0.15544000      868 2011       1
#> 134    DFW  SAT          5  201.92    143.65 0.58156000      247 2011       1
#> 135    DFW  SEA          5  120.69    241.57 0.14552500     1660 2011       1
#> 136    DFW  SJC          4   79.98     60.15 0.04180000     1439 2011       1
#> 137    DFW  SJU          8   36.49    222.85 0.10293333     2165 2011       1
#> 138    DFW  SLC          5   93.30     59.04 0.05976000      988 2011       1
#> 139    DFW  SNA         11   43.09    109.86 0.09116667     1205 2011       1
#> 140    DFW  TUS          5  251.17    222.90 0.27417500      813 2011       1
#> 141    DSM  DCA          5    0.00    199.49 0.22240000      897 2011       1
#> 142    DTW  ATL          4   41.39    126.28 0.21260000      594 2011       1
#> 143    DTW  BOS          5    0.00    149.53 0.23660000      632 2011       1
#> 144    DTW  FLL          5   77.42    264.66 0.23484000     1127 2011       1
#> 145    DTW  IAH          7    0.00    153.55 0.14270000     1076 2011       1
#> 146    DTW  MDW          4   20.58    104.46 0.45616667      229 2011       1
#> 147    DTW  MSP          7   18.29     55.49 0.10510000      528 2011       1
#> 148    DTW  ORD          4   48.57     46.00 0.19575000      235 2011       1
#> 149    DTW  PHL          6  409.38    346.67 0.76528000      453 2011       1
#> 150    DTW  RSW          5  129.93    186.05 0.17147500     1085 2011       1
#> 151    ELP  DFW          6   63.06    117.99 0.21413333      551 2011       1
#> 152    EWR  BOS         21  249.80    149.61 0.74803333      200 2011       1
#> 153    EWR  LAS          4    0.00    328.48 0.14750000     2227 2011       1
#> 154    EWR  MCO         13   47.56    114.86 0.12245000      938 2011       1
#> 155    EWR  SEA          5   23.71    210.65 0.08773333     2401 2011       1
#> 156    FLL  ATL          8   64.29    101.38 0.17448571      581 2011       1
#> 157    FLL  CLE         10   48.23    234.35 0.22066667     1062 2011       1
#> 158    FLL  CLT          5   78.43    129.92 0.20590000      631 2011       1
#> 159    FLL  JFK         26   80.62    160.67 0.15030000     1069 2011       1
#> 160    FLL  LGA          6    0.00    139.02 0.12920000     1076 2011       1
#> 161    FLL  MCI          6    0.00    129.54 0.10430000     1242 2011       1
#> 162    FLL  PHL          5   80.74     60.96 0.06145000      992 2011       1
#> 163    FLL  TPA          4   17.40     13.07 0.06635000      197 2011       1
#> 164    GEG  SLC          4   85.82    169.88 0.31113333      546 2011       1
#> 165    GRB  MSP          4    9.56     47.22 0.18740000      252 2011       1
#> 166    GRR  ORD          4   51.84     49.93 0.36443333      137 2011       1
#> 167    HNL  KOA          8   37.43     45.38 0.27843333      163 2011       1
#> 168    HNL  LAX         10  126.31    193.43 0.07567500     2556 2011       1
#> 169    HNL  LIH          5   20.40     24.38 0.23902500      102 2011       1
#> 170    HNL  SEA          5  121.15    154.20 0.05760000     2677 2011       1
#> 171    HPN  RSW         22    0.00    140.95 0.12790000     1102 2011       1
#> 172    IAD  DEN          6   92.07    176.03 0.12123333     1452 2011       1
#> 173    IAD  SEA          4    0.00    457.97 0.19860000     2306 2011       1
#> 174    IAD  SFO          5  216.71    393.91 0.16284000     2419 2011       1
#> 175    IAD  SLC         12    0.00    214.49 0.11740000     1827 2011       1
#> 176    IAH  ATL          5   43.13    109.76 0.15930000      689 2011       1
#> 177    IAH  AUS          4   17.31     29.11 0.20790000      140 2011       1
#> 178    IAH  CLT          6   46.45    134.24 0.14703333      913 2011       1
#> 179    IAH  FLL          6  124.02    123.98 0.12847500      965 2011       1
#> 180    IAH  HRL          4   33.38     63.72 0.21600000      295 2011       1
#> 181    IAH  LAS         20  123.56    241.47 0.19760000     1222 2011       1
#> 182    IAH  MCI          4  184.91    217.24 0.33785000      643 2011       1
#> 183    IAH  MCO          4   59.62    140.34 0.16452500      853 2011       1
#> 184    IAH  MSY         12  140.36    123.68 0.40550000      305 2011       1
#> 185    IAH  ORD         16  329.13    232.73 0.25160000      925 2011       1
#> 186    IAH  SAT          4   34.93     45.98 0.24075000      191 2011       1
#> 187    IAH  SFO          4   18.12    143.19 0.08757500     1635 2011       1
#> 188    IND  ATL          9   65.69     80.64 0.18667500      432 2011       1
#> 189    IND  DFW          4    0.00    147.98 0.19420000      762 2011       1
#> 190    IND  MCO          6    0.00     90.50 0.10930000      828 2011       1
#> 191    JAX  BWI          5   76.07    109.81 0.16563333      663 2011       1
#> 192    JAX  LGA          5    0.00    130.52 0.15650000      834 2011       1
#> 193    JFK  BUF          4   42.39     69.00 0.22925000      301 2011       1
#> 194    JFK  FLL          9   63.80     49.07 0.04590000     1069 2011       1
#> 195    JFK  LGA          4    0.52      1.25 0.11392500       11 2011       1
#> 196    JFK  MSP          9    0.00      2.47 0.00240000     1028 2011       1
#> 197    JFK  SFO          5  166.84    351.33 0.13586000     2586 2011       1
#> 198    JFK  SJU          7    0.00    228.05 0.14280000     1597 2011       1
#> 199    JFK  TPA         13    0.00    191.45 0.19050000     1005 2011       1
#> 200    LAN  ORD          7   70.65     83.58 0.46690000      179 2011       1
#> 201    LAS  ATL          6   49.01    147.62 0.08450000     1747 2011       1
#> 202    LAS  BLI         11    0.00     97.98 0.10270000      954 2011       1
#> 203    LAS  DEN         22  110.73    124.76 0.19835000      629 2011       1
#> 204    LAS  DFW          5  166.36    148.49 0.14075000     1055 2011       1
#> 205    LAS  DTW         10   75.12    258.00 0.14742857     1750 2011       1
#> 206    LAS  EWR         20    0.00    224.04 0.10060000     2227 2011       1
#> 207    LAS  FCA          4    0.00     71.99 0.08510000      846 2011       1
#> 208    LAS  IND          4   42.98    159.10 0.10000000     1591 2011       1
#> 209    LAS  LAX         13   84.84    102.13 0.43273333      236 2011       1
#> 210    LAS  LGB          4   62.12     82.09 0.35535000      231 2011       1
#> 211    LAS  MDW         16   63.24    163.81 0.10770000     1521 2011       1
#> 212    LAS  MSP         12  225.21    298.74 0.22980000     1300 2011       1
#> 213    LAS  OAK          5   48.15    100.60 0.24716667      407 2011       1
#> 214    LAS  ORD          6   44.27    199.07 0.13140000     1515 2011       1
#> 215    LAS  PDX         20    0.00     94.03 0.12340000      762 2011       1
#> 216    LAS  PHX          4   27.82     71.53 0.27942500      256 2011       1
#> 217    LAS  SEA          8   36.44    128.73 0.14865000      866 2011       1
#> 218    LAS  SFO          7   41.84    138.21 0.33384000      414 2011       1
#> 219    LAS  SHV          7    0.00     61.95 0.04980000     1244 2011       1
#> 220    LAX  ATL         16  163.62    181.35 0.09319286     1946 2011       1
#> 221    LAX  CLT          5  162.27    284.43 0.13385000     2125 2011       1
#> 222    LAX  DEN          8   58.42    131.07 0.15205000      862 2011       1
#> 223    LAX  DFW          4   94.21    168.70 0.13660000     1235 2011       1
#> 224    LAX  DTW          4  125.74    156.49 0.07907500     1979 2011       1
#> 225    LAX  IAH          6  474.97    379.11 0.27492000     1379 2011       1
#> 226    LAX  JFK        137  203.64    322.86 0.13045000     2475 2011       1
#> 227    LAX  LIH          4  177.33    129.31 0.04945000     2615 2011       1
#> 228    LAX  MIA          4   90.11    305.28 0.13035000     2342 2011       1
#> 229    LAX  OGG          5   61.75    238.10 0.09577500     2486 2011       1
#> 230    LAX  ORD          6  138.38     91.23 0.05228333     1745 2011       1
#> 231    LAX  PHX          5   56.65     91.95 0.24850000      370 2011       1
#> 232    LAX  SEA         17  116.76    201.34 0.21105000      954 2011       1
#> 233    LAX  SFO         14   56.95     61.07 0.18122500      337 2011       1
#> 234    LGA  ATL          8   67.38    154.50 0.20302000      761 2011       1
#> 235    LGA  BOS         10  108.64    221.97 1.19985000      185 2011       1
#> 236    LGA  CAK          4    0.00    313.99 0.79290000      396 2011       1
#> 237    LGA  CLT         10   33.67     86.18 0.15842500      544 2011       1
#> 238    LGA  CRW          5    0.00    143.50 0.32320000      444 2011       1
#> 239    LGA  ORD         55   85.24     80.87 0.11033333      733 2011       1
#> 240    LGA  TPA          5  189.37    136.43 0.13495000     1011 2011       1
#> 241    LIH  HNL          5   17.83     23.30 0.22842500      102 2011       1
#> 242    LIH  LAX          5  171.33    189.41 0.07243333     2615 2011       1
#> 243    MCI  DFW          6   29.26     33.56 0.07296667      460 2011       1
#> 244    MCI  HOU          5    0.00      2.00 0.00300000      666 2011       1
#> 245    MCI  LGA          5    0.00    144.46 0.13050000     1107 2011       1
#> 246    MCI  MKE          7   71.04     73.73 0.16910000      436 2011       1
#> 247    MCI  PHL          4    0.00    328.53 0.31650000     1038 2011       1
#> 248    MCO  ATL         12  148.40    114.22 0.28342500      403 2011       1
#> 249    MCO  CLT          4  145.14    187.28 0.40017500      468 2011       1
#> 250    MCO  DEN          4  120.75    173.46 0.11220000     1546 2011       1
#> 251    MCO  DFW          6   21.62    114.44 0.11630000      984 2011       1
#> 252    MCO  DTW          7  100.08     77.76 0.08125000      957 2011       1
#> 253    MCO  EWR          4   81.25    247.35 0.26370000      938 2011       1
#> 254    MCO  FLL          8   42.78     69.25 0.38905000      178 2011       1
#> 255    MCO  FNT         20    0.00     84.52 0.08360000     1011 2011       1
#> 256    MCO  HOU          6  140.73    102.82 0.12125000      848 2011       1
#> 257    MCO  HPN         17    0.00    120.04 0.12350000      972 2011       1
#> 258    MCO  IAH          8   34.21     97.48 0.11428000      853 2011       1
#> 259    MCO  IND          7    0.00    105.98 0.12800000      828 2011       1
#> 260    MCO  MHT         17    0.00    164.45 0.14400000     1142 2011       1
#> 261    MCO  MSP         18   41.13    188.84 0.14415000     1310 2011       1
#> 262    MCO  ORD          7  121.59    139.15 0.13846000     1005 2011       1
#> 263    MCO  PHL          6   42.86    119.97 0.13933333      861 2011       1
#> 264    MDT  MCO          6    0.00     99.48 0.11690000      851 2011       1
#> 265    MDW  CMH          4   53.06     60.75 0.21390000      284 2011       1
#> 266    MDW  ISP         12  141.08    221.77 0.28990000      765 2011       1
#> 267    MDW  MHT          4   79.72    158.91 0.18963333      838 2011       1
#> 268    MEM  ATL         15   38.44     66.61 0.20063333      332 2011       1
#> 269    MEM  LGA          4  124.57    247.91 0.25743333      963 2011       1
#> 270    MEM  TUL          4   54.54     86.41 0.25267500      342 2011       1
#> 271    MIA  CVG          5    0.00    182.49 0.19250000      948 2011       1
#> 272    MIA  DCA          6   53.55    105.43 0.11460000      920 2011       1
#> 273    MIA  DFW          4   82.71    109.19 0.09740000     1121 2011       1
#> 274    MIA  DTW          4  122.42     90.46 0.07900000     1145 2011       1
#> 275    MIA  JFK         28  111.79    213.35 0.19573333     1090 2011       1
#> 276    MIA  LGA          6  103.49    173.27 0.15795000     1097 2011       1
#> 277    MIA  ORD          4   56.96    233.71 0.19525000     1197 2011       1
#> 278    MIA  SFO          4   21.02    260.96 0.10095000     2585 2011       1
#> 279    MIA  SJU          8  311.91    288.18 0.27576667     1045 2011       1
#> 280    MKE  DEN          4   80.26    103.42 0.11542500      896 2011       1
#> 281    MKE  DFW          7  142.17    226.00 0.26495000      853 2011       1
#> 282    MSP  ATL          6   81.95     72.21 0.07970000      906 2011       1
#> 283    MSP  DEN          6   60.17    100.69 0.14808000      680 2011       1
#> 284    MSP  DFW          7  141.11    240.69 0.28250000      852 2011       1
#> 285    MSP  DTW          7   11.96     76.03 0.14400000      528 2011       1
#> 286    MSP  MCI          5  100.63    314.38 0.79996000      393 2011       1
#> 287    MSP  MCO          7   29.08    152.57 0.11646667     1310 2011       1
#> 288    MSP  ORD          4   63.83     76.98 0.23046667      334 2011       1
#> 289    MSP  PHX          4   71.99    164.44 0.12887500     1276 2011       1
#> 290    MSY  ATL          7   56.29     85.57 0.20135000      425 2011       1
#> 291    MSY  HOU         18   37.13    117.82 0.38883333      303 2011       1
#> 292    MSY  MDW          8    0.00    159.47 0.19330000      825 2011       1
#> 293    OAK  ABQ          9    0.00    135.48 0.15240000      889 2011       1
#> 294    OAK  PHX          6   90.95    135.57 0.20986000      646 2011       1
#> 295    OGG  LAX          7  104.76     71.43 0.02873333     2486 2011       1
#> 296    OGG  PDX          4   55.25    221.48 0.08645000     2562 2011       1
#> 297    OKC  DFW          9    4.10     48.10 0.27485000      175 2011       1
#> 298    OKC  IAH          4  137.37    148.43 0.37577500      395 2011       1
#> 299    OMA  DEN          4    0.00    156.00 0.33050000      472 2011       1
#> 300    OMA  PHX          5   87.07    162.06 0.15627500     1037 2011       1
#> 301    ORD  BNA          5   68.36     78.37 0.19162000      409 2011       1
#> 302    ORD  BOS          5   58.47     82.49 0.09514000      867 2011       1
#> 303    ORD  BWI          5   91.14    165.08 0.26540000      622 2011       1
#> 304    ORD  CMH          4  113.96     89.98 0.30400000      296 2011       1
#> 305    ORD  DCA          5   14.31     59.94 0.09794000      612 2011       1
#> 306    ORD  DEN          4  179.91    241.65 0.27212500      888 2011       1
#> 307    ORD  DFW          4   56.17    111.16 0.13860000      802 2011       1
#> 308    ORD  DSM          4  188.91    122.20 0.40870000      299 2011       1
#> 309    ORD  DTW          6   63.49    101.52 0.43202000      235 2011       1
#> 310    ORD  EWR          8  263.96    274.74 0.38212000      719 2011       1
#> 311    ORD  LAX          7  167.84    327.84 0.18787143     1745 2011       1
#> 312    ORD  LGA          6  105.32    169.29 0.23095000      733 2011       1
#> 313    ORD  MIA          4   29.50    165.16 0.13797500     1197 2011       1
#> 314    ORD  MSP          5   76.90    131.56 0.39388000      334 2011       1
#> 315    ORD  MSY          4   50.89    147.06 0.17570000      837 2011       1
#> 316    ORD  PHL          4   68.94     55.80 0.08230000      678 2011       1
#> 317    ORD  RSW         16   82.88    229.29 0.20472500     1120 2011       1
#> 318    ORD  SAN          6   79.92    174.32 0.10117500     1723 2011       1
#> 319    ORD  SEA          7  118.27    211.63 0.12296667     1721 2011       1
#> 320    ORD  SFO          5   99.97    160.68 0.08704000     1846 2011       1
#> 321    ORD  STL          5   16.80     54.65 0.21182000      258 2011       1
#> 322    PBI  ATL          6   33.75     74.95 0.13751667      545 2011       1
#> 323    PDX  LAX          4   50.74    131.25 0.15737500      834 2011       1
#> 324    PDX  SEA          8   66.46     59.36 0.46015000      129 2011       1
#> 325    PDX  SNA          4    0.00    205.47 0.23920000      859 2011       1
#> 326    PHL  DEN          9  170.78    216.82 0.13925556     1557 2011       1
#> 327    PHL  DFW          6   79.40    215.84 0.16577500     1302 2011       1
#> 328    PHL  MCO          5   13.09    186.28 0.21635000      861 2011       1
#> 329    PHL  MSP          5  138.09    174.68 0.17824000      980 2011       1
#> 330    PHL  ORD          5   33.98    137.31 0.20252500      678 2011       1
#> 331    PHL  PHX          5  120.17    197.62 0.09524000     2075 2011       1
#> 332    PHL  RDU         17    0.00      2.02 0.00600000      336 2011       1
#> 333    PHX  ATL          7   74.21    153.26 0.09657143     1587 2011       1
#> 334    PHX  DCA          5  312.20    510.29 0.25785000     1979 2011       1
#> 335    PHX  DFW          4   50.04     94.89 0.10932500      868 2011       1
#> 336    PHX  DTW          5   95.02    206.93 0.12383333     1671 2011       1
#> 337    PHX  EWR          5   95.00    291.37 0.13660000     2133 2011       1
#> 338    PHX  GJT          5   81.44    146.35 0.33413333      438 2011       1
#> 339    PHX  IAH          5   74.62    203.88 0.20206000     1009 2011       1
#> 340    PHX  LAX          9   51.50     78.76 0.21287778      370 2011       1
#> 341    PHX  MSP          6   74.07    131.58 0.10312000     1276 2011       1
#> 342    PHX  OAK          4  186.64    133.53 0.20670000      646 2011       1
#> 343    PHX  OMA          4  115.34    245.33 0.23657500     1037 2011       1
#> 344    PHX  ORD          6   27.19    146.23 0.10155000     1440 2011       1
#> 345    PHX  PDX         35   60.36     86.61 0.08583333     1009 2011       1
#> 346    PHX  PIT          5   74.98    213.25 0.11762000     1813 2011       1
#> 347    PHX  PVD          4   85.01     64.44 0.02830000     2277 2011       1
#> 348    PHX  RNO          4   12.19     73.44 0.12220000      601 2011       1
#> 349    PHX  SAN          4   49.78     53.02 0.17440000      304 2011       1
#> 350    PHX  SEA         14   75.69    317.89 0.28716667     1107 2011       1
#> 351    PHX  SLC          8   54.40     80.82 0.15941667      507 2011       1
#> 352    PIE  CID          5    0.00    130.47 0.11970000     1090 2011       1
#> 353    PIT  MIA          4    0.00    177.98 0.17570000     1013 2011       1
#> 354    PNS  ATL          6   20.73     45.70 0.16801667      272 2011       1
#> 355    PSE  JFK          4    0.00    182.56 0.11290000     1617 2011       1
#> 356    PSP  PHX          4    0.00    115.23 0.44150000      261 2011       1
#> 357    RDU  ATL          7   80.20    102.78 0.28870000      356 2011       1
#> 358    RIC  CLT          6   24.85     70.50 0.27540000      256 2011       1
#> 359    RNO  LAS          7    0.00    200.51 0.58120000      345 2011       1
#> 360    ROC  ATL          4   43.01     95.20 0.12710000      749 2011       1
#> 361    RSW  BOS          6  156.94    238.00 0.19055000     1249 2011       1
#> 362    RSW  BWI         10    0.00    161.47 0.17570000      919 2011       1
#> 363    RSW  IAH          4   56.19    108.79 0.12635000      861 2011       1
#> 364    RSW  MSP          4    0.00    160.01 0.11300000     1416 2011       1
#> 365    SAN  DEN          4   47.06    129.61 0.15195000      853 2011       1
#> 366    SAN  MSP         13    0.00    242.52 0.15830000     1532 2011       1
#> 367    SAN  ORD          4  206.76    272.10 0.15792500     1723 2011       1
#> 368    SAN  PHX         11   30.69     48.27 0.15876667      304 2011       1
#> 369    SAT  DAL          6    0.60     98.43 0.39690000      248 2011       1
#> 370    SAT  DFW          5  157.67    112.75 0.45647500      247 2011       1
#> 371    SAT  MDW          4   34.06    140.45 0.13556667     1036 2011       1
#> 372    SAT  MSP          4  114.88     84.30 0.07685000     1097 2011       1
#> 373    SEA  ANC          6  229.46    253.38 0.17486667     1449 2011       1
#> 374    SEA  BUR          4   66.12    157.23 0.16780000      937 2011       1
#> 375    SEA  DFW          8  245.58    306.38 0.18456667     1660 2011       1
#> 376    SEA  HNL          4   49.46    199.88 0.07466667     2677 2011       1
#> 377    SEA  JFK         33   23.53    185.29 0.07653333     2421 2011       1
#> 378    SEA  LAS          4    0.00    142.46 0.16450000      866 2011       1
#> 379    SEA  OAK          4   89.48     71.73 0.10690000      671 2011       1
#> 380    SEA  PHX          4   86.07    130.32 0.11772500     1107 2011       1
#> 381    SEA  RNO         13   58.86     90.86 0.16110000      564 2011       1
#> 382    SEA  SAN          8  101.28     88.10 0.08390000     1050 2011       1
#> 383    SFO  BOS         14  136.93    249.58 0.09230000     2704 2011       1
#> 384    SFO  DEN          8   47.64    164.27 0.16987500      967 2011       1
#> 385    SFO  HNL          4  202.32    159.69 0.06656667     2399 2011       1
#> 386    SFO  JFK          4  461.16    488.75 0.18900000     2586 2011       1
#> 387    SFO  LAS          7  105.81    166.26 0.40160000      414 2011       1
#> 388    SFO  LAX          6   56.80    100.85 0.29926667      337 2011       1
#> 389    SFO  ORD         18  126.64    203.56 0.11027000     1846 2011       1
#> 390    SFO  PHL          5  309.82    413.44 0.16400000     2521 2011       1
#> 391    SFO  SEA          5   18.19     52.35 0.07710000      679 2011       1
#> 392    SFO  SNA         14   61.98    125.80 0.33818000      372 2011       1
#> 393    SJU  ATL          7   78.59    195.26 0.12622000     1547 2011       1
#> 394    SJU  FLL          6   37.20    102.98 0.09845000     1046 2011       1
#> 395    SLC  DEN          9   32.67     43.89 0.11253333      390 2011       1
#> 396    SLC  HNL          4   80.91    193.41 0.06460000     2994 2011       1
#> 397    SLC  IAD          6  217.04    407.97 0.22330000     1827 2011       1
#> 398    SLC  MDW          5   14.77    141.02 0.11210000     1258 2011       1
#> 399    SLC  PDX         14   28.02     74.69 0.11855000      630 2011       1
#> 400    SLC  PHX          4   72.11    100.28 0.19780000      507 2011       1
#> 401    SMF  DEN          9   37.05    149.24 0.16418000      909 2011       1
#> 402    SNA  DEN          5  273.68    291.64 0.34473333      846 2011       1
#> 403    SNA  DFW          6   19.71    109.90 0.09120000     1205 2011       1
#> 404    SNA  SEA         15   37.10    196.63 0.20105000      978 2011       1
#> 405    STL  DFW         18  166.92    114.18 0.20722500      551 2011       1
#> 406    STL  DTW          4   87.08    186.00 0.42273333      440 2011       1
#> 407    STL  LIT         10   70.45    117.69 0.39760000      296 2011       1
#> 408    STL  OKC          4   51.97    156.66 0.33910000      462 2011       1
#> 409    STL  PHX          7   38.55    214.29 0.16980000     1262 2011       1
#> 410    STT  CLT          4   33.32    121.30 0.07980000     1520 2011       1
#> 411    TPA  ATL          7   43.59     73.47 0.18096667      406 2011       1
#> 412    TPA  DFW          6   49.23     82.09 0.08836667      929 2011       1
#> 413    TPA  FLL         14    0.00     39.50 0.20050000      197 2011       1
#> 414    TPA  ISP          7    0.00     89.54 0.08660000     1034 2011       1
#> 415    TPA  MIA         12    0.00     83.50 0.40930000      204 2011       1
#> 416    TPA  STL          4   57.64    229.76 0.26440000      869 2011       1
#> 417    TYS  ATL          4   25.78     35.11 0.23100000      152 2011       1
#> 418    TYS  CLT          5   25.71     62.88 0.35524000      177 2011       1
#>     origin_city_mkt_id                           origin_city dest_city_mkt_id
#> 1                30140                       Albuquerque, NM            30194
#> 2                30140                       Albuquerque, NM            34614
#> 3                30299                         Anchorage, AK            31517
#> 4                30299                         Anchorage, AK            30559
#> 5                30397       Atlanta, GA (Metropolitan Area)            30529
#> 6                30397       Atlanta, GA (Metropolitan Area)            30721
#> 7                30397       Atlanta, GA (Metropolitan Area)            30852
#> 8                30397       Atlanta, GA (Metropolitan Area)            30868
#> 9                30397       Atlanta, GA (Metropolitan Area)            30994
#> 10               30397       Atlanta, GA (Metropolitan Area)            31057
#> 11               30397       Atlanta, GA (Metropolitan Area)            33105
#> 12               30397       Atlanta, GA (Metropolitan Area)            30325
#> 13               30397       Atlanta, GA (Metropolitan Area)            30194
#> 14               30397       Atlanta, GA (Metropolitan Area)            32467
#> 15               30397       Atlanta, GA (Metropolitan Area)            31721
#> 16               30397       Atlanta, GA (Metropolitan Area)            31871
#> 17               30397       Atlanta, GA (Metropolitan Area)            30852
#> 18               30397       Atlanta, GA (Metropolitan Area)            31453
#> 19               30397       Atlanta, GA (Metropolitan Area)            32337
#> 20               30397       Atlanta, GA (Metropolitan Area)            31136
#> 21               30397       Atlanta, GA (Metropolitan Area)            32211
#> 22               30397       Atlanta, GA (Metropolitan Area)            32575
#> 23               30397       Atlanta, GA (Metropolitan Area)            31454
#> 24               30397       Atlanta, GA (Metropolitan Area)            33342
#> 25               30397       Atlanta, GA (Metropolitan Area)            30562
#> 26               30397       Atlanta, GA (Metropolitan Area)            31650
#> 27               30397       Atlanta, GA (Metropolitan Area)            33495
#> 28               30397       Atlanta, GA (Metropolitan Area)            30977
#> 29               30397       Atlanta, GA (Metropolitan Area)            33667
#> 30               30397       Atlanta, GA (Metropolitan Area)            34100
#> 31               30397       Atlanta, GA (Metropolitan Area)            30198
#> 32               30397       Atlanta, GA (Metropolitan Area)            34524
#> 33               30397       Atlanta, GA (Metropolitan Area)            34576
#> 34               30397       Atlanta, GA (Metropolitan Area)            31714
#> 35               30397       Atlanta, GA (Metropolitan Area)            34685
#> 36               30397       Atlanta, GA (Metropolitan Area)            34819
#> 37               30397       Atlanta, GA (Metropolitan Area)            33195
#> 38               30397       Atlanta, GA (Metropolitan Area)            31504
#> 39               30423                            Austin, TX            30194
#> 40               30529                          Hartford, CT            32467
#> 41               30599                        Birmingham, AL            30397
#> 42               30666                        Bellingham, WA            30559
#> 43               30693                         Nashville, TN            30397
#> 44               30693                         Nashville, TN            30852
#> 45               30693                         Nashville, TN            30194
#> 46               30693                         Nashville, TN            31703
#> 47               30713                             Boise, ID            32457
#> 48               30713                             Boise, ID            30559
#> 49               30721        Boston, MA (Metropolitan Area)            30397
#> 50               30721        Boston, MA (Metropolitan Area)            30852
#> 51               30721        Boston, MA (Metropolitan Area)            30194
#> 52               30721        Boston, MA (Metropolitan Area)            31703
#> 53               30721        Boston, MA (Metropolitan Area)            33495
#> 54               30721        Boston, MA (Metropolitan Area)            30977
#> 55               30721        Boston, MA (Metropolitan Area)            34100
#> 56               30721        Boston, MA (Metropolitan Area)            32457
#> 57               30792                           Buffalo, NY            31295
#> 58               30792                           Buffalo, NY            31454
#> 59               30852    Washington, DC (Metropolitan Area)            30397
#> 60               30852    Washington, DC (Metropolitan Area)            30721
#> 61               30852    Washington, DC (Metropolitan Area)            31057
#> 62               30852    Washington, DC (Metropolitan Area)            30977
#> 63               30852    Washington, DC (Metropolitan Area)            30721
#> 64               30852    Washington, DC (Metropolitan Area)            30977
#> 65               30852    Washington, DC (Metropolitan Area)            30466
#> 66               30647     Cleveland, OH (Metropolitan Area)            30397
#> 67               30647     Cleveland, OH (Metropolitan Area)            31057
#> 68               30994                        Charleston, SC            31057
#> 69               31057                         Charlotte, NC            30208
#> 70               31057                         Charlotte, NC            30397
#> 71               31057                         Charlotte, NC            30423
#> 72               31057                         Charlotte, NC            30792
#> 73               31057                         Charlotte, NC            30852
#> 74               31057                         Charlotte, NC            30852
#> 75               31057                         Charlotte, NC            30194
#> 76               31057                         Charlotte, NC            31295
#> 77               31057                         Charlotte, NC            31703
#> 78               31057                         Charlotte, NC            31454
#> 79               31057                         Charlotte, NC            33795
#> 80               31057                         Charlotte, NC            30977
#> 81               31057                         Charlotte, NC            33667
#> 82               31057                         Charlotte, NC            34100
#> 83               31057                         Charlotte, NC            30466
#> 84               31057                         Charlotte, NC            30721
#> 85               31057                         Charlotte, NC            31714
#> 86               31057                         Charlotte, NC            31123
#> 87               31057                         Charlotte, NC            33195
#> 88               30189                  Colorado Springs, CO            30325
#> 89               30194                 Dallas/Fort Worth, TX            30693
#> 90               30194                 Dallas/Fort Worth, TX            30325
#> 91               30194                 Dallas/Fort Worth, TX            31453
#> 92               31267                            Dayton, OH            30397
#> 93               31267                            Dayton, OH            33195
#> 94               30852    Washington, DC (Metropolitan Area)            30721
#> 95               30852    Washington, DC (Metropolitan Area)            30325
#> 96               30852    Washington, DC (Metropolitan Area)            30194
#> 97               30852    Washington, DC (Metropolitan Area)            31454
#> 98               30852    Washington, DC (Metropolitan Area)            30977
#> 99               30852    Washington, DC (Metropolitan Area)            33195
#> 100              30325                            Denver, CO            32467
#> 101              30325                            Denver, CO            32441
#> 102              30325                            Denver, CO            32211
#> 103              30325                            Denver, CO            32575
#> 104              30325                            Denver, CO            33198
#> 105              30325                            Denver, CO            31454
#> 106              30325                            Denver, CO            30977
#> 107              30325                            Denver, CO            33342
#> 108              30325                            Denver, CO            31650
#> 109              30325                            Denver, CO            33851
#> 110              30325                            Denver, CO            33316
#> 111              30325                            Denver, CO            30977
#> 112              30325                            Denver, CO            34057
#> 113              30325                            Denver, CO            30466
#> 114              30325                            Denver, CO            33570
#> 115              30325                            Denver, CO            32457
#> 116              30325                            Denver, CO            34614
#> 117              30325                            Denver, CO            33192
#> 118              30325                            Denver, CO            32575
#> 119              30325                            Denver, CO            30436
#> 120              30194                 Dallas/Fort Worth, TX            30397
#> 121              30194                 Dallas/Fort Worth, TX            30693
#> 122              30194                 Dallas/Fort Worth, TX            31057
#> 123              30194                 Dallas/Fort Worth, TX            30852
#> 124              30194                 Dallas/Fort Worth, TX            30325
#> 125              30194                 Dallas/Fort Worth, TX            32337
#> 126              30194                 Dallas/Fort Worth, TX            32211
#> 127              30194                 Dallas/Fort Worth, TX            32575
#> 128              30194                 Dallas/Fort Worth, TX            31703
#> 129              30194                 Dallas/Fort Worth, TX            33830
#> 130              30194                 Dallas/Fort Worth, TX            32575
#> 131              30194                 Dallas/Fort Worth, TX            30977
#> 132              30194                 Dallas/Fort Worth, TX            34100
#> 133              30194                 Dallas/Fort Worth, TX            30466
#> 134              30194                 Dallas/Fort Worth, TX            33214
#> 135              30194                 Dallas/Fort Worth, TX            30559
#> 136              30194                 Dallas/Fort Worth, TX            32457
#> 137              30194                 Dallas/Fort Worth, TX            34819
#> 138              30194                 Dallas/Fort Worth, TX            34614
#> 139              30194                 Dallas/Fort Worth, TX            32575
#> 140              30194                 Dallas/Fort Worth, TX            30436
#> 141              31423                        Des Moines, IA            30852
#> 142              31295                           Detroit, MI            30397
#> 143              31295                           Detroit, MI            30721
#> 144              31295                           Detroit, MI            32467
#> 145              31295                           Detroit, MI            31453
#> 146              31295                           Detroit, MI            30977
#> 147              31295                           Detroit, MI            31650
#> 148              31295                           Detroit, MI            30977
#> 149              31295                           Detroit, MI            34100
#> 150              31295                           Detroit, MI            31714
#> 151              30615                           El Paso, TX            30194
#> 152              31703 New York City, NY (Metropolitan Area)            30721
#> 153              31703 New York City, NY (Metropolitan Area)            32211
#> 154              31703 New York City, NY (Metropolitan Area)            31454
#> 155              31703 New York City, NY (Metropolitan Area)            30559
#> 156              32467         Miami, FL (Metropolitan Area)            30397
#> 157              32467         Miami, FL (Metropolitan Area)            30647
#> 158              32467         Miami, FL (Metropolitan Area)            31057
#> 159              32467         Miami, FL (Metropolitan Area)            31703
#> 160              32467         Miami, FL (Metropolitan Area)            31703
#> 161              32467         Miami, FL (Metropolitan Area)            33198
#> 162              32467         Miami, FL (Metropolitan Area)            34100
#> 163              32467         Miami, FL (Metropolitan Area)            33195
#> 164              31884                           Spokane, WA            34614
#> 165              31977                         Green Bay, WI            31650
#> 166              31986                      Grand Rapids, MI            30977
#> 167              32134                          Honolulu, HI            32758
#> 168              32134                          Honolulu, HI            32575
#> 169              32134                          Honolulu, HI            32982
#> 170              32134                          Honolulu, HI            30559
#> 171              31703 New York City, NY (Metropolitan Area)            31714
#> 172              30852    Washington, DC (Metropolitan Area)            30325
#> 173              30852    Washington, DC (Metropolitan Area)            30559
#> 174              30852    Washington, DC (Metropolitan Area)            32457
#> 175              30852    Washington, DC (Metropolitan Area)            34614
#> 176              31453                           Houston, TX            30397
#> 177              31453                           Houston, TX            30423
#> 178              31453                           Houston, TX            31057
#> 179              31453                           Houston, TX            32467
#> 180              31453                           Houston, TX            32206
#> 181              31453                           Houston, TX            32211
#> 182              31453                           Houston, TX            33198
#> 183              31453                           Houston, TX            31454
#> 184              31453                           Houston, TX            33495
#> 185              31453                           Houston, TX            30977
#> 186              31453                           Houston, TX            33214
#> 187              31453                           Houston, TX            32457
#> 188              32337                      Indianapolis, IN            30397
#> 189              32337                      Indianapolis, IN            30194
#> 190              32337                      Indianapolis, IN            31454
#> 191              31136                      Jacksonville, FL            30852
#> 192              31136                      Jacksonville, FL            31703
#> 193              31703 New York City, NY (Metropolitan Area)            30792
#> 194              31703 New York City, NY (Metropolitan Area)            32467
#> 195              31703 New York City, NY (Metropolitan Area)            31703
#> 196              31703 New York City, NY (Metropolitan Area)            31650
#> 197              31703 New York City, NY (Metropolitan Area)            32457
#> 198              31703 New York City, NY (Metropolitan Area)            34819
#> 199              31703 New York City, NY (Metropolitan Area)            33195
#> 200              32884                           Lansing, MI            30977
#> 201              32211                         Las Vegas, NV            30397
#> 202              32211                         Las Vegas, NV            30666
#> 203              32211                         Las Vegas, NV            30325
#> 204              32211                         Las Vegas, NV            30194
#> 205              32211                         Las Vegas, NV            31295
#> 206              32211                         Las Vegas, NV            31703
#> 207              32211                         Las Vegas, NV            31648
#> 208              32211                         Las Vegas, NV            32337
#> 209              32211                         Las Vegas, NV            32575
#> 210              32211                         Las Vegas, NV            32575
#> 211              32211                         Las Vegas, NV            30977
#> 212              32211                         Las Vegas, NV            31650
#> 213              32211                         Las Vegas, NV            32457
#> 214              32211                         Las Vegas, NV            30977
#> 215              32211                         Las Vegas, NV            34057
#> 216              32211                         Las Vegas, NV            30466
#> 217              32211                         Las Vegas, NV            30559
#> 218              32211                         Las Vegas, NV            32457
#> 219              32211                         Las Vegas, NV            30476
#> 220              32575   Los Angeles, CA (Metropolitan Area)            30397
#> 221              32575   Los Angeles, CA (Metropolitan Area)            31057
#> 222              32575   Los Angeles, CA (Metropolitan Area)            30325
#> 223              32575   Los Angeles, CA (Metropolitan Area)            30194
#> 224              32575   Los Angeles, CA (Metropolitan Area)            31295
#> 225              32575   Los Angeles, CA (Metropolitan Area)            31453
#> 226              32575   Los Angeles, CA (Metropolitan Area)            31703
#> 227              32575   Los Angeles, CA (Metropolitan Area)            32982
#> 228              32575   Los Angeles, CA (Metropolitan Area)            32467
#> 229              32575   Los Angeles, CA (Metropolitan Area)            33830
#> 230              32575   Los Angeles, CA (Metropolitan Area)            30977
#> 231              32575   Los Angeles, CA (Metropolitan Area)            30466
#> 232              32575   Los Angeles, CA (Metropolitan Area)            30559
#> 233              32575   Los Angeles, CA (Metropolitan Area)            32457
#> 234              31703 New York City, NY (Metropolitan Area)            30397
#> 235              31703 New York City, NY (Metropolitan Area)            30721
#> 236              31703 New York City, NY (Metropolitan Area)            30647
#> 237              31703 New York City, NY (Metropolitan Area)            31057
#> 238              31703 New York City, NY (Metropolitan Area)            31146
#> 239              31703 New York City, NY (Metropolitan Area)            30977
#> 240              31703 New York City, NY (Metropolitan Area)            33195
#> 241              32982                             Lihue, HI            32134
#> 242              32982                             Lihue, HI            32575
#> 243              33198                       Kansas City, MO            30194
#> 244              33198                       Kansas City, MO            31453
#> 245              33198                       Kansas City, MO            31703
#> 246              33198                       Kansas City, MO            33342
#> 247              33198                       Kansas City, MO            34100
#> 248              31454                           Orlando, FL            30397
#> 249              31454                           Orlando, FL            31057
#> 250              31454                           Orlando, FL            30325
#> 251              31454                           Orlando, FL            30194
#> 252              31454                           Orlando, FL            31295
#> 253              31454                           Orlando, FL            31703
#> 254              31454                           Orlando, FL            32467
#> 255              31454                           Orlando, FL            31721
#> 256              31454                           Orlando, FL            31453
#> 257              31454                           Orlando, FL            31703
#> 258              31454                           Orlando, FL            31453
#> 259              31454                           Orlando, FL            32337
#> 260              31454                           Orlando, FL            30721
#> 261              31454                           Orlando, FL            31650
#> 262              31454                           Orlando, FL            30977
#> 263              31454                           Orlando, FL            34100
#> 264              32070                        Harrisburg, PA            31454
#> 265              30977                           Chicago, IL            31066
#> 266              30977                           Chicago, IL            31703
#> 267              30977                           Chicago, IL            30721
#> 268              33244                           Memphis, TN            30397
#> 269              33244                           Memphis, TN            31703
#> 270              33244                           Memphis, TN            34653
#> 271              32467         Miami, FL (Metropolitan Area)            33105
#> 272              32467         Miami, FL (Metropolitan Area)            30852
#> 273              32467         Miami, FL (Metropolitan Area)            30194
#> 274              32467         Miami, FL (Metropolitan Area)            31295
#> 275              32467         Miami, FL (Metropolitan Area)            31703
#> 276              32467         Miami, FL (Metropolitan Area)            31703
#> 277              32467         Miami, FL (Metropolitan Area)            30977
#> 278              32467         Miami, FL (Metropolitan Area)            32457
#> 279              32467         Miami, FL (Metropolitan Area)            34819
#> 280              33342                         Milwaukee, WI            30325
#> 281              33342                         Milwaukee, WI            30194
#> 282              31650              Minneapolis/St. Paul, MN            30397
#> 283              31650              Minneapolis/St. Paul, MN            30325
#> 284              31650              Minneapolis/St. Paul, MN            30194
#> 285              31650              Minneapolis/St. Paul, MN            31295
#> 286              31650              Minneapolis/St. Paul, MN            33198
#> 287              31650              Minneapolis/St. Paul, MN            31454
#> 288              31650              Minneapolis/St. Paul, MN            30977
#> 289              31650              Minneapolis/St. Paul, MN            30466
#> 290              33495                       New Orleans, LA            30397
#> 291              33495                       New Orleans, LA            31453
#> 292              33495                       New Orleans, LA            30977
#> 293              32457 San Francisco, CA (Metropolitan Area)            30140
#> 294              32457 San Francisco, CA (Metropolitan Area)            30466
#> 295              33830                           Kahului, HI            32575
#> 296              33830                           Kahului, HI            34057
#> 297              33851                     Oklahoma City, OK            30194
#> 298              33851                     Oklahoma City, OK            31453
#> 299              33316                             Omaha, NE            30325
#> 300              33316                             Omaha, NE            30466
#> 301              30977                           Chicago, IL            30693
#> 302              30977                           Chicago, IL            30721
#> 303              30977                           Chicago, IL            30852
#> 304              30977                           Chicago, IL            31066
#> 305              30977                           Chicago, IL            30852
#> 306              30977                           Chicago, IL            30325
#> 307              30977                           Chicago, IL            30194
#> 308              30977                           Chicago, IL            31423
#> 309              30977                           Chicago, IL            31295
#> 310              30977                           Chicago, IL            31703
#> 311              30977                           Chicago, IL            32575
#> 312              30977                           Chicago, IL            31703
#> 313              30977                           Chicago, IL            32467
#> 314              30977                           Chicago, IL            31650
#> 315              30977                           Chicago, IL            33495
#> 316              30977                           Chicago, IL            34100
#> 317              30977                           Chicago, IL            31714
#> 318              30977                           Chicago, IL            33570
#> 319              30977                           Chicago, IL            30559
#> 320              30977                           Chicago, IL            32457
#> 321              30977                           Chicago, IL            31123
#> 322              34027        West Palm Beach/Palm Beach, FL            30397
#> 323              34057                          Portland, OR            32575
#> 324              34057                          Portland, OR            30559
#> 325              34057                          Portland, OR            32575
#> 326              34100                      Philadelphia, PA            30325
#> 327              34100                      Philadelphia, PA            30194
#> 328              34100                      Philadelphia, PA            31454
#> 329              34100                      Philadelphia, PA            31650
#> 330              34100                      Philadelphia, PA            30977
#> 331              34100                      Philadelphia, PA            30466
#> 332              34100                      Philadelphia, PA            34492
#> 333              30466                           Phoenix, AZ            30397
#> 334              30466                           Phoenix, AZ            30852
#> 335              30466                           Phoenix, AZ            30194
#> 336              30466                           Phoenix, AZ            31295
#> 337              30466                           Phoenix, AZ            31703
#> 338              30466                           Phoenix, AZ            31921
#> 339              30466                           Phoenix, AZ            31453
#> 340              30466                           Phoenix, AZ            32575
#> 341              30466                           Phoenix, AZ            31650
#> 342              30466                           Phoenix, AZ            32457
#> 343              30466                           Phoenix, AZ            33316
#> 344              30466                           Phoenix, AZ            30977
#> 345              30466                           Phoenix, AZ            34057
#> 346              30466                           Phoenix, AZ            30198
#> 347              30466                           Phoenix, AZ            30721
#> 348              30466                           Phoenix, AZ            34570
#> 349              30466                           Phoenix, AZ            33570
#> 350              30466                           Phoenix, AZ            30559
#> 351              30466                           Phoenix, AZ            34614
#> 352              33195         Tampa, FL (Metropolitan Area)            31003
#> 353              30198                        Pittsburgh, PA            32467
#> 354              33728                         Pensacola, FL            30397
#> 355              34254                    Ponce, Puerto Rico            31703
#> 356              34262                      Palm Springs, CA            30466
#> 357              34492                    Raleigh/Durham, NC            30397
#> 358              34524                          Richmond, VA            31057
#> 359              34570                              Reno, NV            32211
#> 360              34576                         Rochester, NY            30397
#> 361              31714                        Fort Myers, FL            30721
#> 362              31714                        Fort Myers, FL            30852
#> 363              31714                        Fort Myers, FL            31453
#> 364              31714                        Fort Myers, FL            31650
#> 365              33570                         San Diego, CA            30325
#> 366              33570                         San Diego, CA            31650
#> 367              33570                         San Diego, CA            30977
#> 368              33570                         San Diego, CA            30466
#> 369              33214                       San Antonio, TX            30194
#> 370              33214                       San Antonio, TX            30194
#> 371              33214                       San Antonio, TX            30977
#> 372              33214                       San Antonio, TX            31650
#> 373              30559                           Seattle, WA            30299
#> 374              30559                           Seattle, WA            32575
#> 375              30559                           Seattle, WA            30194
#> 376              30559                           Seattle, WA            32134
#> 377              30559                           Seattle, WA            31703
#> 378              30559                           Seattle, WA            32211
#> 379              30559                           Seattle, WA            32457
#> 380              30559                           Seattle, WA            30466
#> 381              30559                           Seattle, WA            34570
#> 382              30559                           Seattle, WA            33570
#> 383              32457 San Francisco, CA (Metropolitan Area)            30721
#> 384              32457 San Francisco, CA (Metropolitan Area)            30325
#> 385              32457 San Francisco, CA (Metropolitan Area)            32134
#> 386              32457 San Francisco, CA (Metropolitan Area)            31703
#> 387              32457 San Francisco, CA (Metropolitan Area)            32211
#> 388              32457 San Francisco, CA (Metropolitan Area)            32575
#> 389              32457 San Francisco, CA (Metropolitan Area)            30977
#> 390              32457 San Francisco, CA (Metropolitan Area)            34100
#> 391              32457 San Francisco, CA (Metropolitan Area)            30559
#> 392              32457 San Francisco, CA (Metropolitan Area)            32575
#> 393              34819                 San Juan, Puerto Rico            30397
#> 394              34819                 San Juan, Puerto Rico            32467
#> 395              34614                    Salt Lake City, UT            30325
#> 396              34614                    Salt Lake City, UT            32134
#> 397              34614                    Salt Lake City, UT            30852
#> 398              34614                    Salt Lake City, UT            30977
#> 399              34614                    Salt Lake City, UT            34057
#> 400              34614                    Salt Lake City, UT            30466
#> 401              33192                        Sacramento, CA            30325
#> 402              32575   Los Angeles, CA (Metropolitan Area)            30325
#> 403              32575   Los Angeles, CA (Metropolitan Area)            30194
#> 404              32575   Los Angeles, CA (Metropolitan Area)            30559
#> 405              31123                         St. Louis, MO            30194
#> 406              31123                         St. Louis, MO            31295
#> 407              31123                         St. Louis, MO            32600
#> 408              31123                         St. Louis, MO            33851
#> 409              31123                         St. Louis, MO            30466
#> 410              34945      Charlotte Amalie, Virgin Islands            31057
#> 411              33195         Tampa, FL (Metropolitan Area)            30397
#> 412              33195         Tampa, FL (Metropolitan Area)            30194
#> 413              33195         Tampa, FL (Metropolitan Area)            32467
#> 414              33195         Tampa, FL (Metropolitan Area)            31703
#> 415              33195         Tampa, FL (Metropolitan Area)            32467
#> 416              33195         Tampa, FL (Metropolitan Area)            31123
#> 417              35412                         Knoxville, TN            30397
#> 418              35412                         Knoxville, TN            31057
#>                                 dest_city
#> 1                   Dallas/Fort Worth, TX
#> 2                      Salt Lake City, UT
#> 3                           Fairbanks, AK
#> 4                             Seattle, WA
#> 5                            Hartford, CT
#> 6          Boston, MA (Metropolitan Area)
#> 7      Washington, DC (Metropolitan Area)
#> 8                            Columbia, SC
#> 9                          Charleston, SC
#> 10                          Charlotte, NC
#> 11                         Cincinnati, OH
#> 12                             Denver, CO
#> 13                  Dallas/Fort Worth, TX
#> 14          Miami, FL (Metropolitan Area)
#> 15                              Flint, MI
#> 16             Greenville/Spartanburg, SC
#> 17     Washington, DC (Metropolitan Area)
#> 18                            Houston, TX
#> 19                       Indianapolis, IN
#> 20                       Jacksonville, FL
#> 21                          Las Vegas, NV
#> 22    Los Angeles, CA (Metropolitan Area)
#> 23                            Orlando, FL
#> 24                          Milwaukee, WI
#> 25                             Mobile, AL
#> 26               Minneapolis/St. Paul, MN
#> 27                        New Orleans, LA
#> 28                            Chicago, IL
#> 29        Norfolk, VA (Metropolitan Area)
#> 30                       Philadelphia, PA
#> 31                         Pittsburgh, PA
#> 32                           Richmond, VA
#> 33                          Rochester, NY
#> 34                         Fort Myers, FL
#> 35                           Savannah, GA
#> 36                  San Juan, Puerto Rico
#> 37          Tampa, FL (Metropolitan Area)
#> 38                         Valparaiso, FL
#> 39                  Dallas/Fort Worth, TX
#> 40          Miami, FL (Metropolitan Area)
#> 41        Atlanta, GA (Metropolitan Area)
#> 42                            Seattle, WA
#> 43        Atlanta, GA (Metropolitan Area)
#> 44     Washington, DC (Metropolitan Area)
#> 45                  Dallas/Fort Worth, TX
#> 46  New York City, NY (Metropolitan Area)
#> 47  San Francisco, CA (Metropolitan Area)
#> 48                            Seattle, WA
#> 49        Atlanta, GA (Metropolitan Area)
#> 50     Washington, DC (Metropolitan Area)
#> 51                  Dallas/Fort Worth, TX
#> 52  New York City, NY (Metropolitan Area)
#> 53                        New Orleans, LA
#> 54                            Chicago, IL
#> 55                       Philadelphia, PA
#> 56  San Francisco, CA (Metropolitan Area)
#> 57                            Detroit, MI
#> 58                            Orlando, FL
#> 59        Atlanta, GA (Metropolitan Area)
#> 60         Boston, MA (Metropolitan Area)
#> 61                          Charlotte, NC
#> 62                            Chicago, IL
#> 63         Boston, MA (Metropolitan Area)
#> 64                            Chicago, IL
#> 65                            Phoenix, AZ
#> 66        Atlanta, GA (Metropolitan Area)
#> 67                          Charlotte, NC
#> 68                          Charlotte, NC
#> 69                            Augusta, GA
#> 70        Atlanta, GA (Metropolitan Area)
#> 71                             Austin, TX
#> 72                            Buffalo, NY
#> 73     Washington, DC (Metropolitan Area)
#> 74     Washington, DC (Metropolitan Area)
#> 75                  Dallas/Fort Worth, TX
#> 76                            Detroit, MI
#> 77  New York City, NY (Metropolitan Area)
#> 78                            Orlando, FL
#> 79          Jacksonville/Camp Lejeune, NC
#> 80                            Chicago, IL
#> 81        Norfolk, VA (Metropolitan Area)
#> 82                       Philadelphia, PA
#> 83                            Phoenix, AZ
#> 84         Boston, MA (Metropolitan Area)
#> 85                         Fort Myers, FL
#> 86                          St. Louis, MO
#> 87          Tampa, FL (Metropolitan Area)
#> 88                             Denver, CO
#> 89                          Nashville, TN
#> 90                             Denver, CO
#> 91                            Houston, TX
#> 92        Atlanta, GA (Metropolitan Area)
#> 93          Tampa, FL (Metropolitan Area)
#> 94         Boston, MA (Metropolitan Area)
#> 95                             Denver, CO
#> 96                  Dallas/Fort Worth, TX
#> 97                            Orlando, FL
#> 98                            Chicago, IL
#> 99          Tampa, FL (Metropolitan Area)
#> 100         Miami, FL (Metropolitan Area)
#> 101                           Jackson, WY
#> 102                         Las Vegas, NV
#> 103   Los Angeles, CA (Metropolitan Area)
#> 104                       Kansas City, MO
#> 105                           Orlando, FL
#> 106                           Chicago, IL
#> 107                         Milwaukee, WI
#> 108              Minneapolis/St. Paul, MN
#> 109                     Oklahoma City, OK
#> 110                             Omaha, NE
#> 111                           Chicago, IL
#> 112                          Portland, OR
#> 113                           Phoenix, AZ
#> 114                         San Diego, CA
#> 115 San Francisco, CA (Metropolitan Area)
#> 116                    Salt Lake City, UT
#> 117                        Sacramento, CA
#> 118   Los Angeles, CA (Metropolitan Area)
#> 119                            Tucson, AZ
#> 120       Atlanta, GA (Metropolitan Area)
#> 121                         Nashville, TN
#> 122                         Charlotte, NC
#> 123    Washington, DC (Metropolitan Area)
#> 124                            Denver, CO
#> 125                      Indianapolis, IN
#> 126                         Las Vegas, NV
#> 127   Los Angeles, CA (Metropolitan Area)
#> 128 New York City, NY (Metropolitan Area)
#> 129                           Kahului, HI
#> 130   Los Angeles, CA (Metropolitan Area)
#> 131                           Chicago, IL
#> 132                      Philadelphia, PA
#> 133                           Phoenix, AZ
#> 134                       San Antonio, TX
#> 135                           Seattle, WA
#> 136 San Francisco, CA (Metropolitan Area)
#> 137                 San Juan, Puerto Rico
#> 138                    Salt Lake City, UT
#> 139   Los Angeles, CA (Metropolitan Area)
#> 140                            Tucson, AZ
#> 141    Washington, DC (Metropolitan Area)
#> 142       Atlanta, GA (Metropolitan Area)
#> 143        Boston, MA (Metropolitan Area)
#> 144         Miami, FL (Metropolitan Area)
#> 145                           Houston, TX
#> 146                           Chicago, IL
#> 147              Minneapolis/St. Paul, MN
#> 148                           Chicago, IL
#> 149                      Philadelphia, PA
#> 150                        Fort Myers, FL
#> 151                 Dallas/Fort Worth, TX
#> 152        Boston, MA (Metropolitan Area)
#> 153                         Las Vegas, NV
#> 154                           Orlando, FL
#> 155                           Seattle, WA
#> 156       Atlanta, GA (Metropolitan Area)
#> 157     Cleveland, OH (Metropolitan Area)
#> 158                         Charlotte, NC
#> 159 New York City, NY (Metropolitan Area)
#> 160 New York City, NY (Metropolitan Area)
#> 161                       Kansas City, MO
#> 162                      Philadelphia, PA
#> 163         Tampa, FL (Metropolitan Area)
#> 164                    Salt Lake City, UT
#> 165              Minneapolis/St. Paul, MN
#> 166                           Chicago, IL
#> 167                              Kona, HI
#> 168   Los Angeles, CA (Metropolitan Area)
#> 169                             Lihue, HI
#> 170                           Seattle, WA
#> 171                        Fort Myers, FL
#> 172                            Denver, CO
#> 173                           Seattle, WA
#> 174 San Francisco, CA (Metropolitan Area)
#> 175                    Salt Lake City, UT
#> 176       Atlanta, GA (Metropolitan Area)
#> 177                            Austin, TX
#> 178                         Charlotte, NC
#> 179         Miami, FL (Metropolitan Area)
#> 180              Harlingen/San Benito, TX
#> 181                         Las Vegas, NV
#> 182                       Kansas City, MO
#> 183                           Orlando, FL
#> 184                       New Orleans, LA
#> 185                           Chicago, IL
#> 186                       San Antonio, TX
#> 187 San Francisco, CA (Metropolitan Area)
#> 188       Atlanta, GA (Metropolitan Area)
#> 189                 Dallas/Fort Worth, TX
#> 190                           Orlando, FL
#> 191    Washington, DC (Metropolitan Area)
#> 192 New York City, NY (Metropolitan Area)
#> 193                           Buffalo, NY
#> 194         Miami, FL (Metropolitan Area)
#> 195 New York City, NY (Metropolitan Area)
#> 196              Minneapolis/St. Paul, MN
#> 197 San Francisco, CA (Metropolitan Area)
#> 198                 San Juan, Puerto Rico
#> 199         Tampa, FL (Metropolitan Area)
#> 200                           Chicago, IL
#> 201       Atlanta, GA (Metropolitan Area)
#> 202                        Bellingham, WA
#> 203                            Denver, CO
#> 204                 Dallas/Fort Worth, TX
#> 205                           Detroit, MI
#> 206 New York City, NY (Metropolitan Area)
#> 207                         Kalispell, MT
#> 208                      Indianapolis, IN
#> 209   Los Angeles, CA (Metropolitan Area)
#> 210   Los Angeles, CA (Metropolitan Area)
#> 211                           Chicago, IL
#> 212              Minneapolis/St. Paul, MN
#> 213 San Francisco, CA (Metropolitan Area)
#> 214                           Chicago, IL
#> 215                          Portland, OR
#> 216                           Phoenix, AZ
#> 217                           Seattle, WA
#> 218 San Francisco, CA (Metropolitan Area)
#> 219                        Shreveport, LA
#> 220       Atlanta, GA (Metropolitan Area)
#> 221                         Charlotte, NC
#> 222                            Denver, CO
#> 223                 Dallas/Fort Worth, TX
#> 224                           Detroit, MI
#> 225                           Houston, TX
#> 226 New York City, NY (Metropolitan Area)
#> 227                             Lihue, HI
#> 228         Miami, FL (Metropolitan Area)
#> 229                           Kahului, HI
#> 230                           Chicago, IL
#> 231                           Phoenix, AZ
#> 232                           Seattle, WA
#> 233 San Francisco, CA (Metropolitan Area)
#> 234       Atlanta, GA (Metropolitan Area)
#> 235        Boston, MA (Metropolitan Area)
#> 236     Cleveland, OH (Metropolitan Area)
#> 237                         Charlotte, NC
#> 238                 Charleston/Dunbar, WV
#> 239                           Chicago, IL
#> 240         Tampa, FL (Metropolitan Area)
#> 241                          Honolulu, HI
#> 242   Los Angeles, CA (Metropolitan Area)
#> 243                 Dallas/Fort Worth, TX
#> 244                           Houston, TX
#> 245 New York City, NY (Metropolitan Area)
#> 246                         Milwaukee, WI
#> 247                      Philadelphia, PA
#> 248       Atlanta, GA (Metropolitan Area)
#> 249                         Charlotte, NC
#> 250                            Denver, CO
#> 251                 Dallas/Fort Worth, TX
#> 252                           Detroit, MI
#> 253 New York City, NY (Metropolitan Area)
#> 254         Miami, FL (Metropolitan Area)
#> 255                             Flint, MI
#> 256                           Houston, TX
#> 257 New York City, NY (Metropolitan Area)
#> 258                           Houston, TX
#> 259                      Indianapolis, IN
#> 260        Boston, MA (Metropolitan Area)
#> 261              Minneapolis/St. Paul, MN
#> 262                           Chicago, IL
#> 263                      Philadelphia, PA
#> 264                           Orlando, FL
#> 265                          Columbus, OH
#> 266 New York City, NY (Metropolitan Area)
#> 267        Boston, MA (Metropolitan Area)
#> 268       Atlanta, GA (Metropolitan Area)
#> 269 New York City, NY (Metropolitan Area)
#> 270                             Tulsa, OK
#> 271                        Cincinnati, OH
#> 272    Washington, DC (Metropolitan Area)
#> 273                 Dallas/Fort Worth, TX
#> 274                           Detroit, MI
#> 275 New York City, NY (Metropolitan Area)
#> 276 New York City, NY (Metropolitan Area)
#> 277                           Chicago, IL
#> 278 San Francisco, CA (Metropolitan Area)
#> 279                 San Juan, Puerto Rico
#> 280                            Denver, CO
#> 281                 Dallas/Fort Worth, TX
#> 282       Atlanta, GA (Metropolitan Area)
#> 283                            Denver, CO
#> 284                 Dallas/Fort Worth, TX
#> 285                           Detroit, MI
#> 286                       Kansas City, MO
#> 287                           Orlando, FL
#> 288                           Chicago, IL
#> 289                           Phoenix, AZ
#> 290       Atlanta, GA (Metropolitan Area)
#> 291                           Houston, TX
#> 292                           Chicago, IL
#> 293                       Albuquerque, NM
#> 294                           Phoenix, AZ
#> 295   Los Angeles, CA (Metropolitan Area)
#> 296                          Portland, OR
#> 297                 Dallas/Fort Worth, TX
#> 298                           Houston, TX
#> 299                            Denver, CO
#> 300                           Phoenix, AZ
#> 301                         Nashville, TN
#> 302        Boston, MA (Metropolitan Area)
#> 303    Washington, DC (Metropolitan Area)
#> 304                          Columbus, OH
#> 305    Washington, DC (Metropolitan Area)
#> 306                            Denver, CO
#> 307                 Dallas/Fort Worth, TX
#> 308                        Des Moines, IA
#> 309                           Detroit, MI
#> 310 New York City, NY (Metropolitan Area)
#> 311   Los Angeles, CA (Metropolitan Area)
#> 312 New York City, NY (Metropolitan Area)
#> 313         Miami, FL (Metropolitan Area)
#> 314              Minneapolis/St. Paul, MN
#> 315                       New Orleans, LA
#> 316                      Philadelphia, PA
#> 317                        Fort Myers, FL
#> 318                         San Diego, CA
#> 319                           Seattle, WA
#> 320 San Francisco, CA (Metropolitan Area)
#> 321                         St. Louis, MO
#> 322       Atlanta, GA (Metropolitan Area)
#> 323   Los Angeles, CA (Metropolitan Area)
#> 324                           Seattle, WA
#> 325   Los Angeles, CA (Metropolitan Area)
#> 326                            Denver, CO
#> 327                 Dallas/Fort Worth, TX
#> 328                           Orlando, FL
#> 329              Minneapolis/St. Paul, MN
#> 330                           Chicago, IL
#> 331                           Phoenix, AZ
#> 332                    Raleigh/Durham, NC
#> 333       Atlanta, GA (Metropolitan Area)
#> 334    Washington, DC (Metropolitan Area)
#> 335                 Dallas/Fort Worth, TX
#> 336                           Detroit, MI
#> 337 New York City, NY (Metropolitan Area)
#> 338                    Grand Junction, CO
#> 339                           Houston, TX
#> 340   Los Angeles, CA (Metropolitan Area)
#> 341              Minneapolis/St. Paul, MN
#> 342 San Francisco, CA (Metropolitan Area)
#> 343                             Omaha, NE
#> 344                           Chicago, IL
#> 345                          Portland, OR
#> 346                        Pittsburgh, PA
#> 347        Boston, MA (Metropolitan Area)
#> 348                              Reno, NV
#> 349                         San Diego, CA
#> 350                           Seattle, WA
#> 351                    Salt Lake City, UT
#> 352            Cedar Rapids/Iowa City, IA
#> 353         Miami, FL (Metropolitan Area)
#> 354       Atlanta, GA (Metropolitan Area)
#> 355 New York City, NY (Metropolitan Area)
#> 356                           Phoenix, AZ
#> 357       Atlanta, GA (Metropolitan Area)
#> 358                         Charlotte, NC
#> 359                         Las Vegas, NV
#> 360       Atlanta, GA (Metropolitan Area)
#> 361        Boston, MA (Metropolitan Area)
#> 362    Washington, DC (Metropolitan Area)
#> 363                           Houston, TX
#> 364              Minneapolis/St. Paul, MN
#> 365                            Denver, CO
#> 366              Minneapolis/St. Paul, MN
#> 367                           Chicago, IL
#> 368                           Phoenix, AZ
#> 369                 Dallas/Fort Worth, TX
#> 370                 Dallas/Fort Worth, TX
#> 371                           Chicago, IL
#> 372              Minneapolis/St. Paul, MN
#> 373                         Anchorage, AK
#> 374   Los Angeles, CA (Metropolitan Area)
#> 375                 Dallas/Fort Worth, TX
#> 376                          Honolulu, HI
#> 377 New York City, NY (Metropolitan Area)
#> 378                         Las Vegas, NV
#> 379 San Francisco, CA (Metropolitan Area)
#> 380                           Phoenix, AZ
#> 381                              Reno, NV
#> 382                         San Diego, CA
#> 383        Boston, MA (Metropolitan Area)
#> 384                            Denver, CO
#> 385                          Honolulu, HI
#> 386 New York City, NY (Metropolitan Area)
#> 387                         Las Vegas, NV
#> 388   Los Angeles, CA (Metropolitan Area)
#> 389                           Chicago, IL
#> 390                      Philadelphia, PA
#> 391                           Seattle, WA
#> 392   Los Angeles, CA (Metropolitan Area)
#> 393       Atlanta, GA (Metropolitan Area)
#> 394         Miami, FL (Metropolitan Area)
#> 395                            Denver, CO
#> 396                          Honolulu, HI
#> 397    Washington, DC (Metropolitan Area)
#> 398                           Chicago, IL
#> 399                          Portland, OR
#> 400                           Phoenix, AZ
#> 401                            Denver, CO
#> 402                            Denver, CO
#> 403                 Dallas/Fort Worth, TX
#> 404                           Seattle, WA
#> 405                 Dallas/Fort Worth, TX
#> 406                           Detroit, MI
#> 407                       Little Rock, AR
#> 408                     Oklahoma City, OK
#> 409                           Phoenix, AZ
#> 410                         Charlotte, NC
#> 411       Atlanta, GA (Metropolitan Area)
#> 412                 Dallas/Fort Worth, TX
#> 413         Miami, FL (Metropolitan Area)
#> 414 New York City, NY (Metropolitan Area)
#> 415         Miami, FL (Metropolitan Area)
#> 416                         St. Louis, MO
#> 417       Atlanta, GA (Metropolitan Area)
#> 418                         Charlotte, NC
#> 
#> $nodes
#>     airport pass_dep pass_arr pass_tr city_mkt_id
#> 1       ABQ       22       24       4       30140
#> 2       AGS        3        7       0       30208
#> 3       ANC       12       10       4       30299
#> 4       ATL      395      321     229       30397
#> 5       AUS       27       40       4       30423
#> 6       BDL       34       28       1       30529
#> 7       BHM       13       12       1       30599
#> 8       BLI        4       14       3       30666
#> 9       BNA       62       45      10       30693
#> 10      BOI       19        9       1       30713
#> 11      BOS      213      106       4       30721
#> 12      BUF       24       21       1       30792
#> 13      BUR       11       12       3       32575
#> 14      BWI       94       76      22       30852
#> 15      CAE        5        8       0       30868
#> 16      CAK       28       12       1       30647
#> 17      CHS       13       12       0       30994
#> 18      CID        1        8       0       31003
#> 19      CLE       19       42      14       30647
#> 20      CLT      186      170     138       31057
#> 21      CMH       20       25       1       31066
#> 22      COS        5        7       0       30189
#> 23      CRW        6        6       0       31146
#> 24      CVG       31       28       6       33105
#> 25      DAL       42       27      14       30194
#> 26      DAY       24        8       0       31267
#> 27      DCA       97      113      24       30852
#> 28      DEN      256      253     123       30325
#> 29      DFW      277      250     145       30194
#> 30      DSM       10       10       0       31423
#> 31      DTW      120      127      68       31295
#> 32      ELP       16        6       1       30615
#> 33      EWR       88       72      17       31703
#> 34      FAI        1        6       1       31517
#> 35      FCA        0        5       0       31648
#> 36      FLL       98      127       8       32467
#> 37      FNT        4       27       0       31721
#> 38      GEG       10       14       0       31884
#> 39      GJT        3        7       0       31921
#> 40      GRB        5        2       0       31977
#> 41      GRR       13       11       0       31986
#> 42      GSP        3       12       0       31871
#> 43      HNL       57       29      10       32134
#> 44      HOU       35       65      23       31453
#> 45      HPN       26       24       0       31703
#> 46      HRL        1        6       0       32206
#> 47      IAD       66       52      23       30852
#> 48      IAH      143      121      73       31453
#> 49      IND       39       41       3       32337
#> 50      ISP        4       21       0       31703
#> 51      JAC        0        6       0       32441
#> 52      JAX       25       14       0       31136
#> 53      JFK       78      267      15       31703
#> 54      KOA        5       13       2       32758
#> 55      LAN        7        1       0       32884
#> 56      LAS      235      137      25       32211
#> 57      LAX      286      136      48       32575
#> 58      LGA      136      106      13       31703
#> 59      LGB        7        8       3       32575
#> 60      LIH       15        9       0       32982
#> 61      LIT       11       20       0       32600
#> 62      MCI       53       34       1       33198
#> 63      MCO      200      111      12       31454
#> 64      MDT        9        9       0       32070
#> 65      MDW       68      109      49       30977
#> 66      MEM       65       36      23       33244
#> 67      MHT       10       41       1       30721
#> 68      MIA       91       59      20       32467
#> 69      MKE       33       56       4       33342
#> 70      MOB        1        8       0       30562
#> 71      MSP      109      176      63       31650
#> 72      MSY       63       64       2       33495
#> 73      OAJ        3        4       0       33795
#> 74      OAK       33       28       4       32457
#> 75      OGG       17       16       2       33830
#> 76      OKC       25       20       2       33851
#> 77      OMA       23       24       1       33316
#> 78      ONT       16       20       1       32575
#> 79      ORD      213      288     106       30977
#> 80      ORF       10       14       1       33667
#> 81      PBI       24       16       0       34027
#> 82      PDX       42      100       6       34057
#> 83      PHF        3        9       0       33667
#> 84      PHL      115      119      55       34100
#> 85      PHX      201      172      68       30466
#> 86      PIE        8        0       0       33195
#> 87      PIT       18       39       1       30198
#> 88      PNS       11        5       0       33728
#> 89      PSE        4        0       0       34254
#> 90      PSP       14        7       3       34262
#> 91      PVD       16       12       0       30721
#> 92      RDU       29       45       2       34492
#> 93      RIC       12       14       1       34524
#> 94      RNO       21       29       3       34570
#> 95      ROC       11       14       0       34576
#> 96      RSW       48       71       2       31714
#> 97      SAN       54       50       2       33570
#> 98      SAT       37       33       1       33214
#> 99      SAV        4       10       0       34685
#> 100     SEA      121      135      35       30559
#> 101     SFO      121      215      27       32457
#> 102     SHV        1       10       0       30476
#> 103     SJC       17       14       1       32457
#> 104     SJU       30       39       5       34819
#> 105     SLC      100       88      35       34614
#> 106     SMF       25       25       5       33192
#> 107     SNA       37       52       0       32575
#> 108     STL       60       49      15       31123
#> 109     STT        6        7       0       34945
#> 110     TPA       76       98       9       33195
#> 111     TUL       10        8       1       34653
#> 112     TUS       10       21       1       30436
#> 113     TYS       11        8       0       35412
#> 114     VPS        2        5       0       31504
#>                                      city latitude  longitude
#> 1                         Albuquerque, NM 35.04167 -106.60639
#> 2                             Augusta, GA 33.36917  -81.96444
#> 3                           Anchorage, AK 61.16917 -149.98528
#> 4         Atlanta, GA (Metropolitan Area) 33.64083  -84.42722
#> 5                              Austin, TX 30.19444  -97.67000
#> 6                            Hartford, CT 41.93861  -72.68333
#> 7                          Birmingham, AL 33.56306  -86.75556
#> 8                          Bellingham, WA 48.79444 -122.53472
#> 9                           Nashville, TN 36.12667  -86.68194
#> 10                              Boise, ID 43.56528 -116.22500
#> 11         Boston, MA (Metropolitan Area) 42.36361  -71.00611
#> 12                            Buffalo, NY 42.94111  -78.73639
#> 13    Los Angeles, CA (Metropolitan Area) 34.20000 -118.35778
#> 14     Washington, DC (Metropolitan Area) 39.17500  -76.67000
#> 15                           Columbia, SC 33.93639  -81.11583
#> 16      Cleveland, OH (Metropolitan Area) 40.91389  -81.44167
#> 17                         Charleston, SC 32.89917  -80.03889
#> 18             Cedar Rapids/Iowa City, IA 41.88444  -91.70611
#> 19      Cleveland, OH (Metropolitan Area) 41.41083  -81.84944
#> 20                          Charlotte, NC 35.21917  -80.93583
#> 21                           Columbus, OH 39.99111  -82.87833
#> 22                   Colorado Springs, CO 38.80889 -104.70917
#> 23                  Charleston/Dunbar, WV 38.37278  -81.59306
#> 24                         Cincinnati, OH 39.04778  -84.66861
#> 25                  Dallas/Fort Worth, TX 32.84694  -96.85333
#> 26                             Dayton, OH 39.90111  -84.22000
#> 27     Washington, DC (Metropolitan Area) 38.85167  -77.03694
#> 28                             Denver, CO 39.77444 -104.87972
#> 29                  Dallas/Fort Worth, TX 32.89444  -97.02972
#> 30                         Des Moines, IA 41.53389  -93.65667
#> 31                            Detroit, MI 42.21667  -83.34444
#> 32                            El Paso, TX 31.80667 -106.37722
#> 33  New York City, NY (Metropolitan Area) 40.69583  -74.17167
#> 34                          Fairbanks, AK 64.81444 -147.86278
#> 35                          Kalispell, MT 48.31278 -114.25111
#> 36          Miami, FL (Metropolitan Area) 26.07417  -80.15167
#> 37                              Flint, MI 42.96667  -83.74167
#> 38                            Spokane, WA 47.62000 -117.53278
#> 39                     Grand Junction, CO 39.11861 -108.51389
#> 40                          Green Bay, WI 44.48806  -88.13056
#> 41                       Grand Rapids, MI 42.88111  -85.52417
#> 42             Greenville/Spartanburg, SC 34.89889  -82.21389
#> 43                           Honolulu, HI 21.31861 -157.92250
#> 44                            Houston, TX 29.64500  -95.27861
#> 45  New York City, NY (Metropolitan Area) 41.06889  -73.70778
#> 46               Harlingen/San Benito, TX 26.22806  -97.65222
#> 47     Washington, DC (Metropolitan Area) 38.94167  -77.45750
#> 48                            Houston, TX 29.98333  -95.34000
#> 49                       Indianapolis, IN 39.72889  -86.28167
#> 50  New York City, NY (Metropolitan Area) 40.79667  -73.10083
#> 51                            Jackson, WY 43.60667 -110.73694
#> 52                       Jacksonville, FL 30.48472  -81.68778
#> 53  New York City, NY (Metropolitan Area) 40.63861  -73.77694
#> 54                               Kona, HI 19.73889 -156.04556
#> 55                            Lansing, MI 42.77917  -84.58833
#> 56                          Las Vegas, NV 36.08000 -115.15222
#> 57    Los Angeles, CA (Metropolitan Area) 33.94250 -118.40806
#> 58  New York City, NY (Metropolitan Area) 40.77944  -73.87583
#> 59    Los Angeles, CA (Metropolitan Area) 33.81750 -118.15111
#> 60                              Lihue, HI 21.97917 -159.34583
#> 61                        Little Rock, AR 34.72917  -92.23444
#> 62                        Kansas City, MO 39.29750  -94.71389
#> 63                            Orlando, FL 28.43167  -81.32472
#> 64                         Harrisburg, PA 40.19306  -76.76222
#> 65                            Chicago, IL 41.78500  -87.75194
#> 66                            Memphis, TN 35.04972  -89.97861
#> 67         Boston, MA (Metropolitan Area) 42.93833  -71.43889
#> 68          Miami, FL (Metropolitan Area) 25.79250  -80.28611
#> 69                          Milwaukee, WI 42.95028  -87.89722
#> 70                             Mobile, AL 30.68833  -88.24083
#> 71               Minneapolis/St. Paul, MN 44.88611  -93.21778
#> 72                        New Orleans, LA 29.99111  -90.25139
#> 73          Jacksonville/Camp Lejeune, NC 34.83028  -77.61167
#> 74  San Francisco, CA (Metropolitan Area) 37.72139 -122.22083
#> 75                            Kahului, HI 20.90056 -156.43361
#> 76                      Oklahoma City, OK 35.39222  -97.60167
#> 77                              Omaha, NE 41.30194  -95.89333
#> 78    Los Angeles, CA (Metropolitan Area) 34.05611 -117.60111
#> 79                            Chicago, IL 41.97806  -87.90611
#> 80        Norfolk, VA (Metropolitan Area) 36.89583  -76.20139
#> 81         West Palm Beach/Palm Beach, FL 26.68222  -80.09417
#> 82                           Portland, OR 45.58917 -122.59500
#> 83        Norfolk, VA (Metropolitan Area) 37.13167  -76.49333
#> 84                       Philadelphia, PA 39.86806  -75.24861
#> 85                            Phoenix, AZ 33.43611 -112.00944
#> 86          Tampa, FL (Metropolitan Area) 27.90722  -82.68556
#> 87                         Pittsburgh, PA 40.49667  -80.23583
#> 88                          Pensacola, FL 30.47333  -87.18750
#> 89                     Ponce, Puerto Rico 18.01083  -66.56361
#> 90                       Palm Springs, CA 33.82667 -116.50500
#> 91         Boston, MA (Metropolitan Area) 41.72833  -71.42611
#> 92                     Raleigh/Durham, NC 35.87528  -78.78194
#> 93                           Richmond, VA 37.50528  -77.31972
#> 94                               Reno, NV 39.49778 -119.76750
#> 95                          Rochester, NY 43.12139  -77.67083
#> 96                         Fort Myers, FL 26.53611  -81.75500
#> 97                          San Diego, CA 32.73278 -117.18722
#> 98                        San Antonio, TX 29.53333  -98.46944
#> 99                           Savannah, GA 32.12750  -81.20250
#> 100                           Seattle, WA 47.44722 -122.30556
#> 101 San Francisco, CA (Metropolitan Area) 37.61889 -122.37500
#> 102                        Shreveport, LA 32.44694  -93.82556
#> 103 San Francisco, CA (Metropolitan Area) 37.36278 -121.94056
#> 104                 San Juan, Puerto Rico 18.44000  -66.00222
#> 105                    Salt Lake City, UT 40.78417 -111.96694
#> 106                        Sacramento, CA 38.69556 -121.58972
#> 107   Los Angeles, CA (Metropolitan Area) 33.67556 -117.86694
#> 108                         St. Louis, MO 38.74722  -90.36444
#> 109      Charlotte Amalie, Virgin Islands 18.33722  -64.97333
#> 110         Tampa, FL (Metropolitan Area) 27.97306  -82.53528
#> 111                             Tulsa, OK 36.19778  -95.88972
#> 112                            Tucson, AZ 32.11611 -110.94056
#> 113                         Knoxville, TN 35.81222  -83.99250
#> 114                        Valparaiso, FL 30.48333  -86.52528
#>                    airport_city_name airport_country_code airport_state
#> 1                    Albuquerque, NM                   US            NM
#> 2                        Augusta, GA                   US            GA
#> 3                      Anchorage, AK                   US            AK
#> 4                        Atlanta, GA                   US            GA
#> 5                         Austin, TX                   US            TX
#> 6                       Hartford, CT                   US            CT
#> 7                     Birmingham, AL                   US            AL
#> 8                     Bellingham, WA                   US            WA
#> 9                      Nashville, TN                   US            TN
#> 10                         Boise, ID                   US            ID
#> 11                        Boston, MA                   US            MA
#> 12                       Buffalo, NY                   US            NY
#> 13                       Burbank, CA                   US            CA
#> 14                     Baltimore, MD                   US            MD
#> 15                      Columbia, SC                   US            SC
#> 16                         Akron, OH                   US            OH
#> 17                    Charleston, SC                   US            SC
#> 18        Cedar Rapids/Iowa City, IA                   US            IA
#> 19                     Cleveland, OH                   US            OH
#> 20                     Charlotte, NC                   US            NC
#> 21                      Columbus, OH                   US            OH
#> 22              Colorado Springs, CO                   US            CO
#> 23             Charleston/Dunbar, WV                   US            WV
#> 24                    Cincinnati, OH                   US            KY
#> 25                        Dallas, TX                   US            TX
#> 26                        Dayton, OH                   US            OH
#> 27                    Washington, DC                   US            VA
#> 28                        Denver, CO                   US            CO
#> 29             Dallas/Fort Worth, TX                   US            TX
#> 30                    Des Moines, IA                   US            IA
#> 31                       Detroit, MI                   US            MI
#> 32                       El Paso, TX                   US            TX
#> 33                        Newark, NJ                   US            NJ
#> 34                     Fairbanks, AK                   US            AK
#> 35                     Kalispell, MT                   US            MT
#> 36               Fort Lauderdale, FL                   US            FL
#> 37                         Flint, MI                   US            MI
#> 38                       Spokane, WA                   US            WA
#> 39                Grand Junction, CO                   US            CO
#> 40                     Green Bay, WI                   US            WI
#> 41                  Grand Rapids, MI                   US            MI
#> 42                         Greer, SC                   US            SC
#> 43                      Honolulu, HI                   US            HI
#> 44                       Houston, TX                   US            TX
#> 45                  White Plains, NY                   US            NY
#> 46          Harlingen/San Benito, TX                   US            TX
#> 47                    Washington, DC                   US            VA
#> 48                       Houston, TX                   US            TX
#> 49                  Indianapolis, IN                   US            IN
#> 50                         Islip, NY                   US            NY
#> 51                       Jackson, WY                   US            WY
#> 52                  Jacksonville, FL                   US            FL
#> 53                      New York, NY                   US            NY
#> 54                          Kona, HI                   US            HI
#> 55                       Lansing, MI                   US            MI
#> 56                     Las Vegas, NV                   US            NV
#> 57                   Los Angeles, CA                   US            CA
#> 58                      New York, NY                   US            NY
#> 59                    Long Beach, CA                   US            CA
#> 60                         Lihue, HI                   US            HI
#> 61                   Little Rock, AR                   US            AR
#> 62                   Kansas City, MO                   US            MO
#> 63                       Orlando, FL                   US            FL
#> 64                    Harrisburg, PA                   US            PA
#> 65                       Chicago, IL                   US            IL
#> 66                       Memphis, TN                   US            TN
#> 67                    Manchester, NH                   US            NH
#> 68                         Miami, FL                   US            FL
#> 69                     Milwaukee, WI                   US            WI
#> 70                        Mobile, AL                   US            AL
#> 71                   Minneapolis, MN                   US            MN
#> 72                   New Orleans, LA                   US            LA
#> 73     Jacksonville/Camp Lejeune, NC                   US            NC
#> 74                       Oakland, CA                   US            CA
#> 75                       Kahului, HI                   US            HI
#> 76                 Oklahoma City, OK                   US            OK
#> 77                         Omaha, NE                   US            NE
#> 78                       Ontario, CA                   US            CA
#> 79                       Chicago, IL                   US            IL
#> 80                       Norfolk, VA                   US            VA
#> 81    West Palm Beach/Palm Beach, FL                   US            FL
#> 82                      Portland, OR                   US            OR
#> 83     Newport News/Williamsburg, VA                   US            VA
#> 84                  Philadelphia, PA                   US            PA
#> 85                       Phoenix, AZ                   US            AZ
#> 86                St. Petersburg, FL                   US            FL
#> 87                    Pittsburgh, PA                   US            PA
#> 88                     Pensacola, FL                   US            FL
#> 89                Ponce, Puerto Rico                   PR              
#> 90                  Palm Springs, CA                   US            CA
#> 91                    Providence, RI                   US            RI
#> 92                Raleigh/Durham, NC                   US            NC
#> 93                      Richmond, VA                   US            VA
#> 94                          Reno, NV                   US            NV
#> 95                     Rochester, NY                   US            NY
#> 96                    Fort Myers, FL                   US            FL
#> 97                     San Diego, CA                   US            CA
#> 98                   San Antonio, TX                   US            TX
#> 99                      Savannah, GA                   US            GA
#> 100                      Seattle, WA                   US            WA
#> 101                San Francisco, CA                   US            CA
#> 102                   Shreveport, LA                   US            LA
#> 103                     San Jose, CA                   US            CA
#> 104            San Juan, Puerto Rico                   PR              
#> 105               Salt Lake City, UT                   US            UT
#> 106                   Sacramento, CA                   US            CA
#> 107                    Santa Ana, CA                   US            CA
#> 108                    St. Louis, MO                   US            MO
#> 109 Charlotte Amalie, Virgin Islands                   VI              
#> 110                        Tampa, FL                   US            FL
#> 111                        Tulsa, OK                   US            OK
#> 112                       Tucson, AZ                   US            AZ
#> 113                    Knoxville, TN                   US            TN
#> 114                   Valparaiso, FL                   US            FL
#>     airport_id freq
#> 1        10140   42
#> 2        10208   10
#> 3        10299   18
#> 4        10397  487
#> 5        10423   63
#> 6        10529   61
#> 7        10599   24
#> 8        10666   15
#> 9        10693   97
#> 10       10713   27
#> 11       10721  315
#> 12       10792   44
#> 13       10800   20
#> 14       10821  148
#> 15       10868   13
#> 16       10874   39
#> 17       10994   25
#> 18       11003    9
#> 19       11042   47
#> 20       11057  218
#> 21       11066   44
#> 22       11109   12
#> 23       11146   12
#> 24       11193   53
#> 25       11259   55
#> 26       11267   32
#> 27       11278  186
#> 28       11292  386
#> 29       11298  382
#> 30       11423   20
#> 31       11433  179
#> 32       11540   21
#> 33       11618  143
#> 34       11630    6
#> 35       11648    5
#> 36       11697  217
#> 37       11721   31
#> 38       11884   24
#> 39       11921   10
#> 40       11977    7
#> 41       11986   24
#> 42       11996   15
#> 43       12173   76
#> 44       12191   77
#> 45       12197   50
#> 46       12206    7
#> 47       12264   95
#> 48       12266  191
#> 49       12339   77
#> 50       12391   25
#> 51       12441    6
#> 52       12451   39
#> 53       12478  330
#> 54       12758   16
#> 55       12884    8
#> 56       12889  347
#> 57       12892  374
#> 58       12953  229
#> 59       12954   12
#> 60       12982   24
#> 61       12992   31
#> 62       13198   86
#> 63       13204  299
#> 64       13230   18
#> 65       13232  128
#> 66       13244   78
#> 67       13296   50
#> 68       13303  130
#> 69       13342   85
#> 70       13422    9
#> 71       13487  222
#> 72       13495  125
#> 73       13795    7
#> 74       13796   57
#> 75       13830   31
#> 76       13851   43
#> 77       13871   46
#> 78       13891   35
#> 79       13930  395
#> 80       13931   23
#> 81       14027   40
#> 82       14057  136
#> 83       14098   12
#> 84       14100  179
#> 85       14107  305
#> 86       14112    8
#> 87       14122   56
#> 88       14193   16
#> 89       14254    4
#> 90       14262   18
#> 91       14307   28
#> 92       14492   72
#> 93       14524   25
#> 94       14570   47
#> 95       14576   25
#> 96       14635  117
#> 97       14679  102
#> 98       14683   69
#> 99       14685   14
#> 100      14747  221
#> 101      14771  309
#> 102      14814   11
#> 103      14831   30
#> 104      14843   64
#> 105      14869  153
#> 106      14893   45
#> 107      14908   89
#> 108      15016   94
#> 109      15024   13
#> 110      15304  165
#> 111      15370   17
#> 112      15376   30
#> 113      15412   19
#> 114      15624    7
#> 
#> attr(,"class")
#> [1] "skynet"
```
