Class17 Corona Virus
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

    ##       Province.State Country.Region     Lat     Long       date cases      type
    ## 33043       Zhejiang          China 29.1832 120.0934 2020-03-07     7 recovered
    ## 33044       Zhejiang          China 29.1832 120.0934 2020-03-08     7 recovered
    ## 33045       Zhejiang          China 29.1832 120.0934 2020-03-09    15 recovered
    ## 33046       Zhejiang          China 29.1832 120.0934 2020-03-10    15 recovered
    ## 33047       Zhejiang          China 29.1832 120.0934 2020-03-11     4 recovered
    ## 33048       Zhejiang          China 29.1832 120.0934 2020-03-12     2 recovered

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

    ## # A tibble: 116 x 2
    ##    Country.Region `sum(cases)`
    ##    <fct>                 <int>
    ##  1 Afghanistan               7
    ##  2 Albania                  24
    ##  3 Algeria                  33
    ##  4 Andorra                   2
    ##  5 Argentina                20
    ##  6 Armenia                   4
    ##  7 Australia               152
    ##  8 Austria                 307
    ##  9 Azerbaijan               14
    ## 10 Bahrain                 230
    ## # … with 106 more rows

> Q1. How many total infected cases are there around the world?

``` r
total_cases <- sum(virus$cases)
total_cases
```

    ## [1] 201387

> Q2. How many deaths linked to infected cases have there been? Lets
> have a look at the *$type* column

``` r
table(virus$type)
```

    ## 
    ## confirmed     death recovered 
    ##     11016     11016     11016

``` r
inds <- virus$type == "death"
death_cases<- sum(virus[inds,"cases"])
```

> Q3. What is the overall death rate?

Percent death

``` r
round(death_cases/total_cases * 100, 2)
```

    ## [1] 2.34

> Q4. What is the death rate in “Mainland China”?

``` r
china.cases <- virus$Country.Region == "Mainland China"

china.death_cases <- sum(virus[china.cases,"cases"])
```

``` r
round(china.death_cases/total_cases * 100, 2)
```

    ## [1] 0

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
