# Find Airport function

Searches for airport information based on its IATA code or city name It
will display multiple airports as it works with partial names.

## Usage

``` r
find_airport(x)
```

## Arguments

- x:

  airport IATA code or city name

## Value

A data frame with the rows of `airportCode` whose IATA code (`origin`)
or `city` matches `x`, including the city market id (`city_mkt_id`),
`latitude` and `longitude`.

## Examples

``` r
find_airport("Atlanta")
#>    origin city_mkt_id                            city latitude longitude
#>    <char>       <int>                          <char>    <num>     <num>
#> 1:    ATL       30397 Atlanta, GA (Metropolitan Area) 33.64083 -84.42722
#> 2:    FTY       30397 Atlanta, GA (Metropolitan Area) 33.77917 -84.52139
#> 3:    GA3       30397 Atlanta, GA (Metropolitan Area) 33.31167 -84.76972
#> 4:    JAJ       30397 Atlanta, GA (Metropolitan Area) 33.76500 -84.41778
#> 5:    JAO       30397 Atlanta, GA (Metropolitan Area) 33.93333 -84.15000
#> 6:    JGL       30397 Atlanta, GA (Metropolitan Area) 33.58333 -84.46667
#> 7:    PDK       30397 Atlanta, GA (Metropolitan Area) 33.87500 -84.30222
#> 8:    QMA       30397 Atlanta, GA (Metropolitan Area) 34.01333 -84.60000

find_airport("ATL")
#>    origin city_mkt_id                            city latitude longitude
#>    <char>       <int>                          <char>    <num>     <num>
#> 1:    ATL       30397 Atlanta, GA (Metropolitan Area) 33.64083 -84.42722
```
