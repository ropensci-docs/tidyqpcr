# Calculate dR/dT of melt curves for of every well in a plate.

dR/dT, the derivative of the melt curve (of fluorescence signal R vs
temperature T), has a maximum at the melting temperature Tm. A single
peak in this suggests a single-length PCR product is present in the
well.

## Usage

``` r
calculate_drdt_plate(platemelt, method = "spline", ...)
```

## Arguments

- platemelt:

  data frame describing melt curves, including variables well,
  temperature, fluor_raw (raw fluorescence value).

- method:

  to use for smoothing:

  "spline" default, uses smoothing spline stats::smooth.spline.

  "diff" base::diff for lagged difference

- ...:

  other arguments to pass to smoothing method.

## Value

platemelt with additional column dRdT.

## Details

Note that this function does not group by plate, only by well. The
function will give strange results if you pass it data from more than
one plate. Avoid this by analysing one plate at a time.

## See also

Other melt_curve_functions:
[`calculate_dydx()`](https://docs.ropensci.org/tidyqpcr/reference/calculate_dydx.md)

## Examples

``` r
# create simple curve
# create simple dataset of raw fluorescence with two samples
temp_tibble <- tibble(sample_id = rep(c("S1", "S2"), each = 10),
                          target_id = "T1",
                          well_row = "A",
                          well_col = rep(c(1, 2), each = 10),
                          well = rep(c("A1", "A2"), each = 10),
                          temperature = rep(56:65,2),
                          fluor_raw = c(1:10, 6:15))

# calculate drdt of all melt curves
#----- use case 1 : using splines
temp_tibble %>%
    calculate_drdt_plate()
#> # A tibble: 20 × 8
#>    sample_id target_id well_row well_col well  temperature fluor_raw   dRdT
#>    <chr>     <chr>     <chr>       <dbl> <chr>       <int>     <int>  <dbl>
#>  1 S1        T1        A               1 A1             56         1 -1.00 
#>  2 S1        T1        A               1 A1             57         2 -1    
#>  3 S1        T1        A               1 A1             58         3 -1.00 
#>  4 S1        T1        A               1 A1             59         4 -1.00 
#>  5 S1        T1        A               1 A1             60         5 -1.000
#>  6 S1        T1        A               1 A1             61         6 -1.000
#>  7 S1        T1        A               1 A1             62         7 -1    
#>  8 S1        T1        A               1 A1             63         8 -1.000
#>  9 S1        T1        A               1 A1             64         9 -1.00 
#> 10 S1        T1        A               1 A1             65        10 -1.00 
#> 11 S2        T1        A               2 A2             56         6 -1.00 
#> 12 S2        T1        A               2 A2             57         7 -1    
#> 13 S2        T1        A               2 A2             58         8 -1.000
#> 14 S2        T1        A               2 A2             59         9 -1.000
#> 15 S2        T1        A               2 A2             60        10 -1    
#> 16 S2        T1        A               2 A2             61        11 -1.00 
#> 17 S2        T1        A               2 A2             62        12 -1.00 
#> 18 S2        T1        A               2 A2             63        13 -1.000
#> 19 S2        T1        A               2 A2             64        14 -1.00 
#> 20 S2        T1        A               2 A2             65        15 -1.000

# optional arguments are passed to smooth.splines function
temp_tibble %>%
    calculate_drdt_plate(spar = 0.5)
#> # A tibble: 20 × 8
#>    sample_id target_id well_row well_col well  temperature fluor_raw   dRdT
#>    <chr>     <chr>     <chr>       <dbl> <chr>       <int>     <int>  <dbl>
#>  1 S1        T1        A               1 A1             56         1 -1.000
#>  2 S1        T1        A               1 A1             57         2 -1.000
#>  3 S1        T1        A               1 A1             58         3 -1.000
#>  4 S1        T1        A               1 A1             59         4 -1.000
#>  5 S1        T1        A               1 A1             60         5 -1.000
#>  6 S1        T1        A               1 A1             61         6 -1.000
#>  7 S1        T1        A               1 A1             62         7 -1    
#>  8 S1        T1        A               1 A1             63         8 -1.00 
#>  9 S1        T1        A               1 A1             64         9 -1.00 
#> 10 S1        T1        A               1 A1             65        10 -1.00 
#> 11 S2        T1        A               2 A2             56         6 -1.000
#> 12 S2        T1        A               2 A2             57         7 -1.000
#> 13 S2        T1        A               2 A2             58         8 -1.000
#> 14 S2        T1        A               2 A2             59         9 -1.000
#> 15 S2        T1        A               2 A2             60        10 -1.000
#> 16 S2        T1        A               2 A2             61        11 -1.000
#> 17 S2        T1        A               2 A2             62        12 -1    
#> 18 S2        T1        A               2 A2             63        13 -1.00 
#> 19 S2        T1        A               2 A2             64        14 -1.00 
#> 20 S2        T1        A               2 A2             65        15 -1.00 

#----- use case 2 : using difference between adjacent points
temp_tibble %>%
    calculate_drdt_plate(method = "diff")
#> # A tibble: 20 × 8
#>    sample_id target_id well_row well_col well  temperature fluor_raw  dRdT
#>    <chr>     <chr>     <chr>       <dbl> <chr>       <int>     <int> <dbl>
#>  1 S1        T1        A               1 A1             56         1    -1
#>  2 S1        T1        A               1 A1             57         2    -1
#>  3 S1        T1        A               1 A1             58         3    -1
#>  4 S1        T1        A               1 A1             59         4    -1
#>  5 S1        T1        A               1 A1             60         5    -1
#>  6 S1        T1        A               1 A1             61         6    -1
#>  7 S1        T1        A               1 A1             62         7    -1
#>  8 S1        T1        A               1 A1             63         8    -1
#>  9 S1        T1        A               1 A1             64         9    -1
#> 10 S1        T1        A               1 A1             65        10    NA
#> 11 S2        T1        A               2 A2             56         6    -1
#> 12 S2        T1        A               2 A2             57         7    -1
#> 13 S2        T1        A               2 A2             58         8    -1
#> 14 S2        T1        A               2 A2             59         9    -1
#> 15 S2        T1        A               2 A2             60        10    -1
#> 16 S2        T1        A               2 A2             61        11    -1
#> 17 S2        T1        A               2 A2             62        12    -1
#> 18 S2        T1        A               2 A2             63        13    -1
#> 19 S2        T1        A               2 A2             64        14    -1
#> 20 S2        T1        A               2 A2             65        15    NA
```
