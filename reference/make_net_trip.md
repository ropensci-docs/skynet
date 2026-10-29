# Trip directed network

Generates Trip/Route based Directed Network with an iGraph **gDir**
object, a Data Frame **netDir** and a Data Frame with Airport/Nodes
statistics **nodes**. Returns type of trip: OD = Origin/Destination
pair, OT = Origin/Transfer pair, TT = Transfer/Transfer pair, TD =
Transfer/Destination pair

## Usage

``` r
make_net_trip(x, carrier = FALSE)
```

## Arguments

- x:

  Data frame

- carrier:

  Groups data per carrier and OD

## Examples

``` r
if (FALSE) { # \dontrun{
make_net_trip(OD_Sample)
} # }
```
