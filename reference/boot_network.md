# Network bootstrapping

Bootstraps a network and returns output containing three network
statistics: Average Path Length, Transitivity, Mean Betweenness.

## Usage

``` r
boot_network(g, n = 500, left_ci = 0.005, right_ci = 0.995)
```

## Arguments

- g:

  iGraph graph or skynet object.

- n:

  Number of bootstraps to run. (500 default)

- left_ci:

  Confidence interval left limit. (0.005 default)

- right_ci:

  Confidence interval left limit (0.995 default)

## Value

A data frame with one row per network statistic (`average.path.length`,
`transitivity` and `betweenness`) and four columns: the left and right
confidence limits of the statistic in the bootstrapped (randomly
rewired) networks, named after their quantiles (e.g. `0.5%` and
`99.5%`), `mean_random`, the mean value in the bootstrapped networks,
and `mean_empirical`, the value in the original network.

## Examples

``` r
net <- make_net_dir(OD_Sample)
boot_network(net, n = 10)
#>                            0.5%       99.5% mean_random mean_empirical
#> average.path.length   2.4493491   2.4700107   2.4619252      3.4255542
#> transitivity          0.3379659   0.3462258   0.3414765      0.3302566
#> betweenness         279.5642629 283.5920717 281.0462151    377.7058371

```
