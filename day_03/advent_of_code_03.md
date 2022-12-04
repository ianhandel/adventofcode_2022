🎄🎄🎄 day 03 🎄🎄🎄
================

# Rucksac Reorganisation

``` r
library(tidyverse)
library(here)
library(adventdrob)
```

``` r
test <- tibble(pack = c(
  "vJrwpWtwJgWrhcsFMMfFFhFp",
  "jqHRNqRjqzjGDLGLrsFMfFZSrLrFZsSL",
  "PmmdzqPrVvPwwTWBwg",
  "wMqvLMZHhHMvwLHjbvcjnnSBnvTQFn",
  "ttgJtRGJQctTZtZT",
  "CrZsJsPPZsGzwwsLwLmpwMDw"
))

input <- tibble(pack = read_lines(here("day_03", "input.txt")))
```

### Part 1

``` r
input |>
  mutate(elf = row_number()) |>
  mutate(one = map_chr(pack, ~ str_sub(.x, start = 1, end = nchar(.x) / 2))) |>
  mutate(two = map_chr(pack, ~ str_sub(.x, start = nchar(.x) / 2 + 1, end = nchar(.x)))) |>
  select(-pack) |>
  pivot_longer(one:two, names_to = "compartment", values_to = "contents") |>
  separate_rows(contents, sep = "") |>
  filter(contents != "") |>
  group_by(elf) |>
  summarise(common = intersect(contents[compartment == "one"], contents[compartment == "two"])) |>
  mutate(priority = match(common, c(letters, LETTERS))) |>
  summarise(sum(priority))
```

    ## # A tibble: 1 × 1
    ##   `sum(priority)`
    ##             <int>
    ## 1            7878

### Part 2

``` r
input |>
  mutate(group = rep(1:(n() / 3), each = 3)) |>
  mutate(elfingroup = rep(1:3, times = n() / 3)) |>
  separate_rows(pack, sep = "") |>
  filter(pack != "") |>
  group_by(group) |>
  summarise(common = intersect(
    intersect(
      pack[elfingroup == 1],
      pack[elfingroup == 2]
    ),
    pack[elfingroup == 3]
  )) |>
  mutate(priority = match(common, c(letters, LETTERS))) |>
  summarise(sum(priority))
```

    ## # A tibble: 1 × 1
    ##   `sum(priority)`
    ##             <int>
    ## 1            2760
