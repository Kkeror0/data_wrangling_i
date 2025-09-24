data manipulation
================

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.2     ✔ tibble    3.3.0
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.1.0     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

\##load in the fas litters

``` r
litters_df=read_csv('./data/FAS_litters.csv')
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df=janitor::clean_names(litters_df)
```

\##select-column

``` r
select(litters_df, group, litter_number)
```

    ## # A tibble: 49 × 2
    ##    group litter_number  
    ##    <chr> <chr>          
    ##  1 Con7  #85            
    ##  2 Con7  #1/2/95/2      
    ##  3 Con7  #5/5/3/83/3-3  
    ##  4 Con7  #5/4/2/95/2    
    ##  5 Con7  #4/2/95/3-3    
    ##  6 Con7  #2/2/95/3-2    
    ##  7 Con7  #1/5/3/83/3-3/2
    ##  8 Con8  #3/83/3-3      
    ##  9 Con8  #2/95/3        
    ## 10 Con8  #3/5/2/2/95    
    ## # ℹ 39 more rows

``` r
select(litters_df, starts_with('gd'))
```

    ## # A tibble: 49 × 3
    ##    gd0_weight gd18_weight gd_of_birth
    ##    <chr>      <chr>             <dbl>
    ##  1 19.7       34.7                 20
    ##  2 27         42                   19
    ##  3 26         41.4                 19
    ##  4 28.5       44.1                 19
    ##  5 <NA>       <NA>                 20
    ##  6 <NA>       <NA>                 20
    ##  7 <NA>       <NA>                 20
    ##  8 <NA>       <NA>                 20
    ##  9 <NA>       <NA>                 20
    ## 10 28.5       <NA>                 20
    ## # ℹ 39 more rows

\##‘filter’-rows

``` r
filter(litters_df, gd0_weight<22)
```

    ## # A tibble: 10 × 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ##  1 Con7  #85           19.7       34.7                 20               3
    ##  2 Mod7  #59           17         33.4                 19               8
    ##  3 Mod7  #103          21.4       42.1                 19               9
    ##  4 Mod7  #8/110/3-2    .          .                    20               9
    ##  5 Mod7  #106          21.7       37.8                 20               5
    ##  6 Mod7  #62           19.5       35.9                 19               7
    ##  7 Mod8  #5/93/2       .          .                    19               8
    ##  8 Low8  #53           21.8       37.2                 20               8
    ##  9 Low8  #100          20         39.2                 20               8
    ## 10 Low8  #4/84         21.8       35.2                 20               4
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_df, group %in% c('Con7','Con8'))
```

    ## # A tibble: 15 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>           <chr>      <chr>             <dbl>           <dbl>
    ##  1 Con7  #85             19.7       34.7                 20               3
    ##  2 Con7  #1/2/95/2       27         42                   19               8
    ##  3 Con7  #5/5/3/83/3-3   26         41.4                 19               6
    ##  4 Con7  #5/4/2/95/2     28.5       44.1                 19               5
    ##  5 Con7  #4/2/95/3-3     <NA>       <NA>                 20               6
    ##  6 Con7  #2/2/95/3-2     <NA>       <NA>                 20               6
    ##  7 Con7  #1/5/3/83/3-3/2 <NA>       <NA>                 20               9
    ##  8 Con8  #3/83/3-3       <NA>       <NA>                 20               9
    ##  9 Con8  #2/95/3         <NA>       <NA>                 20               8
    ## 10 Con8  #3/5/2/2/95     28.5       <NA>                 20               8
    ## 11 Con8  #5/4/3/83/3     28         <NA>                 19               9
    ## 12 Con8  #1/6/2/2/95-2   <NA>       <NA>                 20               7
    ## 13 Con8  #3/5/3/83/3-3-2 <NA>       <NA>                 20               8
    ## 14 Con8  #2/2/95/2       <NA>       <NA>                 19               5
    ## 15 Con8  #3/6/2/2/95-3   <NA>       <NA>                 20               7
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

\#mutate

\##arrange

\##%\>%

%\>%
