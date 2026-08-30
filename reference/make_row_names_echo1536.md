# Generates row names for the Labcyte Echo 1536-well plates

Creates a vector containing 36 row names according to the labelling
system used by the Labcyte Echo

## Usage

``` r
make_row_names_echo1536()
```

## Value

Vector of row names: A,B,...,Z,AA,AB,...,AF.

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
[`label_plate_rowcol()`](https://docs.ropensci.org/tidyqpcr/reference/label_plate_rowcol.md),
[`make_row_names_lc1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_lc1536.md)

## Examples

``` r
make_row_names_echo1536()
#>  [1] "A"  "B"  "C"  "D"  "E"  "F"  "G"  "H"  "I"  "J"  "K"  "L"  "M"  "N"  "O" 
#> [16] "P"  "Q"  "R"  "S"  "T"  "U"  "V"  "W"  "X"  "Y"  "Z"  "AA" "AB" "AC" "AD"
#> [31] "AE" "AF"
```
