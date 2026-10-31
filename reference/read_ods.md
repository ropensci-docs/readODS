# Read Data From (F)ODS File

read_ods is a function to read a single sheet from an (f)ods file and
return a data frame. The function can be used for reading both ods and
flat ods files. (`read_fods`) is also available, which can only read
flat ods files.

## Usage

``` r
read_ods(
  path,
  sheet = 1,
  col_names = TRUE,
  col_types = NULL,
  na = "",
  skip = 0,
  formula_as_formula = FALSE,
  range = NULL,
  row_names = FALSE,
  strings_as_factors = FALSE,
  verbose = FALSE,
  as_tibble = TRUE,
  .name_repair = "unique",
  ods_format = c("auto", "ods", "fods"),
  guess = FALSE,
  trim_ws = TRUE,
  n_max = Inf,
  guess_max = min(1000, n_max),
  progress = readODS_progress()
)

read_fods(
  path,
  sheet = 1,
  col_names = TRUE,
  col_types = NULL,
  na = "",
  skip = 0,
  formula_as_formula = FALSE,
  range = NULL,
  row_names = FALSE,
  strings_as_factors = FALSE,
  verbose = FALSE,
  as_tibble = TRUE,
  .name_repair = "unique",
  trim_ws = TRUE,
  n_max = Inf,
  guess_max = min(1000, n_max),
  progress = readODS_progress()
)
```

## Arguments

- path:

  path to the (f)ods file.

- sheet:

  sheet to read. Either a string (the sheet name), or an integer sheet
  number. The default is 1.

- col_names:

  logical, indicating whether the file contains the names of the
  variables as its first line. Default is TRUE.

- col_types:

  Either NULL to guess from the spreadsheet or refer to
  [`readr::type_convert()`](https://readr.tidyverse.org/reference/type_convert.html)
  to specify cols specification. It can also be a shorthand such as
  "ccf" ("character", "character", "factor"), a list, or an object
  created by
  [`readr::cols()`](https://readr.tidyverse.org/reference/cols.html). NA
  will return a data frame with all columns being "characters". Please
  note that it will not speed up the reading by a lot by specifying this
  parameter explicitly. It is more for accuracy.

- na:

  Character vector of strings to use for missing values. By default
  read_ods converts blank cells to missing data. It can also be set to
  NULL, so that empty cells are treated as NA.

- skip:

  the number of lines of the data file to skip before beginning to read
  data. If this parameter is larger than the total number of lines in
  the ods file, an empty data frame is returned.

- formula_as_formula:

  logical, a switch to display formulas as formulas "SUM(A1:A3)" or as
  the resulting value "3"... or "8".. . Default is FALSE.

- range:

  selection of rectangle using Excel-like cell range, such as
  `range = "D12:F15"` or `range = "R1C12:R6C15"`. Cell range processing
  is handled by the
  [`cellranger::as.cell_limits()`](https://rdrr.io/pkg/cellranger/man/cell_limits.html).
  If sheet name is in the range, such as `range = "Sheet2!A2:B7"`, this
  sheet name is used instead of the provided `sheet`. If `sheet` is not
  the default value (1), a warning is given.

- row_names:

  logical, indicating whether the file contains the names of the rows as
  its first column. Default is FALSE.

- strings_as_factors:

  logical, if character columns to be converted to factors. Default is
  FALSE.

- verbose:

  logical, if messages should be displayed. Default is FALSE.

- as_tibble:

  logical, if the output should be a tibble (as opposed to a
  data.frame). Default is TRUE.

- .name_repair:

  A string or function passed on as `.name_repair` to
  [`tibble::as_tibble()`](https://tibble.tidyverse.org/reference/as_tibble.html)

  - `"minimal"`: No name repair

  - `"unique"` : Make sure names are unique and not empty

  - `"check_unique"`: Check names are unique, but do not repair

  - `"universal"` : Checks names are unique and valid R variables names
    in scope

  - A function to apply custom name repair.

  Default is `"unique"`.

- ods_format:

  character, must be "auto", "ods" or "fods". The default "auto" is to
  determine the format automatically. By default, the format is
  determined by file extension, unless `guess` is `FALSE`.

- guess:

  logical, If the file extension is absent or not recognized, this
  controls whether we attempt to guess format based on the file
  signature or "magic number".

- trim_ws:

  logical, should leading and trailing whitespace be trimmed?

- n_max:

  numeric, Maximum number of data rows to read. Ignored if `range` is
  given.

- guess_max:

  numeric, Maximum number of data rows to use for guessing column types.
  Defaults to min(1000, n_max).

- progress:

  logical, Display a progress bar? By default, shows a progress bar in
  interactive sessions unless disabled. See
  [`readODS_progress`](https://docs.ropensci.org/readODS/reference/readODS_progress.md)
  for more details.

## Value

A tibble (`tibble`) or data frame (`data.frame`) containing a
representation of data in the (f)ods file.

## Author

Peter Brohan <peter.brohan+cran@gmail.com>, Chung-hong Chan
<chainsawtiney@gmail.com>, Gerrit-Jan Schutten <phonixor@gmail.com>

## Examples

``` r
if (FALSE) { # \dontrun{
# Read an ODS file
read_ods("starwars.ods")
# Read a specific sheet, e.g. the 2nd sheet
read_ods("starwars.ods", sheet = 2)
# Read a specific range, e.g. A1:C11
read_ods("starwars.ods", sheet = 2, range = "A1:C11")
# Read an FODS file
read_ods("starwars.fods")
# Read a specific sheet, e.g. the 2nd sheet
read_ods("starwars.fods", sheet = 2)
# Read a specific range, e.g. A1:C11
read_ods("starwars.fods", sheet = 2, range = "A1:C11")
# Give a warning and read from Sheet1 (not 2)
read_ods("starwars.fods", sheet = 2, range = "Sheet1!A1:C11")
# Specifying col_types as shorthand, the third column as factor; other by guessing
read_ods("starwars.ods", col_types = "??f")
# Specifying col_types as list
read_ods("starwars.ods", col_types = list(species = "f"))
# Using read_fods, although you don't have to
read_ods("starwars.fods")
} # }
```
