# Create a 6-value, 24-column key for plates

Create a 24-column key with 6 values repeated over 24 plate columns.
Each of the 6 values is repeated over 3x +RT Techreps and 1x -RT.

## Usage

``` r
create_colkey_6_in_24(...)
```

## Arguments

- ...:

  Vectors of length 6 describing well contents, e.g. sample_id or
  target_id

## Value

tibble (data frame) with 24 rows, and columns well_col, prep_type,
tech_rep, and supplied values.

## Details

This helps to create plate layouts with standard designs.

## See also

Other plate creation functions:
[`create_blank_plate()`](https://docs.ropensci.org/tidyqpcr/reference/create_blank_plate.md),
[`create_colkey_4diln_2ctrl_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_4diln_2ctrl_in_24.md),
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
create_colkey_6_in_24(sample_id=LETTERS[1:6])
#> # A tibble: 24 × 4
#>    well_col prep_type tech_rep sample_id
#>    <fct>    <fct>     <fct>    <chr>    
#>  1 1        +RT       1        A        
#>  2 2        +RT       1        B        
#>  3 3        +RT       1        C        
#>  4 4        +RT       1        D        
#>  5 5        +RT       1        E        
#>  6 6        +RT       1        F        
#>  7 7        +RT       2        A        
#>  8 8        +RT       2        B        
#>  9 9        +RT       2        C        
#> 10 10       +RT       2        D        
#> # ℹ 14 more rows
```
