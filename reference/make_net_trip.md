# Trip directed network

Generates Trip/Route based Directed Network with an iGraph **gDir**
object, a Data Frame **netDir** and a Data Frame with Airport/Nodes
statistics **nodes**. Returns type of trip: OD = Origin/Destination
pair, OT = Origin/Transfer pair, TT = Transfer/Transfer pair, TD =
Transfer/Destination pair

## Usage

``` r
make_net_trip(x, carrier = FALSE)
```

## Arguments

- x:

  Data frame

- carrier:

  Groups data per carrier and OD

## Value

An object of class `skynet`: a list with `gDir`, the igraph directed
network weighted by passengers, `netTrip`, a data frame with one row per
origin, destination and `route_type` (OD, OT, TT or TD) with passengers,
average fare and its standard deviation, yield, distance and city
information, and `nodes`, a data frame with the airport/node statistics
(see
[`node_stats`](https://docs.ropensci.org/skynet/reference/node_stats.md)).

## Examples

``` r
make_net_trip(OD_Sample)
#> $gDir
#> IGRAPH 4d78329 UNW- 251 2182 -- 
#> + attr: name (v/c), pass_dep (v/n), pass_arr (v/n), pass_tr (v/n),
#> | city_mkt_id (v/n), city (v/c), latitude (v/n), longitude (v/n),
#> | airport_city_name (v/c), airport_country_code (v/c), airport_state
#> | (v/c), airport_id (v/n), freq (v/n), route_type (e/c), weight (e/n),
#> | fare_sd (e/n), itin_fare (e/n), itin_yield (e/n), distance (e/n),
#> | year (e/n), quarter (e/n)
#> + edges from 4d78329 (vertex names):
#>  [1] ABE--IAD ABI--DFW ABQ--ATL ABQ--BWI ABQ--DFW ABQ--IAH ABQ--LBB ABQ--MDW
#>  [9] ABQ--MSP ABQ--ORD ABQ--PHX ABQ--SAN ABQ--SEA ABQ--SLC ABQ--STL ABY--ATL
#> [17] ACT--DFW ACY--FLL ACY--MYR AEX--ATL AGS--ATL AGS--CLT ALB--CLT ALB--LAS
#> + ... omitted several edges
#> 
#> $netTrip
#> # A tibble: 2,182 × 14
#> # Groups:   origin, dest, year, quarter [2,182]
#>    origin dest  route_type passengers fare_sd itin_fare itin_yield distance
#>    <chr>  <chr> <chr>           <int>   <dbl>     <dbl>      <dbl>    <dbl>
#>  1 ABE    IAD   OD                  1     0      271.       1.69        160
#>  2 ABI    DFW   OD                  1     0       35.4      0.224       158
#>  3 ABQ    ATL   OD                  1     0        2.66     0.0021     1269
#>  4 ABQ    BWI   OD                  1     0       78.5      0.047      1670
#>  5 ABQ    DFW   OD                  4    12.3     96.5      0.170       569
#>  6 ABQ    IAH   OD                  1     0      117.       0.157       744
#>  7 ABQ    LBB   OD                  1     0       65.2      0.226       289
#>  8 ABQ    MDW   OD                  2     0      170.       0.151      1121
#>  9 ABQ    MSP   OD                  1     0      413.       0.422       981
#> 10 ABQ    ORD   OD                  2     0      175.       0.156      1118
#> # ℹ 2,172 more rows
#> # ℹ 6 more variables: year <int>, quarter <int>, origin_city_mkt_id <int>,
#> #   origin_city <chr>, dest_city_mkt_id <int>, dest_city <chr>
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
```
