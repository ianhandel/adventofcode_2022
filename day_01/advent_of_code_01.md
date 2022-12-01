🎄🎄🎄 day 01 🎄🎄🎄
================

``` r
library(tidyverse)
library(here)
```

## Data

``` r
test <- tibble( calories = c(1000L, 2000L, 3000L, NA, 4000L, NA, 5000L, 6000L, NA, 7000L, 8000L, 9000L, NA, 10000L))

input <- read_csv(here("day_01", "input.txt"),
                  col_names = "calories",
                  skip_empty_rows = FALSE)
```

I think we’ll go with the tidyverse for this one…

## Part 1

``` r
input |> 
  mutate(elf = cumsum(is.na(calories))) |> 
  drop_na(calories) |> 
  group_by(elf) |> 
  summarise(total = sum(calories)) |> 
  filter(total == max(total))
```

    ## # A tibble: 1 × 2
    ##     elf total
    ##   <int> <dbl>
    ## 1    79 69836

## Part 2

``` r
input |> 
  mutate(elf = cumsum(is.na(calories))) |> 
  drop_na(calories) |> 
  group_by(elf) |> 
  summarise(total = sum(calories)) |> 
  arrange(desc(total)) |> 
  top_n(n = 3) |> 
  summarise(sum(total))
```

    ## # A tibble: 1 × 1
    ##   `sum(total)`
    ##          <dbl>
    ## 1       207968
