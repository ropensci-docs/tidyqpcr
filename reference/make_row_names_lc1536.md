# Generates row names for the Roche Lightcycler (tm) 1536-well plates

Creates a vector containing 36 row names according to the labelling
system used by the Roche Lightcycler (tm)

## Usage

``` r
make_row_names_lc1536()
```

## Value

Vector of row names: Aa,Ab,Ac,Ad,Ba,...,Hd.

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
[`make_row_names_echo1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_echo1536.md)

## Examples

``` r
make_row_names_lc1536()
#>  [1] "Aa" "Ab" "Ac" "Ad" "Ba" "Bb" "Bc" "Bd" "Ca" "Cb" "Cc" "Cd" "Da" "Db" "Dc"
#> [16] "Dd" "Ea" "Eb" "Ec" "Ed" "Fa" "Fb" "Fc" "Fd" "Ga" "Gb" "Gc" "Gd" "Ha" "Hb"
#> [31] "Hc" "Hd"
```
