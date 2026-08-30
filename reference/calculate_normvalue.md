# Calculate a normalized value for a subset of reference ids

This is used to calculate the normalized \`cq\` values for reference
\`target_ids\` (e.g. genes), to use in \`delta_cq\` calculation for each
\`sample_id\`.

## Usage

``` r
calculate_normvalue(
  value_df,
  ref_ids,
  value_name = "value",
  id_name = "id",
  norm_function = median
)
```

## Arguments

- value_df:

  data frame containing relevant columns, those named in \`value_name\`
  and \`id_name\` parameters.

- ref_ids:

  values of reference ids, that are used to calculate normalized
  reference value.

- value_name:

  name of column containing values. This column should be numeric.

- id_name:

  name of column containing ids.

- norm_function:

  Function to use to calculate the value to normalize by. Default
  function is median, alternatively could use mean, geometric mean, etc.

## Details

Also used to calculate the normalized \`delta_cq\` values for reference
\`sample_ids\`, to use in \`deltadelta_cq\` calculation for each
\`target_id\`.

## Examples

``` r
# create simple cq dataset with one sample, two targets  and 3 reps
cq_tibble <- tibble(sample_id = "S_1",
                     target_id = rep(c("T_1",
                                       "T_norm"), each = 3),
                     tech_rep = rep(1:3, 2),
                     well_row = rep(c("A",
                                      "B"), each = 3),
                     well_col = 1,
                     well = paste0(well_row, well_col),
                     cq = c(10, 10, 10,
                            12, 12, 11))
                     
# normalise cq to reference target_id called 'T_norm'

#----- use case 1: median reference target_id value
cq_tibble %>%
    calculate_normvalue(ref_ids = "T_norm",
                        value_name = "cq",
                        id_name = "target_id")
#> # A tibble: 6 × 8
#>   sample_id target_id tech_rep well_row well_col well     cq value_to_norm_by
#>   <chr>     <chr>        <int> <chr>       <dbl> <chr> <dbl>            <dbl>
#> 1 S_1       T_1              1 A               1 A1       10               12
#> 2 S_1       T_1              2 A               1 A1       10               12
#> 3 S_1       T_1              3 A               1 A1       10               12
#> 4 S_1       T_norm           1 B               1 B1       12               12
#> 5 S_1       T_norm           2 B               1 B1       12               12
#> 6 S_1       T_norm           3 B               1 B1       11               12

#----- use case 2: mean reference target_id value 
cq_tibble %>%
    calculate_normvalue(ref_ids = "T_norm",
                        value_name = "cq",
                        id_name = "target_id",
                        norm_function = mean)
#> # A tibble: 6 × 8
#>   sample_id target_id tech_rep well_row well_col well     cq value_to_norm_by
#>   <chr>     <chr>        <int> <chr>       <dbl> <chr> <dbl>            <dbl>
#> 1 S_1       T_1              1 A               1 A1       10             11.7
#> 2 S_1       T_1              2 A               1 A1       10             11.7
#> 3 S_1       T_1              3 A               1 A1       10             11.7
#> 4 S_1       T_norm           1 B               1 B1       12             11.7
#> 5 S_1       T_norm           2 B               1 B1       12             11.7
#> 6 S_1       T_norm           3 B               1 B1       11             11.7
```
