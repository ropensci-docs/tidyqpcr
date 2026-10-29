# Reads raw text-format fluorescence data in 1 colour from Roche Lightcyclers

This is the data from "export in text format" from the Lightcycler
software. The other data format, .ixo, can be converted to .txt format
by the Lightcycler software.

## Usage

``` r
read_lightcycler_1colour_raw(
  filename,
  skip = 2,
  col_names = c("well", "sample_info", "program_no", "segment_no", "cycle", "time",
    "temperature", "fluor_raw"),
  col_types = "ccffinnn",
  ...
)
```

## Arguments

- filename:

  file name

- skip:

  number of lines to skip, defaults to 2

- col_names:

  names to give to columns

- col_types:

  data types of columns

- ...:

  other arguments to pass to read_tsv, if needed

## Value

tibble containing raw data, with default column names:

well: the well of the plate, e.g. A1

sample_info: this is the "Sample" field entered in lightcycler software,
defaults to "Sample X"

program_no: the number of the cycler program, for 2-step PCR defaults to
1 = melt, 2 = amplify, 3 = melt.

segment_no: the number of the segment of the cycler program, e.g.
hold/raise/lower temperature

cycle: the cycle number, for programs with repeated cycles (i.e.
amplification)

time: the time of fluorescence reading acquisition (in what units???)

temperature: the temperature of the block at fluorescence acquisition

fluor_raw: the raw fluorescence reading in "arbitrary units". For SYBR
safe, this would be 483nm excitation, 533nm emission.

## Details

This function is a thin wrapper around readr::read_tsv.

## See also

read_lightcycler_1colour_cq

## Examples

``` r
read_lightcycler_1colour_raw(system.file("extdata/Edward_qPCR_Nrd1_calibration_2019-02-02.txt.gz", 
                                                 package = "tidyqpcr"))
#> # A tibble: 82,944 × 8
#>    well  sample_info program_no segment_no cycle   time temperature fluor_raw
#>    <chr> <chr>       <fct>      <fct>      <int>  <dbl>       <dbl>     <dbl>
#>  1 A1    Sample 1    2          2              1 234700        59.9      0.59
#>  2 A1    Sample 1    2          2              2 274117        59.8      0.57
#>  3 A1    Sample 1    2          2              3 313634        59.8      0.56
#>  4 A1    Sample 1    2          2              4 353100        59.8      0.56
#>  5 A1    Sample 1    2          2              5 392600        59.8      0.56
#>  6 A1    Sample 1    2          2              6 432234        59.8      0.56
#>  7 A1    Sample 1    2          2              7 471801        59.8      0.55
#>  8 A1    Sample 1    2          2              8 511334        59.8      0.55
#>  9 A1    Sample 1    2          2              9 550834        59.8      0.55
#> 10 A1    Sample 1    2          2             10 590417        59.8      0.54
#> # ℹ 82,934 more rows
```
