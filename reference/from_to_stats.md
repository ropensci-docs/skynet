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

## Examples

``` r
if (FALSE) { # \dontrun{
netDir <- make.netDir(OD_Sample)
from_to_stats(netDir$gDir, "JFK", orig = "from")

from_to_stats(netDir$gDir, "JFK", orig = "to")
} # }
```
