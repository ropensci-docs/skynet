# International Data

Imports International data to complement to the DB1B data set. NOTE:
When using this function, certain variables will be skewed as the T100
dataset does not contain all the data the DB1B dataset contains.

## Usage

``` r
make.netInt(x = NULL, m = NULL, Q = NULL)
```

## Arguments

- x:

  T-100 International Segment csv file

- m:

  Data set to merge with

- Q:

  Desired T-100 Quarter. Should be equal to 1, 2, 3 or 4.

## Value

No return value, called for side effects. The function is deprecated and
only issues a warning pointing to
[`import_t100`](https://docs.ropensci.org/skynet/reference/import_t100.md).

## Examples

``` r
make.netInt(skynet_example("T100_2011_int.csv"), OD_Sample, 1)
#> Warning: netInt function is deprecated, please use `import_t100()`,
#>         generate your desired network and rbind() with the db1b network of choice.
```
