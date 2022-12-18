🎄🎄🎄 day 18 🎄🎄🎄
================

``` r
library(tidyverse)
library(here)
```

``` r
test <- tribble(
                ~x, ~y, ~z,
                2,2,2,
                1,2,2,
                3,2,2,
                2,1,2,
                2,3,2,
                2,2,1,
                2,2,3,
                2,2,4,
                2,2,6,
                1,2,5,
                3,2,5,
                2,1,5,
                2,3,5)

input <- read_csv(here("day_18", "input.txt"), col_names = c("x", "y", "z"))
```

### Part 1

``` r
delta  <- tribble(~dx,  ~dy, ~dz,
                   0,    0,   0.5,
                   0,    0,  -0.5,
                   0,    0.5, 0,
                   0,   -0.5, 0,
                   0.5,  0,   0,
                  -0.5,  0,   0)

input |> 
  crossing(delta) |> 
  mutate(x = x + dx, y = y + dy, z = z + dz) |> 
  select(x, y, z) |> 
  group_by(x, y, z) |> 
  mutate(nn = n()) |> 
  ungroup() |>
  count(nn)
```

    ## # A tibble: 2 × 2
    ##      nn     n
    ##   <int> <int>
    ## 1     1  4320
    ## 2     2 12660

### Part 2
