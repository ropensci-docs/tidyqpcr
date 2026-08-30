# Create a plain 8-value, 16-row key for plates

Create a 16-row key with 8 values repeated over 16 plate rows. No other
information is included by default, hence "plain".

## Usage

``` r
create_rowkey_8_in_16_plain(...)
```

## Arguments

- ...:

  Vectors of length 8 describing well contents, e.g. sample or probe.

## Value

tibble (data frame) with 16 rows, and variables well_col, and supplied
values.

## Details

This helps to create plate layouts with standard designs.

## See also

Other plate creation functions:
[`create_blank_plate()`](https://docs.ropensci.org/tidyqpcr/reference/create_blank_plate.md),
[`create_colkey_4diln_2ctrl_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_4diln_2ctrl_in_24.md),
[`create_colkey_6_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_6_in_24.md),
[`create_colkey_6diln_2ctrl_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_6diln_2ctrl_in_24.md),
[`create_rowkey_4_in_16()`](https://docs.ropensci.org/tidyqpcr/reference/create_rowkey_4_in_16.md),
[`display_plate_qpcr()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate_qpcr.md),
[`display_plate_value()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate_value.md),
[`display_plate()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate.md),
[`label_plate_rowcol()`](https://docs.ropensci.org/tidyqpcr/reference/label_plate_rowcol.md),
[`make_row_names_echo1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_echo1536.md),
[`make_row_names_lc1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_lc1536.md)

## Examples

``` r
create_rowkey_8_in_16_plain(sample_id=c("me","you","them","him",
                                   "her","dog","cat","monkey"))
#> # A tibble: 16 × 2
#>    well_row sample_id
#>    <fct>    <chr>    
#>  1 A        me       
#>  2 B        you      
#>  3 C        them     
#>  4 D        him      
#>  5 E        her      
#>  6 F        dog      
#>  7 G        cat      
#>  8 H        monkey   
#>  9 I        me       
#> 10 J        you      
#> 11 K        them     
#> 12 L        him      
#> 13 M        her      
#> 14 N        dog      
#> 15 O        cat      
#> 16 P        monkey   
```
