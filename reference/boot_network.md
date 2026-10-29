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

## Examples

``` r
if (FALSE) { # \dontrun{
boot_net(g, n = 500)

} # }
```
