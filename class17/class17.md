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

    ##          Province.State Country.Region     Lat     Long       date cases
    ## 3028           Shanghai Mainland China 31.2020 121.4491 2020-03-06     3
    ## 3029            Sichuan Mainland China 30.6171 102.7103 2020-03-06    17
    ## 3030 Suffolk County, MA             US 42.3601 -71.0589 2020-03-06     1
    ## 3031           Xinjiang Mainland China 41.1129  85.2401 2020-03-06     1
    ## 3032             Yunnan Mainland China 24.9740 101.4870 2020-03-06     1
    ## 3033           Zhejiang Mainland China 29.1832 120.0934 2020-03-06    23
    ##           type
    ## 3028 recovered
    ## 3029 recovered
    ## 3030 recovered
    ## 3031 recovered
    ## 3032 recovered
    ## 3033 recovered

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

    ## # A tibble: 99 x 2
    ##    Country.Region `sum(cases)`
    ##    <fct>                 <int>
    ##  1 Afghanistan               1
    ##  2 Algeria                  17
    ##  3 Andorra                   1
    ##  4 Argentina                 2
    ##  5 Armenia                   1
    ##  6 Australia                83
    ##  7 Austria                  55
    ##  8 Azerbaijan                6
    ##  9 Bahrain                  64
    ## 10 Belarus                   6
    ## # … with 89 more rows

> Q1. How many total infected cases are there around the world?

``` r
total_cases <- sum(virus$cases)
total_cases
```

    ## [1] 161126

> Q2. How many deaths linked to infected cases have there been? Lets
> have a look at the *$type* column

``` r
table(virus$type)
```

    ## 
    ## confirmed     death recovered 
    ##      1695       222      1116

``` r
inds <- virus$type == "death"
death_cases<- sum(virus[inds,"cases"])
```

> Q3. What is the overall death rate?

Percent death

``` r
round(death_cases/total_cases * 100, 2)
```

    ## [1] 2.15

> Q4. What is the death rate in “Mainland China”?

``` r
china.cases <- virus$Country.Region == "Mainland China"

china.death_cases <- sum(virus[china.cases,"cases"])
```

``` r
round(china.death_cases/total_cases * 100, 2)
```

    ## [1] 85.34

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
