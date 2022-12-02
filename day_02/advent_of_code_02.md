🎄🎄🎄 day 02 🎄🎄🎄
================

# Rock paper scissors

This is all mightly clunky but hey ho…

``` r
library(tidyverse)
library(here)
```

``` r
test <- tibble::tribble(
  ~"them", ~"you",
  "A", "Y",
  "B", "X",
  "C", "Z"
)
```

``` r
test <- test |>
  mutate(you = as.character(fct_recode(you,
    "A" = "X",
    "B" = "Y",
    "C" = "Z"
  )))

input <- read_delim(here("day_02", "input.txt"), col_names = c("them", "you")) |>
  mutate(you = as.character(fct_recode(you,
    "A" = "X",
    "B" = "Y",
    "C" = "Z"
  )))

score <- function(you, them) {
  win <- you == "A" & them == "C" |
    you == "B" & them == "A" |
    you == "C" & them == "B"
  draw <- you == them

  6 * win + 3 * draw + (you == "A") * 1 + (you == "B") * 2 + (you == "C") * 3
}

input |>
  mutate(score = map2_dbl(you, them, score)) |>
  summarise(sum(score))
```

    ## # A tibble: 1 × 1
    ##   `sum(score)`
    ##          <dbl>
    ## 1         9177

``` r
needed <- function(them, need) {
  if (need == "B") you <- them

  if (need == "A" & them == "A") you <- "C"
  if (need == "A" & them == "B") you <- "A"
  if (need == "A" & them == "C") you <- "B"

  if (need == "C" & them == "A") you <- "B"
  if (need == "C" & them == "B") you <- "C"
  if (need == "C" & them == "C") you <- "A"

  you
}

input |>
  rename(need = you) |>
  mutate(you = map2_chr(them, need, needed)) |>
  mutate(score = map2_dbl(you, them, score)) |>
  summarise(sum(score))
```

    ## # A tibble: 1 × 1
    ##   `sum(score)`
    ##          <dbl>
    ## 1        12111
