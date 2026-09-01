# Determine whether to show progress bar

By default, readODS displays a progress bar unless one of the following
is TRUE:

- The progress is explicitly disabled by setting
  options(readODS.show_progress = FALSE).

- The code is run in a non-interactive session (interactive() is FALSE).

- The code is run by knitr / rmarkdown.

## Usage

``` r
readODS_progress()
```

## Value

logical indicating whether to show progress
