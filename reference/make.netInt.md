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

## Examples

``` r
if (FALSE) { # \dontrun{

make.netInt(skynet_example("T100_2011_int.csv"), OD_Sample, 1)

} # }
```
