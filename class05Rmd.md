Class05: R Graphics
================

# Class 5

# Data visualization and graphics in R

``` r
plot(1:5, col="blue", typ="o")
```

![](class05Rmd_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

# Section 2A.

# Read the data file “weight\_chart.txt”

``` r
baby <- read.table("bimm143_05_rstats/weight_chart.txt", header=TRUE)

plot(baby$Age, baby$Weight, typ="o", col="blue", pch=15, cex=1.5, lwd=2, ylim=c(2,10), 
     xlab="Age(months)", ylab="Weight(kg)", main="Baby weight with age")
```

![](class05Rmd_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
plot(1:5, pch=1:5, cex=1:5, col=1:5)
```

![](class05Rmd_files/figure-gfm/unnamed-chunk-2-2.png)<!-- -->

# Section 2B.

## Read a new file of mouse genome features

``` r
mouse <- read.table("bimm143_05_rstats/feature_counts.txt", header=TRUE, sep="\t")

dotchart(mouse$Count, labels=mouse$Feature)
```

![](class05Rmd_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
barplot(mouse$Count, names.arg=mouse$Feature, horiz = TRUE, ylab="", main="Number of Features in the mouse GRCm38 genome", las=1, xlim=c(0,80000))
```

![](class05Rmd_files/figure-gfm/unnamed-chunk-3-2.png)<!-- -->

``` r
old.par <- par()$mar
par(mar=c(3.1, 11.1, 4.1, 2))
```

# Section 3A.

``` r
mf <- read.delim("bimm143_05_rstats/male_female_counts.txt")

barplot(mf$Count, names.arg=mf$Sample, col=rainbow( nrow(mf) ) )
```

![](class05Rmd_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->
