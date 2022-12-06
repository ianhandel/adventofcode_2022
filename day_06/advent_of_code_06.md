🎄🎄🎄 day 06 🎄🎄🎄
================

``` r
library(tidyverse)
library(here)
```

### Part 1

``` r
test <- "zcfzfwzzqfrljwzlrfnpqdbhtmscgvjw" |> 
  str_split("", simplify = TRUE)

input <- read_file(here("day_06", "input.txt")) |>
  str_split("") %>%
  `[[`(1)
```

``` r
unq <- function(x, index, n){
  if (index < n) return(FALSE)
  length(unique(x[(index - n + 1):index])) == n
}

map_lgl(1:(length(input) - 4), ~unq(input, .x, 4)) |> 
  which() |> 
  first()
```

    ## [1] 1987

### Part 2

``` r
map_lgl(1:(length(input) - 14), ~unq(input, .x, 14)) |> 
  which() |> 
  first()
```

    ## [1] 3059
