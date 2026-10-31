# Get information in an (F)ODS File

`list_ods_sheets` lists all sheets in an (f)ods file. The function can
be used for listing sheets in both ods and flat ods files.
(`list_fods_sheets`) is also available, which can only list sheets in
flat ods files.

## Usage

``` r
list_ods_sheets(
  path,
  include_external_data = FALSE,
  ods_format = c("auto", "ods", "fods"),
  guess = FALSE
)

list_fods_sheets(path, include_external_data = FALSE)

ods_sheets(path)
```

## Arguments

- path:

  Path to the (f)ods file

- include_external_data:

  A boolean value to show or hide sheets containing archived linked data
  (default false)

- ods_format:

  character, must be "auto", "ods" or "fods". The default "auto" is to
  determine the format automatically. By default, the format is
  determined by file extension, unless `guess` is `FALSE`.

- guess:

  logical, If the file extension is absent or not recognized, this
  controls whether we attempt to guess format based on the file
  signature or "magic number".

## Value

A character vector of sheet names

## Details

The default "include_external_data" for `ods_sheets` is TRUE to maintain
compatibility with version 1 of readODS. It will change to `TRUE` in
version 3.

## See also

use
[`read_ods`](https://docs.ropensci.org/readODS/reference/read_ods.md) to
read the data

## Author

Peter Brohan <peter.brohan+cran@gmail.com>, Chung-hong Chan
<chainsawtiney@gmail.com>, Gerrit-Jan Schutten <phonixor@gmail.com>

## Examples

``` r
if (FALSE) { # \dontrun{
# Get the list of names of sheets
list_ods_sheets("starwars.ods")
list_ods_sheets("starwars.fods")
# Using list_fods_sheets, although you don't have to
list_fods_sheets("starwars.fods")
} # }
```
