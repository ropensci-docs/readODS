# Write Data to (F)ODS File

Function to write a single data frame or a list of data frames to a
(f)ods file.

## Usage

``` r
write_ods(
  x,
  path = tempfile(fileext = ".ods"),
  sheet = "Sheet1",
  append = FALSE,
  update = FALSE,
  row_names = FALSE,
  col_names = TRUE,
  na_as_string = FALSE,
  padding = FALSE
)

write_fods(
  x,
  path = tempfile(fileext = ".fods"),
  sheet = "Sheet1",
  append = FALSE,
  update = FALSE,
  row_names = FALSE,
  col_names = TRUE,
  na_as_string = FALSE,
  padding = FALSE
)
```

## Arguments

- x:

  data frame or list of data frames that will be sheets in the (f)ods.
  If the list is named, the names are used as sheet names

- path:

  Path to the (f)ods file to write

- sheet:

  Name of the sheet; ignore if `x` is a list of data frames

- append:

  logical, TRUE indicates that x should be appended to the existing file
  (path) as a new sheet. If a sheet with the same sheet_name exists, an
  exception is thrown. See update. Please also note that writing is
  slightly slower if TRUE. Default is FALSE. Ignore if `x` is a list of
  data frames

- update:

  logical, TRUE indicates that the sheet with sheet_name in the existing
  file (path) should be updated with the content of x. If a sheet with
  sheet_name does not exist, an exception is thrown. Please also note
  that writing is slightly slower if TRUE. Default is FALSE. Ignore if
  `x` is a list of data frames

- row_names:

  logical, TRUE indicates that row names of x are to be included in the
  sheet. Default is FALSE

- col_names:

  logical, TRUE indicates that column names of x are to be included in
  the sheet. Default is TRUE

- na_as_string:

  logical, TRUE indicates that NAs are written as string; FALSE
  indicates that NAs are written as empty cells

- padding:

  logical, TRUE indicates that the sheet is padded with repeated empty
  cells to the maximum size, either 2^20 x 1024 (if the number of
  columns of `x` is less than or equal 1024) or 2^20 x 16,384
  (otherwise). This is the default behaviour of Microsoft Excel. Default
  is FALSE

## Value

A (F)ODS file written to the file path location specified by the user.
The value of `path` is also returned invisibly

## Details

This function emulates `writexl::write_xlsx()` except in the handling of
list columns. The expected behaviour for this is undefined and the two
functions behave differently. This function handles list columns by
converting them to character vectors of R code (similar to the output of
[`dput()`](https://rdrr.io/r/base/dput.html)), which is probably not
ideal.

## Author

Detlef Steuer <steuer@hsu-hh.de>, Thomas J. Leeper
<thosjleeper@gmail.com>, John Foster <john.x.foster@nab.com.au>,
Chung-hong Chan <chainsawtiney@gmail.com>

## Examples

``` r
if (FALSE) { # \dontrun{
# preserve the row names
write_ods(mtcars, "mtcars.ods", row_names = TRUE)
# append a sheet to an existing file
write_ods(PlantGrowth, "mtcars.ods", append = TRUE, sheet = "plant")
# This is however faster
write_ods(list("Sheet1" = mtcars, "plant" = PlantGrowth), "mtcars.ods", row_names = TRUE)
# write flat ODS file
write_fods(mtcars, "mtcars.fods", sheet = "mtcars")
} # }
```
