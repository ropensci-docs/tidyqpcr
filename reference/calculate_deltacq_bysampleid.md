# Calculate delta cq (\\\Delta Cq\\) to normalize quantification cycle (log2-fold) data within sample_id.

This function implements relative quantification by the delta Cq method.
For each sample, the Cq values of all targets (e.g. genes, probes,
primer sets) are compared to one or more reference target ids specified
in \`ref_target_ids\`.

## Usage

``` r
calculate_deltacq_bysampleid(cq_df, ref_target_ids, norm_function = median)
```

## Arguments

- cq_df:

  a data frame containing columns \`sample_id\`, value_name (default
  \`cq\`) and tid_name (default \`target_id\`). Crucially, sample_id
  should be the same for different technical replicates measuring
  identical reactions in different wells of the plate, but differ for
  different biological and experimental replicates. See tidyqpcr
  vignettes for examples.

- ref_target_ids:

  names of targets to normalize by, i.e. reference genes, hydrolysis
  probes, or primer sets. This can be one reference target id, a
  selection of multiple target ids, or even all measured target ids. In
  the case of all of them, the delta Cq value would be calculated
  relative to the median (or other \`norm_function\`) of all measured
  targets.

- norm_function:

  Function to use to calculate the value to normalize by on given scale.
  Default is median, alternatively could use mean.

## Value

data frame like cq_df with three additional columns:

|           |                                                         |
|-----------|---------------------------------------------------------|
| ref_cq    | summary (median/mean) cq value for reference target ids |
| delta_cq  | normalized value, \\\Delta Cq\\                         |
| rel_abund | normalized ratio, \\2^(-\Delta Cq)\\                    |

## Examples

``` r
# create simple cq dataset with two samples, two targets  and 3 reps
cq_tibble <- tibble(sample_id = rep(c("S_1","S_1","S_1", "S_2", "S_2", "S_2"), 2),
                     target_id = rep(c("T_1",
                                       "T_norm"), each = 6),
                     tech_rep = rep(1:3, 4),
                     well_row = rep(c("A",
                                      "B"), each = 6),
                     well_col = rep(1:6, 2),
                     well = paste0(well_row, well_col),
                     cq = c(10, 10, 10, 12, 12, 11,
                             9,  9,  9,  9,  9,  9))
                     
# calculate deltacq using reference target_id called 'T_norm'

#----- use case 1: median reference target_id value
cq_tibble %>%
    calculate_deltacq_bysampleid(ref_target_ids = "T_norm")
#> # A tibble: 12 × 10
#>    sample_id target_id tech_rep well_row well_col well     cq ref_cq delta_cq
#>    <chr>     <chr>        <int> <chr>       <int> <chr> <dbl>  <dbl>    <dbl>
#>  1 S_1       T_1              1 A               1 A1       10      9        1
#>  2 S_1       T_1              2 A               2 A2       10      9        1
#>  3 S_1       T_1              3 A               3 A3       10      9        1
#>  4 S_1       T_norm           1 B               1 B1        9      9        0
#>  5 S_1       T_norm           2 B               2 B2        9      9        0
#>  6 S_1       T_norm           3 B               3 B3        9      9        0
#>  7 S_2       T_1              1 A               4 A4       12      9        3
#>  8 S_2       T_1              2 A               5 A5       12      9        3
#>  9 S_2       T_1              3 A               6 A6       11      9        2
#> 10 S_2       T_norm           1 B               4 B4        9      9        0
#> 11 S_2       T_norm           2 B               5 B5        9      9        0
#> 12 S_2       T_norm           3 B               6 B6        9      9        0
#> # ℹ 1 more variable: rel_abund <dbl>

#----- use case 2: mean reference target_id value 
cq_tibble %>%
    calculate_deltacq_bysampleid(ref_target_ids = "T_norm",
                                 norm_function = mean)
#> # A tibble: 12 × 10
#>    sample_id target_id tech_rep well_row well_col well     cq ref_cq delta_cq
#>    <chr>     <chr>        <int> <chr>       <int> <chr> <dbl>  <dbl>    <dbl>
#>  1 S_1       T_1              1 A               1 A1       10      9        1
#>  2 S_1       T_1              2 A               2 A2       10      9        1
#>  3 S_1       T_1              3 A               3 A3       10      9        1
#>  4 S_1       T_norm           1 B               1 B1        9      9        0
#>  5 S_1       T_norm           2 B               2 B2        9      9        0
#>  6 S_1       T_norm           3 B               3 B3        9      9        0
#>  7 S_2       T_1              1 A               4 A4       12      9        3
#>  8 S_2       T_1              2 A               5 A5       12      9        3
#>  9 S_2       T_1              3 A               6 A6       11      9        2
#> 10 S_2       T_norm           1 B               4 B4        9      9        0
#> 11 S_2       T_norm           2 B               5 B5        9      9        0
#> 12 S_2       T_norm           3 B               6 B6        9      9        0
#> # ℹ 1 more variable: rel_abund <dbl>
```
