# Power Law

Plots power law fit

## Usage

``` r
fit_power(graph)
```

## Arguments

- graph:

  iGraph object

## Value

A ggplot object plotting the log of the degree probability against the
log of the degree, with the fitted linear regression line and the name
of the node with the highest degree. The fitted alpha (minus the slope)
and the R squared of the fit are printed as messages.

## Examples

``` r
netDir <- make_net_dir(OD_Sample)
fit_power(netDir$gDir)
#> Alpha = 0.731
#> R square = 0.693

```
