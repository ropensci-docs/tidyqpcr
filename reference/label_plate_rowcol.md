# Label a plate with sample and probe information

For more help, examples and explanations, see the plate setup vignette:
[`vignette("platesetup_vignette", package = "tidyqpcr")`](https://docs.ropensci.org/tidyqpcr/articles/platesetup_vignette.md)

## Usage

``` r
label_plate_rowcol(plate, rowkey = NULL, colkey = NULL, coercefactors = TRUE)
```

## Arguments

- plate:

  tibble (data frame) with variables well_row, well_col, well. This
  would usually be produced by create_blank_plate(). It is possible to
  include other information in additional variables.

- rowkey:

  tibble (data frame) describing plate rows, with variables well_row and
  others.

- colkey:

  tibble (data frame) describing plate columns, with variables well_col
  and others.

- coercefactors:

  if TRUE, coerce well_row in rowkey and well_col in colkey to factors

## Value

tibble (data frame) with variables well_row, well_col, well, and others.

This tibble contains all combinations of well_row and well_col found in
the input plate, and all information supplied in rowkey and colkey
distributed across every well of the plate. Return plate is ordered by
row well_row then column well_col.

Note this ordering may cause a problem if well_col is supplied as a
character (1,10,11,...), instead of a factor or integer (1,2,3,...). For
this reason, the function by default converts well_row in \`rowkey\`,
and well_col in \`colkey\`, to factors, taking factor levels from
\`plate\`, and messages the user.

If \`plate\$well_col\` or \`plate\$well_row\` are not factors and
coercefactors = TRUE label_plate_rowcol will automatically convert them
to factors, but will output a warning telling users this may lead to
unexpected behaviour.

Other tidyqpcr functions require plate plans to contain variables
sample_id, target_id, and prep_type, so \`label_plate_rowcol\` will
message if any of these are missing. This is a message, not an error,
because these variables can be added by users later.

## Details

For worked examples of tidyqpcr analysis with 384-well plates, see:
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
[`display_plate_value()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate_value.md),
[`display_plate()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate.md),
[`make_row_names_echo1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_echo1536.md),
[`make_row_names_lc1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_lc1536.md)

## Examples

``` r
label_plate_rowcol(plate = create_blank_plate()) # returns blank plate
#> plate does not contain variable sample_id
#> plate does not have variable target_id
#> plate does not have variable prep_type
#> # A tibble: 384 × 3
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
#> # ℹ 374 more rows

# label blank 96-well plate with empty edge wells

label_plate_rowcol(plate = create_blank_plate(well_row = LETTERS[2:7], 
                                              well_col = 2:11))
#> plate does not contain variable sample_id
#> plate does not have variable target_id
#> plate does not have variable prep_type
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

# label 96-well plate with sample id in rows

label_plate_rowcol(plate = create_blank_plate(well_row = LETTERS[1:8],
                                              well_col = 1:12),
                   rowkey = tibble(well_row = LETTERS[1:8],
                                   sample_id = paste0("S_",1:8)))
#> coercing well_row to a factor with levels from plate$well_row
#> plate does not have variable target_id
#> plate does not have variable prep_type
#> # A tibble: 96 × 4
#>    well  well_row well_col sample_id
#>    <chr> <fct>    <fct>    <chr>    
#>  1 A1    A        1        S_1      
#>  2 A2    A        2        S_1      
#>  3 A3    A        3        S_1      
#>  4 A4    A        4        S_1      
#>  5 A5    A        5        S_1      
#>  6 A6    A        6        S_1      
#>  7 A7    A        7        S_1      
#>  8 A8    A        8        S_1      
#>  9 A9    A        9        S_1      
#> 10 A10   A        10       S_1      
#> # ℹ 86 more rows

# label fraction of 96-well plate with target id in columns

label_plate_rowcol(plate = create_blank_plate(well_row = LETTERS[1:8],
                                              well_col = 1:4),
                   colkey = tibble(well_col = 1:4,
                                   target_id = paste0("T_",1:4)))
#> coercing well_col to a factor with levels from plate$well_col
#> plate does not contain variable sample_id
#> plate does not have variable prep_type
#> # A tibble: 32 × 4
#>    well  well_row well_col target_id
#>    <chr> <fct>    <fct>    <chr>    
#>  1 A1    A        1        T_1      
#>  2 A2    A        2        T_2      
#>  3 A3    A        3        T_3      
#>  4 A4    A        4        T_4      
#>  5 B1    B        1        T_1      
#>  6 B2    B        2        T_2      
#>  7 B3    B        3        T_3      
#>  8 B4    B        4        T_4      
#>  9 C1    C        1        T_1      
#> 10 C2    C        2        T_2      
#> # ℹ 22 more rows
```
