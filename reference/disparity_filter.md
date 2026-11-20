# Disparity Filter

Uses the Serrano's disparity filter
(<https://en.wikipedia.org/wiki/Disparity_filter_algorithm_of_weighted_network>)
to extract the backbone of the network in "Extracting the multiscale
backbone of complex weighted networks"

## Usage

``` r
disparity_filter(g, alpha = 0.003)
```

## Arguments

- g:

  igraph object

- alpha:

  Alpha value. Default 0.003

## Value

An igraph object with the backbone of `g`: only the edges with a
disparity filter value below `alpha` are kept, and that value is stored
in the edge attribute `alpha`. Vertices left without edges are removed.

## Examples

``` r
netDir <- make_net_dir(OD_Sample)
disparity_filter(netDir$gDir, alpha = 0.003)
#> IGRAPH e64ac5b DNW- 36 33 -- 
#> + attr: name (v/c), pass_dep (v/n), pass_arr (v/n), pass_tr (v/n),
#> | city_mkt_id (v/n), city (v/c), latitude (v/n), longitude (v/n),
#> | airport_city_name (v/c), airport_country_code (v/c), airport_state
#> | (v/c), airport_id (v/n), freq (v/n), weight (e/n), fare_sd (e/n),
#> | itin_fare (e/n), itin_yield (e/n), distance (e/n), year (e/n),
#> | quarter (e/n), alpha (e/n)
#> + edges from e64ac5b (vertex names):
#>  [1] ATL->FLL ATL->MSY BNA->LGA BOS->SFO CAK->ATL DCA->DEN DEN->LAS DEN->MDW
#>  [9] DEN->PHX DFW->DCA EWR->BOS FLL->CLE FLL->JFK IAD->SLC IAH->LAS IAH->ORD
#> [17] LAS->DEN LAS->EWR LAX->JFK LGA->ORD MCO->HPN MCO->MHT MCO->MSP MDW->ISP
#> + ... omitted several edges
```
