# From To function

Calculate edges weight from IATA Code

## Usage

``` r
from_to_stats(x, y, orig)
```

## Arguments

- x:

  igraph object to query

- y:

  origin airport IATA code

- orig:

  "from" or "to" options

## Value

A numeric value with the sum of the weights (passengers) of the edges
leaving (`orig = "from"`) or arriving at (`orig = "to"`) airport `y`.

## Examples

``` r
netDir <- make_net_dir(OD_Sample)
from_to_stats(netDir$gDir, "JFK", orig = "from")
#> [1] 78

from_to_stats(netDir$gDir, "JFK", orig = "to")
#> [1] 267

```
