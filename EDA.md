DS_NOTES_EDA
================

``` r
library(tidyverse)
library(dplyr)
library(ggridges)
library(patchwork)
```

``` r
  weather_df = read.csv("C:/Users/Twilight/Desktop/Columbia/Fall Semester 2024/Data Science I/Datasets/weather_data.csv")
  weather_df <- weather_df %>% mutate(month = format(as.Date(date), "%m")) # creates a new column month extracted from date column
```

### Exploratory Data Analysis

- Exploratory Data Analysis is a loosely-defined process. Roughly, the
  stuff between loading data and formal analysis is exploratory.
- Grouping
  - Datasets often consists of groups(by design/implied/nested)
- Quantitative comparisons across groups are informative
  - Measures of Centrality, Variablity, Missingnes
- `group_by()` + `summarize()`
  - `group_by` makes grouping explicit and adds a layer to your data
  - `summarize()` allows you to compute one-number summaries
    - most useful in conjunction with `group_by()`

#### `group_by()`

``` r
  weather_df %>%
    group_by(name, month)
```

    ## # A tibble: 1,095 × 8
    ## # Groups:   name, month [36]
    ##        X name           id          date        prcp  tmax  tmin month
    ##    <int> <chr>          <chr>       <chr>      <int> <dbl> <dbl> <chr>
    ##  1     1 CentralPark_NY USW00094728 2017-01-01     0   8.9   4.4 01   
    ##  2     2 CentralPark_NY USW00094728 2017-01-02    53   5     2.8 01   
    ##  3     3 CentralPark_NY USW00094728 2017-01-03   147   6.1   3.9 01   
    ##  4     4 CentralPark_NY USW00094728 2017-01-04     0  11.1   1.1 01   
    ##  5     5 CentralPark_NY USW00094728 2017-01-05     0   1.1  -2.7 01   
    ##  6     6 CentralPark_NY USW00094728 2017-01-06    13   0.6  -3.8 01   
    ##  7     7 CentralPark_NY USW00094728 2017-01-07    81  -3.2  -6.6 01   
    ##  8     8 CentralPark_NY USW00094728 2017-01-08     0  -3.8  -8.8 01   
    ##  9     9 CentralPark_NY USW00094728 2017-01-09     0  -4.9  -9.9 01   
    ## 10    10 CentralPark_NY USW00094728 2017-01-10     0   7.8  -6   01   
    ## # ℹ 1,085 more rows

### counting things

``` r
  weather_df %>%
    group_by(month) %>%
    summarize(n_obs=n())
```

    ## # A tibble: 12 × 2
    ##    month n_obs
    ##    <chr> <int>
    ##  1 01       93
    ##  2 02       84
    ##  3 03       93
    ##  4 04       90
    ##  5 05       93
    ##  6 06       90
    ##  7 07       93
    ##  8 08       93
    ##  9 09       90
    ## 10 10       93
    ## 11 11       90
    ## 12 12       93

``` r
  weather_df %>%
    group_by(name, month) %>%
    summarize(count=n())
```

    ## `summarise()` has grouped output by 'name'. You can override using the
    ## `.groups` argument.

    ## # A tibble: 36 × 3
    ## # Groups:   name [3]
    ##    name           month count
    ##    <chr>          <chr> <int>
    ##  1 CentralPark_NY 01       31
    ##  2 CentralPark_NY 02       28
    ##  3 CentralPark_NY 03       31
    ##  4 CentralPark_NY 04       30
    ##  5 CentralPark_NY 05       31
    ##  6 CentralPark_NY 06       30
    ##  7 CentralPark_NY 07       31
    ##  8 CentralPark_NY 08       31
    ##  9 CentralPark_NY 09       30
    ## 10 CentralPark_NY 10       31
    ## # ℹ 26 more rows

``` r
  # Using "count"
  weather_df %>%
    count(name, month, name="n_obs")
```

    ##              name month n_obs
    ## 1  CentralPark_NY    01    31
    ## 2  CentralPark_NY    02    28
    ## 3  CentralPark_NY    03    31
    ## 4  CentralPark_NY    04    30
    ## 5  CentralPark_NY    05    31
    ## 6  CentralPark_NY    06    30
    ## 7  CentralPark_NY    07    31
    ## 8  CentralPark_NY    08    31
    ## 9  CentralPark_NY    09    30
    ## 10 CentralPark_NY    10    31
    ## 11 CentralPark_NY    11    30
    ## 12 CentralPark_NY    12    31
    ## 13     Molokai_HI    01    31
    ## 14     Molokai_HI    02    28
    ## 15     Molokai_HI    03    31
    ## 16     Molokai_HI    04    30
    ## 17     Molokai_HI    05    31
    ## 18     Molokai_HI    06    30
    ## 19     Molokai_HI    07    31
    ## 20     Molokai_HI    08    31
    ## 21     Molokai_HI    09    30
    ## 22     Molokai_HI    10    31
    ## 23     Molokai_HI    11    30
    ## 24     Molokai_HI    12    31
    ## 25   Waterhole_WA    01    31
    ## 26   Waterhole_WA    02    28
    ## 27   Waterhole_WA    03    31
    ## 28   Waterhole_WA    04    30
    ## 29   Waterhole_WA    05    31
    ## 30   Waterhole_WA    06    30
    ## 31   Waterhole_WA    07    31
    ## 32   Waterhole_WA    08    31
    ## 33   Waterhole_WA    09    30
    ## 34   Waterhole_WA    10    31
    ## 35   Waterhole_WA    11    30
    ## 36   Waterhole_WA    12    31
