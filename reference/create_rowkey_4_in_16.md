# Create a 4-value, 16-row key for plates

Create a 16-row key with 4 values repeated over 16 plate rows. Each of
the 4 values is repeated over 3x +RT Techreps and 1x -RT.

## Usage

``` r
create_rowkey_4_in_16(...)
```

## Arguments

- ...:

  Vectors of length 4 describing well contents, e.g. sample_id or
  target_id

## Value

tibble (data frame) with 16 rows, and variables well_row, prep_type,
tech_rep, and supplied values.

## Details

This helps to create plate layouts with standard designs.

## See also

Other plate creation functions:
[`create_blank_plate()`](https://docs.ropensci.org/tidyqpcr/reference/create_blank_plate.md),
[`create_colkey_4diln_2ctrl_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_4diln_2ctrl_in_24.md),
[`create_colkey_6_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_6_in_24.md),
[`create_colkey_6diln_2ctrl_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_6diln_2ctrl_in_24.md),
[`create_rowkey_8_in_16_plain()`](https://docs.ropensci.org/tidyqpcr/reference/create_rowkey_8_in_16_plain.md),
[`display_plate_qpcr()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate_qpcr.md),
[`display_plate_value()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate_value.md),
[`display_plate()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate.md),
[`label_plate_rowcol()`](https://docs.ropensci.org/tidyqpcr/reference/label_plate_rowcol.md),
[`make_row_names_echo1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_echo1536.md),
[`make_row_names_lc1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_lc1536.md)

## Examples

``` r
create_rowkey_4_in_16(sample_id=c("sheep","goat","cow","chicken"))
#> # A tibble: 16 × 4
#>    well_row prep_type tech_rep sample_id
#>    <fct>    <fct>     <fct>    <chr>    
#>  1 A        +RT       1        sheep    
#>  2 B        +RT       1        goat     
#>  3 C        +RT       1        cow      
#>  4 D        +RT       1        chicken  
#>  5 E        +RT       2        sheep    
#>  6 F        +RT       2        goat     
#>  7 G        +RT       2        cow      
#>  8 H        +RT       2        chicken  
#>  9 I        +RT       3        sheep    
#> 10 J        +RT       3        goat     
#> 11 K        +RT       3        cow      
#> 12 L        +RT       3        chicken  
#> 13 M        -RT       1        sheep    
#> 14 N        -RT       1        goat     
#> 15 O        -RT       1        cow      
#> 16 P        -RT       1        chicken  
```
