# Package index

## All functions

- [`calculate_deltacq_bysampleid()`](https://docs.ropensci.org/tidyqpcr/reference/calculate_deltacq_bysampleid.md)
  : Calculate delta cq (\\\Delta Cq\\) to normalize quantification cycle
  (log2-fold) data within sample_id.
- [`calculate_deltadeltacq_bytargetid()`](https://docs.ropensci.org/tidyqpcr/reference/calculate_deltadeltacq_bytargetid.md)
  : Calculate delta delta cq (\\\Delta \Delta Cq\\) to globally
  normalize quantification cycle (log2-fold) data across sample_id.
- [`calculate_drdt_plate()`](https://docs.ropensci.org/tidyqpcr/reference/calculate_drdt_plate.md)
  : Calculate dR/dT of melt curves for of every well in a plate.
- [`calculate_dydx()`](https://docs.ropensci.org/tidyqpcr/reference/calculate_dydx.md)
  : Calculate dy/dx vector from vectors y and x
- [`calculate_efficiency()`](https://docs.ropensci.org/tidyqpcr/reference/calculate_efficiency.md)
  : Calibrate primer sets / probes by calculating detection efficiency
  and R squared
- [`calculate_efficiency_bytargetid()`](https://docs.ropensci.org/tidyqpcr/reference/calculate_efficiency_bytargetid.md)
  : Calibrate multiple probes by calculating detection efficiency and R
  squared
- [`calculate_normvalue()`](https://docs.ropensci.org/tidyqpcr/reference/calculate_normvalue.md)
  : Calculate a normalized value for a subset of reference ids
- [`create_blank_plate()`](https://docs.ropensci.org/tidyqpcr/reference/create_blank_plate.md)
  [`create_blank_plate_96well()`](https://docs.ropensci.org/tidyqpcr/reference/create_blank_plate.md)
  [`create_blank_plate_1536well()`](https://docs.ropensci.org/tidyqpcr/reference/create_blank_plate.md)
  : Create a blank plate template as a tibble (with helper functions for
  common plate sizes)
- [`create_colkey_4diln_2ctrl_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_4diln_2ctrl_in_24.md)
  : Create a 4-dilution column key for primer calibration
- [`create_colkey_6_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_6_in_24.md)
  : Create a 6-value, 24-column key for plates
- [`create_colkey_6diln_2ctrl_in_24()`](https://docs.ropensci.org/tidyqpcr/reference/create_colkey_6diln_2ctrl_in_24.md)
  : Create a 6-dilution column key for primer calibration
- [`create_rowkey_4_in_16()`](https://docs.ropensci.org/tidyqpcr/reference/create_rowkey_4_in_16.md)
  : Create a 4-value, 16-row key for plates
- [`create_rowkey_8_in_16_plain()`](https://docs.ropensci.org/tidyqpcr/reference/create_rowkey_8_in_16_plain.md)
  : Create a plain 8-value, 16-row key for plates
- [`debaseline()`](https://docs.ropensci.org/tidyqpcr/reference/debaseline.md)
  : Remove baseline from amplification curves (BETA)
- [`display_plate()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate.md)
  : Display an empty plate plan which can be populated with ggplot2 geom
  elements.
- [`display_plate_qpcr()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate_qpcr.md)
  : Display qPCR plate plan with sample_id, target_id, prep_type per
  well
- [`display_plate_value()`](https://docs.ropensci.org/tidyqpcr/reference/display_plate_value.md)
  : Display the value of each well across the plate.
- [`label_plate_rowcol()`](https://docs.ropensci.org/tidyqpcr/reference/label_plate_rowcol.md)
  : Label a plate with sample and probe information
- [`make_row_names_echo1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_echo1536.md)
  : Generates row names for the Labcyte Echo 1536-well plates
- [`make_row_names_lc1536()`](https://docs.ropensci.org/tidyqpcr/reference/make_row_names_lc1536.md)
  : Generates row names for the Roche Lightcycler (tm) 1536-well plates
- [`read_lightcycler_1colour_cq()`](https://docs.ropensci.org/tidyqpcr/reference/read_lightcycler_1colour_cq.md)
  : Reads quantification cycle (cq) data in 1 colour from Roche
  Lightcyclers
- [`read_lightcycler_1colour_raw()`](https://docs.ropensci.org/tidyqpcr/reference/read_lightcycler_1colour_raw.md)
  : Reads raw text-format fluorescence data in 1 colour from Roche
  Lightcyclers
