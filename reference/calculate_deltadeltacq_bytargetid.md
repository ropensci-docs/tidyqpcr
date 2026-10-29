# Calculate delta delta cq (\\\Delta \Delta Cq\\) to globally normalize quantification cycle (log2-fold) data across sample_id.

By default, \\\Delta \Delta Cq\\ is positive if a target is more highly
detected in the relevant sample, compared to reference samples. This can
be flipped by setting the parameter \`ddcq_positive\` to \`FALSE\`. In
either case, The fold change, \\2^{\Delta \Delta Cq}\\, is also
reported.

## Usage

``` r
calculate_deltadeltacq_bytargetid(
  deltacq_df,
  ref_sample_ids,
  norm_function = median,
  ddcq_positive = TRUE
)
```

## Arguments

- deltacq_df:

  a data frame containing columns \`sample_id\`, value_name (default
  \`delta_cq\`) and tid_name (default \`target_id\`). Crucially,
  sample_id should be the same for different technical replicates
  measuring identical reactions in different wells of the plate, but
  differ for different biological and experimental replicates.

  Usually this will be a data frame that was output by
  \`calculate_deltacq_bysampleid\`.

- ref_sample_ids:

  reference sample_ids to normalize by

- norm_function:

  Function to use to calculate the value to normalize by on given scale.
  Default is median, alternatively could use mean.

- ddcq_positive:

  (default TRUE) output \\\Delta \Delta Cq\\ as positive if a target is
  more highly detected in the relevant sample, compared to reference
  samples.

## Value

data frame like cq_df with three additional columns:

|  |  |
|----|----|
| ref_delta_cq | summary (median/mean) \\\Delta Cq\\ value for target_id in reference sample ids |
| deltadelta_cq | the normalized value, \\\Delta \Delta Cq\\ |
| fold_change | the normalized fold-change ratio, \\2^(-\Delta \Delta Cq)\\ |

## Details

This function does a global normalization, where all samples are
compared to one or more reference samples specified in
\`ref_sample_ids\`. There are other experimental designs that require
comparing samples in pairs or small groups, e.g. a time course comparing
\`delta_cq\` values against a reference strain at each time point. For
those situations, instead we recommend adapting code from this function,
changing the grouping variables used in to \`dplyr::group_by\` to draw
the contrasts appropriate for the experiment.

## Examples

``` r
# create simple deltacq dataset with two samples, two targets and 3 reps
deltacq_tibble <- tibble(sample_id = rep(c("S_1","S_1","S_1", "S_norm", "S_norm", "S_norm"), 2),
                     target_id = rep(c("T_1",
                                       "T_2"), each = 6),
                     tech_rep = rep(1:3, 4),
                     well_row = rep(c("A",
                                      "B"), each = 6),
                     well_col = rep(1:6, 2),
                     well = paste0(well_row,well_col),
                     delta_cq = c(1, 1, 1, 3, 3, 2,
                                  4, 5, 4, 5, 5, 5))
                     
# calculate deltadeltacq using reference target_id called 'S_norm'

#----- use case 1: median reference sample_id value
deltacq_tibble %>%
    calculate_deltadeltacq_bytargetid(ref_sample_ids = "S_norm")
#> # A tibble: 12 × 10
#>    sample_id target_id tech_rep well_row well_col well  delta_cq ref_delta_cq
#>    <chr>     <chr>        <int> <chr>       <int> <chr>    <dbl>        <dbl>
#>  1 S_1       T_1              1 A               1 A1           1            3
#>  2 S_1       T_1              2 A               2 A2           1            3
#>  3 S_1       T_1              3 A               3 A3           1            3
#>  4 S_norm    T_1              1 A               4 A4           3            3
#>  5 S_norm    T_1              2 A               5 A5           3            3
#>  6 S_norm    T_1              3 A               6 A6           2            3
#>  7 S_1       T_2              1 B               1 B1           4            5
#>  8 S_1       T_2              2 B               2 B2           5            5
#>  9 S_1       T_2              3 B               3 B3           4            5
#> 10 S_norm    T_2              1 B               4 B4           5            5
#> 11 S_norm    T_2              2 B               5 B5           5            5
#> 12 S_norm    T_2              3 B               6 B6           5            5
#> # ℹ 2 more variables: deltadelta_cq <dbl>, fold_change <dbl>

#----- use case 2: mean reference sample_id value 
deltacq_tibble %>%
    calculate_deltadeltacq_bytargetid(ref_sample_ids = "S_norm",
                                 norm_function = mean)
#> # A tibble: 12 × 10
#>    sample_id target_id tech_rep well_row well_col well  delta_cq ref_delta_cq
#>    <chr>     <chr>        <int> <chr>       <int> <chr>    <dbl>        <dbl>
#>  1 S_1       T_1              1 A               1 A1           1         2.67
#>  2 S_1       T_1              2 A               2 A2           1         2.67
#>  3 S_1       T_1              3 A               3 A3           1         2.67
#>  4 S_norm    T_1              1 A               4 A4           3         2.67
#>  5 S_norm    T_1              2 A               5 A5           3         2.67
#>  6 S_norm    T_1              3 A               6 A6           2         2.67
#>  7 S_1       T_2              1 B               1 B1           4         5   
#>  8 S_1       T_2              2 B               2 B2           5         5   
#>  9 S_1       T_2              3 B               3 B3           4         5   
#> 10 S_norm    T_2              1 B               4 B4           5         5   
#> 11 S_norm    T_2              2 B               5 B5           5         5   
#> 12 S_norm    T_2              3 B               6 B6           5         5   
#> # ℹ 2 more variables: deltadelta_cq <dbl>, fold_change <dbl>
```
