# Calibrate primer sets / probes by calculating detection efficiency and R squared

Note efficiency is given in ratio, not per cent; multiply by 100 for
that.

## Usage

``` r
calculate_efficiency(cq_df_1, formula = cq ~ log2(dilution) + biol_rep)
```

## Arguments

- cq_df_1:

  data frame with cq (quantification cycle) data, 1 row per well.

  Must have columns cq, dilution.

  Assumes data are only for 1 probe/primer set/target_id, i.e. all
  values in cq_df_1 are fit with the same slope.

- formula:

  formula to use for log-log regression fit.

  Default value assumes multiple biological replicates, cq ~
  log2(dilution) + biol_rep.

  If only a single Biological Replicate, change to cq ~ log2(dilution).

## Value

data frame with 1 single row, and columns: efficiency, efficiency.sd,
r.squared.

## See also

calculate_efficiency_bytargetid

## Examples

``` r
# create simple dilution dataset
dilution_tibble <- tibble(dilution = rep(c(1, 0.1, 0.001, 0.0001), 2),
                     cq = c(1, 3, 4, 6,
                            4, 5, 6, 7),
                     biol_rep = rep(c(1,2), each = 4),
                     target_id = "T1")
                     
# calculate primer efficiency

#----- use case 1: include difference across replicates in model
dilution_tibble %>%
    calculate_efficiency()
#> # A tibble: 1 × 3
#>   efficiency efficiency.sd r.squared
#>        <dbl>         <dbl>     <dbl>
#> 1      0.271        0.0404     0.931

#----- use case 2: ignore difference across replicates
dilution_tibble %>%
    calculate_efficiency(formula = cq ~ log2(dilution))
#> # A tibble: 1 × 3
#>   efficiency efficiency.sd r.squared
#>        <dbl>         <dbl>     <dbl>
#> 1      0.271        0.0860     0.623
```
