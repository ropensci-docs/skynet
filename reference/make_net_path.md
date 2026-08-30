# Path and OD Network

Generates an OD network and a Leg Count data frame(on demand)

## Usage

``` r
make_net_path(x, leg = FALSE, zero = FALSE, carrier = FALSE)
```

## Arguments

- x:

  Data frame

- leg:

  Generates Leg Count Data frame, based on Path taken.

- zero:

  Displays percentage of 0 usd tickets

- carrier:

  Groups data per airline

  For example, all passengers doing the BOS-ATL-LAX path, are summed by
  Air Carrier.

## Examples

``` r
if (FALSE) { # \dontrun{
make_net_path(OD_Sample)

# Generate Leg Count
make_net_path(OD_Sample, leg = TRUE)
} # }
```
