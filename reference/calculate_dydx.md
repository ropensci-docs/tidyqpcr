# Calculate dy/dx vector from vectors y and x

Used in tidyqpcr to calculate dR/dT for a melt curve of fluorescence
signal R vs temperature T.

## Usage

``` r
calculate_dydx(x, y, method = "spline", ...)
```

## Arguments

- x:

  input variable, numeric vector, assumed to be temperature

- y:

  output variable, numeric vector of same length as x, assumed to be
  fluorescence signal.

- method:

  to use for smoothing:

  "spline" default, uses smoothing spline stats::smooth.spline.

  "diff" base::diff for lagged difference

- ...:

  other arguments to pass to smoothing method.

## Value

estimated first derivative of y with respect to x, numeric vector of
same length as y.

## See also

Other melt_curve_functions:
[`calculate_drdt_plate()`](https://docs.ropensci.org/tidyqpcr/reference/calculate_drdt_plate.md)

## Examples

``` r
# create simple curve
x = 1:5
y = x^2

# calculate gradient of curve
#----- use case 1 : using splines
calculate_dydx(x, y)
#> [1] -2.572999 -3.856780 -5.999883 -8.143689 -9.425360

# optional arguments are passed to smooth.splines function
calculate_dydx(x, y, spar = 0.5)
#> [1] -4.847839 -5.178761 -6.000000 -6.821239 -7.152161

#----- use case 2 : using difference between adjacent points
calculate_dydx(x, y, method = "diff")
#> [1] -3 -5 -7 -9 NA
```
