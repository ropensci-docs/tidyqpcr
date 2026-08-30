# Display the value of each well across the plate.

Plots the plate with each well coloured by its value. Example values are
Cq, Delta Cq or Delta Delta Cq.

## Usage

``` r
display_plate_value(plate, value = "cq")
```

## Arguments

- plate:

  tibble with variables well_col, well_row, and the variable to be
  plotted.

- value:

  character vector selecting the variable in plate to plot as the well
  value

## Value

ggplot object; major output is to plot it

## Details

For a specific example see the calibration vignette:
[`vignette("calibration_vignette", package = "tidyqpcr")`](https://docs.ropensci.org/tidyqpcr/articles/calibration_vignette.md)

## See also

Other plate creation functions:
[`create_blank_plate()`](https://docs.ropensci.org/tidyqpcr/reference/create_blank_plate.md),
[`create_colkey_4diln_2ctrl_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_4diln_2ctrl_in_24.md),
[`create_colkey_6_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_6_in_24.md),
[`create_colkey_6diln_2ctrl_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_6diln_2ctrl_in_24.md),
[`create_rowkey_4_in_16()`](https://docs.ropensci.org/tidyqpcr/reference/create_rowkey_4_in_16.md),
[`create_rowkey_8_in_16_plain()`](https://docs.ropensci.org/tidyqpcr/reference/create_rowkey_8_in_16_plain.md),
[`display_plate_qpcr()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate_qpcr.md),
[`display_plate()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate.md),
[`label_plate_rowcol()`](https://docs.ropensci.org/tidyqpcr/reference/label_plate_rowcol.md),
[`make_row_names_echo1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_echo1536.md),
[`make_row_names_lc1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_lc1536.md)

## Examples

``` r
library(dplyr)
#> 
#> Attaching package: ‘dplyr’
#> The following objects are masked from ‘package:stats’:
#> 
#>     filter, lag
#> The following objects are masked from ‘package:base’:
#> 
#>     intersect, setdiff, setequal, union
library(ggplot2)

# create 96 well plate with random values
plate_randomcq <- create_blank_plate_96well() %>%
    mutate(cq = runif(96) * 10,
           deltacq = runif(96) * 2)


# display well Cq value across plate
display_plate_value(plate_randomcq)


# display well Delta Cq value across plate with red colour pallette
display_plate_value(plate_randomcq, value = "deltacq") +   # uses ggplot syntax
    scale_fill_gradient(high = "#FF0000") 

          
```
