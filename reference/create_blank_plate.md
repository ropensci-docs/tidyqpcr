# Create a blank plate template as a tibble (with helper functions for common plate sizes)

For more help, examples and explanations, see the plate setup vignette:
[`vignette("platesetup_vignette", package = "tidyqpcr")`](https://docs.ropensci.org/tidyqpcr/articles/platesetup_vignette.md)

## Usage

``` r
create_blank_plate(well_row = LETTERS[1:16], well_col = 1:24)

create_blank_plate_96well()

create_blank_plate_1536well(
  well_row = make_row_names_lc1536(),
  well_col = 1:48
)
```

## Arguments

- well_row:

  Vector of Row labels, usually LETTERS

- well_col:

  Vector of Column labels, usually numbers

## Value

tibble (data frame) with columns well_row, well_col, well. This contains
all pairwise combinations of well_row and well_col, as well as
individual well names. Both well_row and well_col are coerced to factors
(even if well_col is supplied as numbers), to ensure order is
consistent.

However, well is a character vector as that is the default behaviour of
"unite", and display order doesn't matter.

Default value describes a full 384-well plate.

## Functions

- `create_blank_plate_96well`: create blank 96-well plate

- `create_blank_plate_1536well`: create blank 1536-well plate

## See also

Other plate creation functions:
[`create_colkey_4diln_2ctrl_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_4diln_2ctrl_in_24.md),
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
create_blank_plate(well_row=LETTERS[1:2],well_col=1:3)
#> # A tibble: 6 × 3
#>   well  well_row well_col
#>   <chr> <fct>    <fct>   
#> 1 A1    A        1       
#> 2 A2    A        2       
#> 3 A3    A        3       
#> 4 B1    B        1       
#> 5 B2    B        2       
#> 6 B3    B        3       

create_blank_plate_96well()
#> # A tibble: 96 × 3
#>    well  well_row well_col
#>    <chr> <fct>    <fct>   
#>  1 A1    A        1       
#>  2 A2    A        2       
#>  3 A3    A        3       
#>  4 A4    A        4       
#>  5 A5    A        5       
#>  6 A6    A        6       
#>  7 A7    A        7       
#>  8 A8    A        8       
#>  9 A9    A        9       
#> 10 A10   A        10      
#> # ℹ 86 more rows

create_blank_plate_1536well()
#> # A tibble: 1,536 × 3
#>    well  well_row well_col
#>    <chr> <fct>    <fct>   
#>  1 Aa1   Aa       1       
#>  2 Aa2   Aa       2       
#>  3 Aa3   Aa       3       
#>  4 Aa4   Aa       4       
#>  5 Aa5   Aa       5       
#>  6 Aa6   Aa       6       
#>  7 Aa7   Aa       7       
#>  8 Aa8   Aa       8       
#>  9 Aa9   Aa       9       
#> 10 Aa10  Aa       10      
#> # ℹ 1,526 more rows

# create blank 96-well plate with empty edge wells

create_blank_plate(well_row=LETTERS[2:7], well_col=2:11)
#> # A tibble: 60 × 3
#>    well  well_row well_col
#>    <chr> <fct>    <fct>   
#>  1 B2    B        2       
#>  2 B3    B        3       
#>  3 B4    B        4       
#>  4 B5    B        5       
#>  5 B6    B        6       
#>  6 B7    B        7       
#>  7 B8    B        8       
#>  8 B9    B        9       
#>  9 B10   B        10      
#> 10 B11   B        11      
#> # ℹ 50 more rows

# create blank 1536-well plate with empty edge wells

full_plate_row_names <- make_row_names_lc1536()

create_blank_plate(well_row=full_plate_row_names[2:31], well_col=2:47)
#> # A tibble: 1,380 × 3
#>    well  well_row well_col
#>    <chr> <fct>    <fct>   
#>  1 Ab2   Ab       2       
#>  2 Ab3   Ab       3       
#>  3 Ab4   Ab       4       
#>  4 Ab5   Ab       5       
#>  5 Ab6   Ab       6       
#>  6 Ab7   Ab       7       
#>  7 Ab8   Ab       8       
#>  8 Ab9   Ab       9       
#>  9 Ab10  Ab       10      
#> 10 Ab11  Ab       11      
#> # ℹ 1,370 more rows
```
