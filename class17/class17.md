Untitled
================

## Coronavirus

Here we analyze infection data for the 2019 novel Coronavirus COVID-19
(2019-nCoV) epidemic. The raw data is pulled from the Johns Hopkins
University Center for Systems Science and Engineering (JHU CCSE)
Coronavirus repository.

A CSV file is available here
<https://github.com/RamiKrispin/coronavirus-csv>

``` r
url <- "https://tinyurl.com/COVID-2019"
virus <- read.csv(url)

tail(virus)
```

    ##      Province.State Country.Region     Lat     Long       date cases      type
    ## 3147       Shandong Mainland China 36.3427 118.1498 2020-03-07     9 recovered
    ## 3148       Shanghai Mainland China 31.2020 121.4491 2020-03-07     7 recovered
    ## 3149        Sichuan Mainland China 30.6171 102.7103 2020-03-07    12 recovered
    ## 3150    Toronto, ON         Canada 43.6532 -79.3832 2020-03-07     1 recovered
    ## 3151       Xinjiang Mainland China 41.1129  85.2401 2020-03-07     1 recovered
    ## 3152       Zhejiang Mainland China 29.1832 120.0934 2020-03-07     7 recovered

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
virus %>% group_by(Country.Region) %>%
  summarize(sum(cases)) %>%
  arrange()
```

    ## # A tibble: 102 x 2
    ##    Country.Region `sum(cases)`
    ##    <fct>                 <int>
    ##  1 Afghanistan               1
    ##  2 Algeria                  17
    ##  3 Andorra                   1
    ##  4 Argentina                 8
    ##  5 Armenia                   1
    ##  6 Australia                86
    ##  7 Austria                  79
    ##  8 Azerbaijan                9
    ##  9 Bahrain                  89
    ## 10 Belarus                   6
    ## # … with 92 more rows

> Q1. How many total infected cases are there around the world?

``` r
total_cases <- sum(virus$cases)
total_cases
```

    ## [1] 167753

> Q2. How many deaths linked to infected cases have there been? Lets
> have a look at the *$type* column

``` r
table(virus$type)
```

    ## 
    ## confirmed     death recovered 
    ##      1777       230      1145

``` r
inds <- virus$type == "death"
death_cases<- sum(virus[inds,"cases"])
```

> Q3. What is the overall death rate?

Percent death

``` r
round(death_cases/total_cases * 100, 2)
```

    ## [1] 2.12

> Q4. What is the death rate in “Mainland China”?

``` r
china.cases <- virus$Country.Region == "Mainland China"

china.death_cases <- sum(virus[china.cases,"cases"])
```

``` r
round(china.death_cases/total_cases * 100, 2)
```

    ## [1] 82.98

> Q5. What is the death rate in Italy, Iran and the US?

``` r
Italy.cases <- virus$Country.Region == "Italy"
Italy.death_cases <- sum(virus[Italy.cases, "Italy"])
```

``` r
round(Italy.death_cases/total_cases * 100, 2)
```

    ## [1] 0

``` r
Iran.cases <- virus$Country.Region == "Iran"
Iran.death_cases <- sum(virus[Iran.cases, "Iran"])
```

``` r
round(Iran.death_cases/total_cases * 100, 2)
```

    ## [1] 0

``` r
US.cases <- virus$Country.Region == "US"
US.death_cases <- sum(virus[US.cases, "US"])
```

``` r
round(US.death_cases/total_cases * 100, 2)
```

    ## [1] 0
