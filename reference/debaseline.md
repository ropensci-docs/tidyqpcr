# Remove baseline from amplification curves (BETA)

Remove baseline from qPCR amplification curves by subtracting median of
initial cycles.

## Usage

``` r
debaseline(plateamp, maxcycle = 10)
```

## Arguments

- plateamp:

  data frame with plate amplification data, including variables well,
  cycle, fluor_raw (raw fluorescence value), and program_no. Assume
  program 2 for amplification curves from Roche Lightcycler format data.

- maxcycle:

  maximum cycle value to use for baseline, before amplification.

## Value

platemap with additional columns per well:

|              |                                                             |
|--------------|-------------------------------------------------------------|
| fluor_base   | baseline /background value                                  |
| fluor_signal | normalized fluorescence signal, i.e. fluor_raw - fluor_base |

## Details

BETA function version because:

\- assumes Roche Lightcycler format, we should ideally replace
"program_no == 2" by something more generic?

\- the rule-of thumb "baseline is median of initial 10 cycles" has not
been tested robustly

## Examples

``` r
# create simple dataset of raw fluorescence
# with two samples over 15 cycles
raw_fluor_tibble <- tibble(sample_id = rep(c("S1", "S2"), each = 15),
                          target_id = "T1",
                          well_row = "A",
                          well_col = rep(c(1, 2), each = 15),
                          well = rep(c("A1", "A2"), each = 15),
                          cycle = rep(1:15,2),
                          fluor_raw = c(1:15, 6:20),
                          program_no = 2)

# remove base fluorescence from dataset
raw_fluor_tibble %>%
    debaseline()
#> # A tibble: 30 × 10
#>    sample_id target_id well_row well_col well  cycle fluor_raw program_no
#>    <chr>     <chr>     <chr>       <dbl> <chr> <int>     <int>      <dbl>
#>  1 S1        T1        A               1 A1        1         1          2
#>  2 S1        T1        A               1 A1        2         2          2
#>  3 S1        T1        A               1 A1        3         3          2
#>  4 S1        T1        A               1 A1        4         4          2
#>  5 S1        T1        A               1 A1        5         5          2
#>  6 S1        T1        A               1 A1        6         6          2
#>  7 S1        T1        A               1 A1        7         7          2
#>  8 S1        T1        A               1 A1        8         8          2
#>  9 S1        T1        A               1 A1        9         9          2
#> 10 S1        T1        A               1 A1       10        10          2
#> # ℹ 20 more rows
#> # ℹ 2 more variables: fluor_base <dbl>, fluor_signal <dbl>
    
```
