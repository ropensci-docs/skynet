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

## Examples

``` r
net <- make_net_dir(OD_Sample)
#> Warning: `funs()` was deprecated in dplyr 0.8.0.
#> ℹ Please use a list of either functions or lambdas:
#> 
#> # Simple named list: list(mean = mean, median = median)
#> 
#> # Auto named with `tibble::lst()`: tibble::lst(mean, median)
#> 
#> # Using lambdas list(~ mean(., trim = .2), ~ median(., na.rm = TRUE))
#> ℹ The deprecated feature was likely used in the skynet package.
#>   Please report the issue at <https://github.com/ropensci/skynet/issues>.
summary(net)
#> Skynet Object: 
#>  Year: 2011 
#>  Quarter: 1 
#>  Number of vertices/airports: 251 
#>  Number of edges/routes: 2182 
```
