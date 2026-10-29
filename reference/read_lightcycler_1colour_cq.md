# Reads quantification cycle (cq) data in 1 colour from Roche Lightcyclers

This is the data from "export in text format" from the analysis tab in
the Lightcycler software. That software calls cq, "Cp".

## Usage

``` r
read_lightcycler_1colour_cq(
  filename,
  skip = 2,
  col_names = c("include", "color", "well", "sample_info", "cq", "concentration",
    "standard", "status"),
  col_types = "liccddil",
  ...
)
```

## Arguments

- filename:

  file name

- skip:

  number of lines to skip, defaults to 2

- col_names:

  names to give to columns

- col_types:

  data types of columns

- ...:

  other arguments to pass to read_tsv, if needed

## Value

tibble containing cq data

## Details

This function is a thin wrapper around readr::read_tsv.

## See also

read_lightcycler_1colour_raw

## Examples

``` r
read_lightcycler_1colour_cq(system.file("extdata/Edward_qPCR_Nrd1_calibration_2019-02-02_Cq.txt.gz", 
                                                 package = "tidyqpcr"))
#> # A tibble: 384 × 8
#>    include color well  sample_info    cq concentration standard status
#>    <lgl>   <int> <chr> <chr>       <dbl>         <dbl>    <int> <lgl> 
#>  1 TRUE      255 A1    Sample 1     22.8            NA        0 NA    
#>  2 TRUE      255 A2    Sample 2     24.7            NA        0 NA    
#>  3 TRUE      255 A3    Sample 3     26.8            NA        0 NA    
#>  4 TRUE      255 A4    Sample 4     28.6            NA        0 NA    
#>  5 TRUE    65280 A5    Sample 5     NA              NA        0 NA    
#>  6 TRUE    65280 A6    Sample 6     NA              NA        0 NA    
#>  7 TRUE      255 A7    Sample 7     23.2            NA        0 NA    
#>  8 TRUE      255 A8    Sample 8     24.8            NA        0 NA    
#>  9 TRUE      255 A9    Sample 9     26.9            NA        0 NA    
#> 10 TRUE    65280 A10   Sample 10    NA              NA        0 NA    
#> # ℹ 374 more rows
```
