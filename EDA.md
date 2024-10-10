DS_NOTES_EDA
================

``` r
library(tidyverse)
library(dplyr)
library(ggridges)
library(patchwork)
```

### Exploratory Data Analysis

- Exploratory Data Analysis is a loosely-defined process. Roughly, the
  stuff between loading data and formal analysis is exploratory.
- Grouping
  - Datasets often consists of groups(by design/implied/nested)
- Quantitative comparisons across groups are informative
  - Measures of Centrality, Variablity, Missingness
- `group_by()` + `summarize()`
  - `group_by` makes grouping explicit and adds a layer to your data
  - `summarize()` allows you to compute one-number summaries
    - most useful in conjunction with `group_by()`

#### `group_by()`
