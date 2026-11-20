# Displays a summary of a skynet object

Displays a summary of a skynet object

## Usage

``` r
# S3 method for class 'skynet'
summary(object, ...)
```

## Arguments

- object:

  skynet object to summarise

- ...:

  other arguments ignored (for compatibility with generic)

## Value

No return value, called for side effects: prints the years, quarters,
number of vertices/airports and number of edges/routes of the network to
the console.

## Examples

``` r
net <- make_net_dir(OD_Sample)
summary(net)
#> Skynet Object: 
#>  Year: 2011 
#>  Quarter: 1 
#>  Number of vertices/airports: 251 
#>  Number of edges/routes: 2182 
```
