# Create Nodes

Creates nodes for SKYNET's functions. Despite being possible to use it
individually, it's mainly meant to be used as a complimentary function.

## Usage

``` r
createNodes(y)
```

## Arguments

- y:

  Data Frame

## Value

A data frame with one row per airport: `origin` (airport IATA code),
`freq` (number of departing plus arriving passengers) and the airport
information from `airportCode` (`city_mkt_id`, `city`, `latitude` and
`longitude`).

## Examples

``` r
createNodes(OD_Sample)
```
