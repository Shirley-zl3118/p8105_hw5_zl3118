HW5
================
Shirley Liang
2022-11-13

### Problem 1

### Problem 2

``` r
homicides = read_csv("homicide-data.csv")
```

    ## Rows: 52179 Columns: 12
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (9): uid, victim_last, victim_first, victim_race, victim_age, victim_sex...
    ## dbl (3): reported_date, lat, lon
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

In the `homicides` dataset, there are 52179 observations and 12
variables, including uid, reported_date, victim_last, victim_first,
victim_race, victim_age, victim_sex, city, state, lat, lon, disposition.

``` r
homicides <- homicides %>% 
  janitor::clean_names() %>% 
  mutate(city_state = str_c(city, state, sep = ","),
  disposition_status = case_when(disposition == "Closed without arrest" ~ "unsolved",
                     disposition == "Open/No arrest" ~ "unsolved",
                     disposition == "Closed by arrest" ~ "resolved")) 

summary <- homicides %>% group_by(city_state) %>% 
  summarize(total_number_of_homicides = n(), number_of_unsolved_homicides = sum(disposition_status == "unsolved")) 

summary
```

    ## # A tibble: 51 × 3
    ##    city_state     total_number_of_homicides number_of_unsolved_homicides
    ##    <chr>                              <int>                        <int>
    ##  1 Albuquerque,NM                       378                          146
    ##  2 Atlanta,GA                           973                          373
    ##  3 Baltimore,MD                        2827                         1825
    ##  4 Baton Rouge,LA                       424                          196
    ##  5 Birmingham,AL                        800                          347
    ##  6 Boston,MA                            614                          310
    ##  7 Buffalo,NY                           521                          319
    ##  8 Charlotte,NC                         687                          206
    ##  9 Chicago,IL                          5535                         4073
    ## 10 Cincinnati,OH                        694                          309
    ## # … with 41 more rows

### Problem 3
