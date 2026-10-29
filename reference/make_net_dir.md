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

## Examples

``` r
if (FALSE) { # \dontrun{
make_net_dir(OD_Sample)

# Apply Disparity Filter
make_net_dir(OD_Sample, disp = TRUE, alpha = 0.05)

# Apply Percentage Cap
make_net_dir(OD_Sample, cap = TRUE, pct = 20)
} # }
```
