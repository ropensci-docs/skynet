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

## Examples

``` r
if (FALSE) { # \dontrun{
netDir <- make.netDir(OD_Sample)
disparity_filter(netDir$gDir, alpha = 0.003)
} # }
```
