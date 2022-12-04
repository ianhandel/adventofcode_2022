🎄🎄🎄 day 04 🎄🎄🎄
================

``` r
library(tidyverse)
library(here)
library(adventdrob)
```

# Camp cleanup

``` r
test <- c("2-4,6-8",
          "2-3,4-5",
          "5-7,7-9",
          "2-8,3-7",
          "6-6,4-6",
          "2-6,4-8") |> 
  as_tibble()

input <- advent_input(4)
```

### Part 1

``` r
input |> 
  separate(x, c("first", "second"), sep = ",") |>
  mutate(pair = 1:n()) |> 
  pivot_longer(first:second, names_to = "elf", values_to = "value") |> 
  separate(value, c("from", "to"), "-", convert = TRUE) |> 
  group_by(pair) |> 
  summarise(contained = abs(sign(diff(from)) + sign(diff(to))) < 2) |> 
  summarise(sum(contained))
```

    ## # A tibble: 1 × 1
    ##   `sum(contained)`
    ##              <int>
    ## 1              550

Part 2

``` r
input |> 
  separate(x, c("first", "second"), sep = ",") |>
  mutate(pair = 1:n()) |> 
  pivot_longer(first:second, names_to = "elf", values_to = "value") |> 
  separate(value, c("from", "to"), "-", convert = TRUE) |> 
  group_by(pair) |> 
  summarise(overlap = to[[1]] >= from[[2]] & to[[2]] >= from[[1]] |
           to[[2]] >= from[[1]] & to[[1]] >= from[[2]]) |> 
  summarise(sum(overlap))
```

    ## # A tibble: 1 × 1
    ##   `sum(overlap)`
    ##            <int>
    ## 1            931
