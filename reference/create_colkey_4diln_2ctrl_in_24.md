# Create a 4-dilution column key for primer calibration

Creates a 24-column key for primer calibration, with 2x biol_reps and 2x
tech_reps, and 5-fold dilution until 5^4 of +RT; then -RT (no reverse
transcriptase), NT (no template) negative controls. That is a total of 6
versions of each sample replicate.

## Usage

``` r
create_colkey_4diln_2ctrl_in_24(
  dilution = c(5^(0:-3), 1, 1),
  dilution_nice = c("1x", "5x", "25x", "125x", "-RT", "NT"),
  prep_type = c(rep("+RT", 4), "-RT", "NT"),
  biol_rep = rep(c("A", "B"), each = 12, length.out = 24),
  tech_rep = rep(1:2, each = 6, length.out = 24)
)
```

## Arguments

- dilution:

  Numeric vector of length 6 describing sample dilutions

- dilution_nice:

  Character vector of length 6 with nice labels for sample dilutions

- prep_type:

  Character vector of length 6 describing type of sample (+RT, -RT, NT)

- biol_rep:

  Character vector of length 6 describing biological replicates

- tech_rep:

  Character vector of length 6 describing technical replicates

## Value

tibble (data frame) with 24 rows, and columns well_col, dilution,
dilution_nice, prep_type, biol_rep, tech_rep.

## See also

Other plate creation functions:
[`create_blank_plate()`](https://docs.ropensci.org/tidyqpcr/reference/create_blank_plate.md),
[`create_colkey_6_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_6_in_24.md),
[`create_colkey_6diln_2ctrl_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_6diln_2ctrl_in_24.md),
[`create_rowkey_4_in_16()`](https://docs.ropensci.org/tidyqpcr/reference/create_rowkey_4_in_16.md),
[`create_rowkey_8_in_16_plain()`](https://docs.ropensci.org/tidyqpcr/reference/create_rowkey_8_in_16_plain.md),
[`display_plate_qpcr()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate_qpcr.md),
[`display_plate_value()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate_value.md),
[`display_plate()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate.md),
[`label_plate_rowcol()`](https://docs.ropensci.org/tidyqpcr/reference/label_plate_rowcol.md),
[`make_row_names_echo1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_echo1536.md),
[`make_row_names_lc1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_lc1536.md)

## Examples

``` r
create_colkey_4diln_2ctrl_in_24()
#> # A tibble: 24 × 6
#>    well_col dilution dilution_nice prep_type biol_rep tech_rep
#>    <fct>       <dbl> <chr>         <fct>     <fct>    <fct>   
#>  1 1           1     1x            +RT       A        1       
#>  2 2           0.2   5x            +RT       A        1       
#>  3 3           0.04  25x           +RT       A        1       
#>  4 4           0.008 125x          +RT       A        1       
#>  5 5           1     -RT           -RT       A        1       
#>  6 6           1     NT            NT        A        1       
#>  7 7           1     1x            +RT       A        2       
#>  8 8           0.2   5x            +RT       A        2       
#>  9 9           0.04  25x           +RT       A        2       
#> 10 10          0.008 125x          +RT       A        2       
#> # ℹ 14 more rows
```
