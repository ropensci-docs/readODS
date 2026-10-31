# An Overview of readODS

``` r

library(readODS)
```

You probably only need to use two functions from this package:
`read_ods` and `write_ods`.

Write the data PlantGrowth (from the built-in `datasets` package) as a
new file `plant.ods` in the current working directory of the user’s
session.

``` r

write_ods(PlantGrowth, "plant.ods")
```

You can then read it back from `plant.ods`

``` r

read_ods("plant.ods")
#> # A tibble: 30 × 2
#>    weight group
#>     <dbl> <chr>
#>  1   4.17 ctrl 
#>  2   5.58 ctrl 
#>  3   5.18 ctrl 
#>  4   6.11 ctrl 
#>  5   4.5  ctrl 
#>  6   4.61 ctrl 
#>  7   5.17 ctrl 
#>  8   4.53 ctrl 
#>  9   5.33 ctrl 
#> 10   5.14 ctrl 
#> # ℹ 20 more rows
```

## Update and Append

You can append another sheet into an existing ods file with the sheet
name being “mtcars_ods”.

``` r

write_ods(mtcars, "plant.ods", sheet = "mtcars_ods", append = TRUE)
```

Read from a specific sheet. Notice row names are missing.

``` r

read_ods("plant.ods", sheet = "mtcars_ods")
#> # A tibble: 32 × 11
#>      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
#>    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
#>  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
#>  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
#>  3  22.8     4  108     93  3.85  2.32  18.6     1     1     4     1
#>  4  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
#>  5  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
#>  6  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
#>  7  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
#>  8  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
#>  9  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
#> 10  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
#> # ℹ 22 more rows
```

You can also integer for `sheet`, e.g. 2 for the second sheet.

``` r

read_ods("plant.ods", sheet = 2)
#> # A tibble: 32 × 11
#>      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
#>    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
#>  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
#>  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
#>  3  22.8     4  108     93  3.85  2.32  18.6     1     1     4     1
#>  4  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
#>  5  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
#>  6  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
#>  7  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
#>  8  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
#>  9  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
#> 10  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
#> # ℹ 22 more rows
```

Update an existing sheet and preserve row names

``` r

write_ods(mtcars, "plant.ods", sheet = "mtcars_ods", update = TRUE, row_names = TRUE)
```

Notice the information from the sheet `mtcars_ods` is updated.

``` r

read_ods("plant.ods", sheet = "mtcars_ods")
#> New names:
#> • `` -> `...1`
#> # A tibble: 32 × 12
#>    ...1          mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
#>    <chr>       <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
#>  1 Mazda RX4    21       6  160    110  3.9   2.62  16.5     0     1     4     4
#>  2 Mazda RX4 …  21       6  160    110  3.9   2.88  17.0     0     1     4     4
#>  3 Datsun 710   22.8     4  108     93  3.85  2.32  18.6     1     1     4     1
#>  4 Hornet 4 D…  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
#>  5 Hornet Spo…  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
#>  6 Valiant      18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
#>  7 Duster 360   14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
#>  8 Merc 240D    24.4     4  147.    62  3.69  3.19  20       1     0     4     2
#>  9 Merc 230     22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
#> 10 Merc 280     19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
#> # ℹ 22 more rows
```

Read from a specific range

``` r

read_ods("plant.ods", sheet = "mtcars_ods", range = "A1:C10")
#> New names:
#> • `` -> `...1`
#> # A tibble: 9 × 3
#>   ...1                mpg   cyl
#>   <chr>             <dbl> <dbl>
#> 1 Mazda RX4          21       6
#> 2 Mazda RX4 Wag      21       6
#> 3 Datsun 710         22.8     4
#> 4 Hornet 4 Drive     21.4     6
#> 5 Hornet Sportabout  18.7     8
#> 6 Valiant            18.1     6
#> 7 Duster 360         14.3     8
#> 8 Merc 240D          24.4     4
#> 9 Merc 230           22.8     4
```

You cannot append to an existing sheet.

``` r

write_ods(iris, "plant.ods", sheet = "mtcars_ods", append = TRUE)
#> Error:
#> ! Sheet mtcars_ods exists. Set update to TRUE is you want to update this sheet.
```

You cannot update a missing sheet.

``` r

write_ods(iris, "plant.ods", sheet = "iris", update = TRUE)
#> Error:
#> ! Sheet iris does not exist. Cannot update.
```

## Writing multiple sheets simultaneously

It is much faster to write data frames into the same file by putting
them in a (named) list.

``` r

write_ods(list("iris" = iris, "plant" = PlantGrowth), "plant_multi.ods")
read_ods("plant_multi.ods", sheet = "plant")
#> # A tibble: 30 × 2
#>    weight group
#>     <dbl> <chr>
#>  1   4.17 ctrl 
#>  2   5.58 ctrl 
#>  3   5.18 ctrl 
#>  4   6.11 ctrl 
#>  5   4.5  ctrl 
#>  6   4.61 ctrl 
#>  7   5.17 ctrl 
#>  8   4.53 ctrl 
#>  9   5.33 ctrl 
#> 10   5.14 ctrl 
#> # ℹ 20 more rows
```

## Flat ODS files (`.xml` or `.fods`)

Can be read with
[`read_ods()`](https://docs.ropensci.org/readODS/reference/read_ods.md)
[^1] (note that the same function is used to read flat files, no matter
the extension). This has the same behaviour and arguments as
[`read_ods()`](https://docs.ropensci.org/readODS/reference/read_ods.md)

``` r

read_fods("plant.fods")
```

[`write_ods()`](https://docs.ropensci.org/readODS/reference/write_ods.md)
can be used to write Flat ODS files

``` r

write_ods(PlantGrowth, "plant.fods")
```

## Misc.

Use the function
[`list_ods_sheets()`](https://docs.ropensci.org/readODS/reference/list_ods_sheets.md)
to list out all sheets in an (F)ODS file.

``` r

list_ods_sheets("plant.ods")
#> [1] "Sheet1"     "mtcars_ods"
```

## readODS 2.0.0

Starting from 2.0.0, `write_ods` writes `NA` as empty by default.

``` r

PlantGrowth2 <- tibble::as_tibble(PlantGrowth)
PlantGrowth2[1,1] <- NA
PlantGrowth2$group <- as.character(PlantGrowth2$group)

## NA is preseved; weight is still <dbl>
read_ods(write_ods(PlantGrowth2))
#> # A tibble: 30 × 2
#>    weight group
#>     <dbl> <chr>
#>  1  NA    ctrl 
#>  2   5.58 ctrl 
#>  3   5.18 ctrl 
#>  4   6.11 ctrl 
#>  5   4.5  ctrl 
#>  6   4.61 ctrl 
#>  7   5.17 ctrl 
#>  8   4.53 ctrl 
#>  9   5.33 ctrl 
#> 10   5.14 ctrl 
#> # ℹ 20 more rows
```

If you want `NA` to be written literally as the string “NA”, use
`na_as_string`. You should literally see the string “NA” when the file
is opened with LibreOffice, for example.

But the string “NA” messes up the automatic type inference of
`read_ods`.

``` r

## NA is preseved; but weight is now <chr>
read_ods(write_ods(PlantGrowth2, na_as_string = TRUE))
#> # A tibble: 30 × 2
#>    weight group
#>    <chr>  <chr>
#>  1 NA     ctrl 
#>  2 5.58   ctrl 
#>  3 5.18   ctrl 
#>  4 6.11   ctrl 
#>  5 4.5    ctrl 
#>  6 4.61   ctrl 
#>  7 5.17   ctrl 
#>  8 4.53   ctrl 
#>  9 5.33   ctrl 
#> 10 5.14   ctrl 
#> # ℹ 20 more rows
```

Of course you can fix this by specifying `col_types`.

``` r

## NA is preseved; but weight is now <chr>
read_ods(write_ods(PlantGrowth2, na_as_string = TRUE),
         col_types = readr::cols(weight = readr::col_double()))
#> Warning: [0, 1]: expected a double, but got 'NA'
#> # A tibble: 30 × 2
#>    weight group
#>     <dbl> <chr>
#>  1  NA    ctrl 
#>  2   5.58 ctrl 
#>  3   5.18 ctrl 
#>  4   6.11 ctrl 
#>  5   4.5  ctrl 
#>  6   4.61 ctrl 
#>  7   5.17 ctrl 
#>  8   4.53 ctrl 
#>  9   5.33 ctrl 
#> 10   5.14 ctrl 
#> # ℹ 20 more rows
```

Several functions were removed in readODS 2.0.0. Please consider the API
of `readODS` mature and there should not be any breaking change until
readODS 3.0.0.

### `ods_sheets`

Please use `list_ods_sheets(path = "plant.ods")` instead.

``` r

## ods_sheets("plant.ods")
list_ods_sheets("plant.ods")
#> [1] "Sheet1"     "mtcars_ods"
```

### `get_num_sheets_in_ods` and `getNrOfSheetsInODS`

Please use `list_ods_sheets`

``` r

##get_num_sheets_in_ods("plant.ods")
length(list_ods_sheets("plant.ods"))
#> [1] 2
```

### `read.ods`

Please use `read_ods`. In order to emulate the behaviours of `read.ods`,
the followings are recommended

``` r

## read.ods from 1.6 to 1.8
read_ods("plant.ods", col_names = FALSE, skip = 0, na = NULL, col_types = NA, as_tibble = FALSE)
#> New names:
#> • `` -> `...1`
#> • `` -> `...2`
#>      ...1  ...2
#> 1  weight group
#> 2    4.17  ctrl
#> 3    5.58  ctrl
#> 4    5.18  ctrl
#> 5    6.11  ctrl
#> 6     4.5  ctrl
#> 7    4.61  ctrl
#> 8    5.17  ctrl
#> 9    4.53  ctrl
#> 10   5.33  ctrl
#> 11   5.14  ctrl
#> 12   4.81  trt1
#> 13   4.17  trt1
#> 14   4.41  trt1
#> 15   3.59  trt1
#> 16   5.87  trt1
#> 17   3.83  trt1
#> 18   6.03  trt1
#> 19   4.89  trt1
#> 20   4.32  trt1
#> 21   4.69  trt1
#> 22   6.31  trt2
#> 23   5.12  trt2
#> 24   5.54  trt2
#> 25    5.5  trt2
#> 26   5.37  trt2
#> 27   5.29  trt2
#> 28   4.92  trt2
#> 29   6.15  trt2
#> 30    5.8  trt2
#> 31   5.26  trt2
```

``` r

## read.ods older than 1.6
lapply(list_ods_sheets("plant.ods"),
       function(x) read_ods(path = "plant.ods", sheet = x, col_names = FALSE, skip = 0, na = NULL, col_types = NA, as_tibble = FALSE))
#> New names:
#> New names:
#> • `` -> `...1`
#> • `` -> `...2`
#> [[1]]
#>      ...1  ...2
#> 1  weight group
#> 2    4.17  ctrl
#> 3    5.58  ctrl
#> 4    5.18  ctrl
#> 5    6.11  ctrl
#> 6     4.5  ctrl
#> 7    4.61  ctrl
#> 8    5.17  ctrl
#> 9    4.53  ctrl
#> 10   5.33  ctrl
#> 11   5.14  ctrl
#> 12   4.81  trt1
#> 13   4.17  trt1
#> 14   4.41  trt1
#> 15   3.59  trt1
#> 16   5.87  trt1
#> 17   3.83  trt1
#> 18   6.03  trt1
#> 19   4.89  trt1
#> 20   4.32  trt1
#> 21   4.69  trt1
#> 22   6.31  trt2
#> 23   5.12  trt2
#> 24   5.54  trt2
#> 25    5.5  trt2
#> 26   5.37  trt2
#> 27   5.29  trt2
#> 28   4.92  trt2
#> 29   6.15  trt2
#> 30    5.8  trt2
#> 31   5.26  trt2
#> 
#> [[2]]
#>                   ...1 ...2 ...3  ...4 ...5 ...6  ...7  ...8 ...9 ...10 ...11
#> 1                       mpg  cyl  disp   hp drat    wt  qsec   vs    am  gear
#> 2            Mazda RX4   21    6   160  110  3.9  2.62 16.46    0     1     4
#> 3        Mazda RX4 Wag   21    6   160  110  3.9 2.875 17.02    0     1     4
#> 4           Datsun 710 22.8    4   108   93 3.85  2.32 18.61    1     1     4
#> 5       Hornet 4 Drive 21.4    6   258  110 3.08 3.215 19.44    1     0     3
#> 6    Hornet Sportabout 18.7    8   360  175 3.15  3.44 17.02    0     0     3
#> 7              Valiant 18.1    6   225  105 2.76  3.46 20.22    1     0     3
#> 8           Duster 360 14.3    8   360  245 3.21  3.57 15.84    0     0     3
#> 9            Merc 240D 24.4    4 146.7   62 3.69  3.19    20    1     0     4
#> 10            Merc 230 22.8    4 140.8   95 3.92  3.15  22.9    1     0     4
#> 11            Merc 280 19.2    6 167.6  123 3.92  3.44  18.3    1     0     4
#> 12           Merc 280C 17.8    6 167.6  123 3.92  3.44  18.9    1     0     4
#> 13          Merc 450SE 16.4    8 275.8  180 3.07  4.07  17.4    0     0     3
#> 14          Merc 450SL 17.3    8 275.8  180 3.07  3.73  17.6    0     0     3
#> 15         Merc 450SLC 15.2    8 275.8  180 3.07  3.78    18    0     0     3
#> 16  Cadillac Fleetwood 10.4    8   472  205 2.93  5.25 17.98    0     0     3
#> 17 Lincoln Continental 10.4    8   460  215    3 5.424 17.82    0     0     3
#> 18   Chrysler Imperial 14.7    8   440  230 3.23 5.345 17.42    0     0     3
#> 19            Fiat 128 32.4    4  78.7   66 4.08   2.2 19.47    1     1     4
#> 20         Honda Civic 30.4    4  75.7   52 4.93 1.615 18.52    1     1     4
#> 21      Toyota Corolla 33.9    4  71.1   65 4.22 1.835  19.9    1     1     4
#> 22       Toyota Corona 21.5    4 120.1   97  3.7 2.465 20.01    1     0     3
#> 23    Dodge Challenger 15.5    8   318  150 2.76  3.52 16.87    0     0     3
#> 24         AMC Javelin 15.2    8   304  150 3.15 3.435  17.3    0     0     3
#> 25          Camaro Z28 13.3    8   350  245 3.73  3.84 15.41    0     0     3
#> 26    Pontiac Firebird 19.2    8   400  175 3.08 3.845 17.05    0     0     3
#> 27           Fiat X1-9 27.3    4    79   66 4.08 1.935  18.9    1     1     4
#> 28       Porsche 914-2   26    4 120.3   91 4.43  2.14  16.7    0     1     5
#> 29        Lotus Europa 30.4    4  95.1  113 3.77 1.513  16.9    1     1     5
#> 30      Ford Pantera L 15.8    8   351  264 4.22  3.17  14.5    0     1     5
#> 31        Ferrari Dino 19.7    6   145  175 3.62  2.77  15.5    0     1     5
#> 32       Maserati Bora   15    8   301  335 3.54  3.57  14.6    0     1     5
#> 33          Volvo 142E 21.4    4   121  109 4.11  2.78  18.6    1     1     4
#>    ...12
#> 1   carb
#> 2      4
#> 3      4
#> 4      1
#> 5      1
#> 6      2
#> 7      1
#> 8      4
#> 9      2
#> 10     2
#> 11     4
#> 12     4
#> 13     3
#> 14     3
#> 15     3
#> 16     4
#> 17     4
#> 18     4
#> 19     1
#> 20     2
#> 21     1
#> 22     1
#> 23     2
#> 24     2
#> 25     4
#> 26     2
#> 27     1
#> 28     2
#> 29     2
#> 30     4
#> 31     6
#> 32     8
#> 33     2
```

------------------------------------------------------------------------

[^1]: [`read_fods()`](https://docs.ropensci.org/readODS/reference/read_ods.md)
    and
    [`list_fods_sheets()`](https://docs.ropensci.org/readODS/reference/list_ods_sheets.md)
    are also available. But since version 2.2.0
    [`read_ods()`](https://docs.ropensci.org/readODS/reference/read_ods.md)
    and
    [`list_ods_sheets()`](https://docs.ropensci.org/readODS/reference/list_ods_sheets.md)
    can determine whether the file at the `path` argument is flat or
    not.
