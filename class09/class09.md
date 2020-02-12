Class 9: Machine Learning pt1.
================
Chae Kook
2/5/2020

## K-means clustering

Let’s try the `kmeans()` function in R to cluster some made-up example
data.

``` r
tmp <- c(rnorm(30,-3), rnorm(30,3)) 
x <- cbind(x=tmp, y=rev(tmp))


plot(x)
```

![](class09_files/figure-gfm/unnamed-chunk-1-1.png)<!-- --> Use the
kmeans() function setting k to 2 and nstart=20

``` r
km <- kmeans(x, centers = 2, nstart = 20)
```

Inspect/print the results

``` r
km 
```

    ## K-means clustering with 2 clusters of sizes 30, 30
    ## 
    ## Cluster means:
    ##           x         y
    ## 1 -2.939129  3.059490
    ## 2  3.059490 -2.939129
    ## 
    ## Clustering vector:
    ##  [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2
    ## [39] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
    ## 
    ## Within cluster sum of squares by cluster:
    ## [1] 65.53055 65.53055
    ##  (between_SS / total_SS =  89.2 %)
    ## 
    ## Available components:
    ## 
    ## [1] "cluster"      "centers"      "totss"        "withinss"     "tot.withinss"
    ## [6] "betweenss"    "size"         "iter"         "ifault"

What is in the output object `km`I can use the `attributes()` function
to find this info

``` r
attributes(km)
```

    ## $names
    ## [1] "cluster"      "centers"      "totss"        "withinss"     "tot.withinss"
    ## [6] "betweenss"    "size"         "iter"         "ifault"      
    ## 
    ## $class
    ## [1] "kmeans"

Q. How many points are in each cluster?

``` r
km$size
```

    ## [1] 30 30

Q. What ‘component’ of your result object details - cluster size? -
cluster assignment/membership? - cluster
    center?

``` r
km$cluster
```

    ##  [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2
    ## [39] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2

let’s check how many 2s and 1s are in this vector with the `table()`
function.

``` r
table(km$cluster)
```

    ## 
    ##  1  2 
    ## 30 30

Plot x colored by the kmeans cluster assignment and add cluster centers
as blue points

``` r
plot(x, col=km$cluster+1)
points(km$centers, col="blue", pch=15, cex=3)
```

![](class09_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

## Hierarchical clustering in R

The `hclust()` function is the main Hierarchical clustering method in R
and it must be passed a distance matrix as input not your raw data\!

``` r
hc <- hclust( dist(x)) 
hc
```

    ## 
    ## Call:
    ## hclust(d = dist(x))
    ## 
    ## Cluster method   : complete 
    ## Distance         : euclidean 
    ## Number of objects: 60

``` r
plot(hc)
abline(h=6, col="red", lty=2)
```

![](class09_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
table(cutree(hc, h=3.5))
```

    ## 
    ##  1  2  3  4  5  6 
    ## 16 10  4 16 10  4

You can also ask `cutree()` for the `k` number of groups that you
    want.

``` r
cutree(hc, k=5)
```

    ##  [1] 1 2 1 1 1 2 1 1 1 2 1 2 1 1 1 2 2 1 1 2 2 2 1 1 1 1 1 1 2 1 3 4 3 3 3 3 5 3
    ## [39] 4 4 4 3 5 4 4 3 3 5 4 5 4 3 3 3 4 3 3 3 4 3

### Some more messy data to cluster

``` r
# Step 1. Generate some example data for clustering x <- rbind(
matrix(rnorm(100, mean=0, sd=0.3), ncol = 2) 
```

    ##              [,1]        [,2]
    ##  [1,] -0.02775715 -0.23696221
    ##  [2,] -0.57422891 -0.22861441
    ##  [3,] -0.42399051 -0.21353164
    ##  [4,] -0.09101767 -0.32059918
    ##  [5,]  0.02146266 -0.14674155
    ##  [6,] -0.15977803  0.10435362
    ##  [7,] -0.27579102 -0.02487040
    ##  [8,] -0.14254310  0.13315211
    ##  [9,] -0.06998891 -0.57964966
    ## [10,] -0.19030487  0.26727149
    ## [11,]  0.77913347  0.31680197
    ## [12,] -0.11329903 -0.50010193
    ## [13,] -0.39623306  0.42457428
    ## [14,]  0.06026653 -0.13287384
    ## [15,]  0.15885059 -0.25080784
    ## [16,] -0.03477833 -0.25569467
    ## [17,]  0.13473549  0.12767830
    ## [18,]  0.33211732  0.31179461
    ## [19,] -0.12264195 -0.09847429
    ## [20,] -0.26900767 -0.26835771
    ## [21,] -0.23507133  0.28202394
    ## [22,]  0.13632396  0.02775545
    ## [23,]  0.17336341 -0.49476997
    ## [24,]  0.12109758  0.11741279
    ## [25,] -0.06848261  0.15294415
    ## [26,] -0.18012967 -0.30279931
    ## [27,] -0.27493538  0.25783576
    ## [28,]  0.38176817  0.42317136
    ## [29,] -0.02978064  0.31757910
    ## [30,] -0.34832580 -0.36576432
    ## [31,]  0.06446065  0.08906361
    ## [32,]  0.03523788 -0.69302227
    ## [33,]  0.21330682  0.09821592
    ## [34,] -0.61821147  0.23574663
    ## [35,]  0.48246586 -0.11248931
    ## [36,]  0.34506107 -0.41293041
    ## [37,] -0.36396717  0.18213199
    ## [38,]  0.01611774  0.03128387
    ## [39,]  0.30717845 -0.01822323
    ## [40,]  0.10666143  0.42171030
    ## [41,] -0.18776253 -0.03285607
    ## [42,] -0.30826351 -0.47282986
    ## [43,]  0.20527543 -0.27453122
    ## [44,] -0.11371357  0.10902098
    ## [45,]  0.12330185 -0.31550463
    ## [46,] -0.08180270 -0.28664197
    ## [47,]  0.35495223 -0.07687250
    ## [48,] -0.18599652  0.07605067
    ## [49,]  0.21969205  0.08483616
    ## [50,] -0.13157512 -0.07882112

``` r
matrix(rnorm(100, mean=1, sd=0.3), ncol = 2)
```

    ##            [,1]      [,2]
    ##  [1,] 1.0915410 0.9335760
    ##  [2,] 0.9226210 0.6363475
    ##  [3,] 0.8228454 1.4165913
    ##  [4,] 0.9724753 0.8013258
    ##  [5,] 0.2444294 1.4223090
    ##  [6,] 0.8695445 1.4770139
    ##  [7,] 0.6914379 1.4807277
    ##  [8,] 1.0569795 1.1485659
    ##  [9,] 1.3318963 0.6293962
    ## [10,] 0.7956119 1.1836417
    ## [11,] 0.9915400 0.8085057
    ## [12,] 1.2132366 1.3632821
    ## [13,] 1.0807092 1.1643070
    ## [14,] 0.8966870 0.9426413
    ## [15,] 0.6118650 1.4858598
    ## [16,] 1.0263584 1.0981055
    ## [17,] 1.2686189 0.5131177
    ## [18,] 0.6094432 0.7545855
    ## [19,] 1.1637618 1.3359750
    ## [20,] 0.6416405 0.6953474
    ## [21,] 0.5826931 0.6935017
    ## [22,] 0.8481816 1.1628984
    ## [23,] 0.6248454 1.2173697
    ## [24,] 0.7286479 1.1577441
    ## [25,] 1.0345861 1.0708088
    ## [26,] 0.9398092 1.9547169
    ## [27,] 1.1149289 1.2602754
    ## [28,] 1.1712076 0.8278038
    ## [29,] 0.8159349 0.4318635
    ## [30,] 1.3489096 0.5891355
    ## [31,] 1.1266205 0.9756055
    ## [32,] 0.7687121 0.9546305
    ## [33,] 0.8564022 0.2555261
    ## [34,] 1.0056521 1.0854538
    ## [35,] 1.1053202 1.1526476
    ## [36,] 1.1121741 0.8921480
    ## [37,] 1.6606344 0.9756454
    ## [38,] 0.8438261 1.4166331
    ## [39,] 0.9737325 0.7344169
    ## [40,] 1.3140451 0.8803738
    ## [41,] 1.4411169 0.5593098
    ## [42,] 0.9814031 0.7394828
    ## [43,] 0.9571316 0.8873122
    ## [44,] 1.1671378 1.3706679
    ## [45,] 0.9659649 0.8153628
    ## [46,] 0.8983481 1.1639941
    ## [47,] 0.5635391 0.9660119
    ## [48,] 1.1679422 1.2885660
    ## [49,] 0.6325335 0.5518322
    ## [50,] 0.9880246 0.9356474

``` r
matrix(c(rnorm(50, mean=1, sd=0.3), rnorm(50, mean=0, sd=0.3)), ncol = 2)
```

    ##            [,1]         [,2]
    ##  [1,] 1.1336609 -0.106355924
    ##  [2,] 0.6507498 -0.055088291
    ##  [3,] 0.9087410 -0.006580164
    ##  [4,] 0.7128114  0.289780483
    ##  [5,] 1.0920805 -0.086401162
    ##  [6,] 0.8357102 -0.050990699
    ##  [7,] 1.0617061  0.214712199
    ##  [8,] 1.3048440 -0.180901613
    ##  [9,] 1.3679380 -0.069077559
    ## [10,] 0.8061527 -0.557382442
    ## [11,] 0.8991247  0.194327000
    ## [12,] 0.8846960  0.228233901
    ## [13,] 1.1911785 -0.272715337
    ## [14,] 1.0974746  0.167662687
    ## [15,] 1.0993035 -0.176668364
    ## [16,] 1.0434016  0.176071031
    ## [17,] 0.7937777 -0.157605690
    ## [18,] 1.2123416  0.127394670
    ## [19,] 1.0082470  0.046188468
    ## [20,] 0.9029360  0.026086896
    ## [21,] 0.8510381 -0.306529356
    ## [22,] 0.8850638  0.289919991
    ## [23,] 0.8745208 -0.242424977
    ## [24,] 0.7374343 -0.068996151
    ## [25,] 0.5271769  0.188592097
    ## [26,] 1.6523430  0.616930497
    ## [27,] 1.3106666  0.005339398
    ## [28,] 0.8634521  0.043544189
    ## [29,] 1.1297210 -0.579753840
    ## [30,] 1.1899995  0.636799658
    ## [31,] 1.6585340 -0.333961538
    ## [32,] 0.8663684  0.049363757
    ## [33,] 0.8941262 -0.032739498
    ## [34,] 1.1621613 -0.256051350
    ## [35,] 0.6330496 -0.142555973
    ## [36,] 1.0555895 -0.033633389
    ## [37,] 0.9470544  0.088260053
    ## [38,] 1.1147249 -0.675802724
    ## [39,] 0.9170188 -0.288204835
    ## [40,] 1.4728418  0.255758865
    ## [41,] 1.2379723 -0.386135488
    ## [42,] 1.4195068 -0.170406036
    ## [43,] 0.6748712  0.034111593
    ## [44,] 1.1537935  0.267580264
    ## [45,] 1.2743516  0.193157825
    ## [46,] 0.9781866 -0.090951950
    ## [47,] 1.2392987  0.251904422
    ## [48,] 0.8566102  0.911466556
    ## [49,] 0.9562449 -0.196429805
    ## [50,] 0.7559072 -0.593865725

``` r
colnames(x) <- c("x", "y")
# Step 2. Plot the data without clustering
plot(x)
```

![](class09_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
# c3
 # Step 3. Generate colors for known clusters
# (just so we can compare to hclust results) 
col <- as.factor( rep(c("c1","c2","c3"), each=50) )
plot(x, col=col)
```

![](class09_files/figure-gfm/unnamed-chunk-13-2.png)<!-- -->

Q. Use the dist(), hclust(), plot() and cutree() functions to return 2
and 3 clusters

``` r
hc <- hclust( dist(x) )
plot(hc)
```

![](class09_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

``` r
grps3 <- cutree(hc, k=3)
grps3
```

    ##  [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 3 2 2 2 2 2 2
    ## [39] 3 3 3 2 2 3 3 2 2 2 3 2 3 2 2 2 3 2 2 2 3 2

``` r
table(grps3)
```

    ## grps3
    ##  1  2  3 
    ## 30 20 10

Q. How does this compare to your known ‘col’ groups?

``` r
plot(x, col=grps3)
```

![](class09_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

# Principal Component Analysis (PCA)

The main function in base R for PCA is called `prcomp()`. Here we will
use PCA to examine the funny food that folks eat in the UK and N.
Ireland.

Import the CSV file first:

``` r
x <- read.csv("UK_foods.csv", row.names=1)
x
```

    ##                     England Wales Scotland N.Ireland
    ## Cheese                  105   103      103        66
    ## Carcass_meat            245   227      242       267
    ## Other_meat              685   803      750       586
    ## Fish                    147   160      122        93
    ## Fats_and_oils           193   235      184       209
    ## Sugars                  156   175      147       139
    ## Fresh_potatoes          720   874      566      1033
    ## Fresh_Veg               253   265      171       143
    ## Other_Veg               488   570      418       355
    ## Processed_potatoes      198   203      220       187
    ## Processed_Veg           360   365      337       334
    ## Fresh_fruit            1102  1137      957       674
    ## Cereals                1472  1582     1462      1494
    ## Beverages                57    73       53        47
    ## Soft_drinks            1374  1256     1572      1506
    ## Alcoholic_drinks        375   475      458       135
    ## Confectionery            54    64       62        41

Make some conventional plots

``` r
barplot(as.matrix(x), beside=T, col=rainbow(nrow(x)))
```

![](class09_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

``` r
pairs(x, col=rainbow(10), pch=16)
```

![](class09_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

\#PCA to the rescue\!

``` r
pca <- prcomp(t(x))
```

``` r
summary(pca)
```

    ## Importance of components:
    ##                             PC1      PC2      PC3       PC4
    ## Standard deviation     324.1502 212.7478 73.87622 4.189e-14
    ## Proportion of Variance   0.6744   0.2905  0.03503 0.000e+00
    ## Cumulative Proportion    0.6744   0.9650  1.00000 1.000e+00

``` r
attributes(pca)
```

    ## $names
    ## [1] "sdev"     "rotation" "center"   "scale"    "x"       
    ## 
    ## $class
    ## [1] "prcomp"

``` r
pca
```

    ## Standard deviations (1, .., p=4):
    ## [1] 3.241502e+02 2.127478e+02 7.387622e+01 4.188568e-14
    ## 
    ## Rotation (n x k) = (17 x 4):
    ##                              PC1          PC2         PC3          PC4
    ## Cheese              -0.056955380 -0.016012850 -0.02394295 -0.691718038
    ## Carcass_meat         0.047927628 -0.013915823 -0.06367111  0.635384915
    ## Other_meat          -0.258916658  0.015331138  0.55384854  0.198175921
    ## Fish                -0.084414983  0.050754947 -0.03906481 -0.015824630
    ## Fats_and_oils       -0.005193623  0.095388656  0.12522257  0.052347444
    ## Sugars              -0.037620983  0.043021699  0.03605745  0.014481347
    ## Fresh_potatoes       0.401402060  0.715017078  0.20668248 -0.151706089
    ## Fresh_Veg           -0.151849942  0.144900268 -0.21382237  0.056182433
    ## Other_Veg           -0.243593729  0.225450923  0.05332841 -0.080722623
    ## Processed_potatoes  -0.026886233 -0.042850761  0.07364902 -0.022618707
    ## Processed_Veg       -0.036488269  0.045451802 -0.05289191  0.009235001
    ## Fresh_fruit         -0.632640898  0.177740743 -0.40012865 -0.021899087
    ## Cereals             -0.047702858  0.212599678  0.35884921  0.084667257
    ## Beverages           -0.026187756  0.030560542  0.04135860 -0.011880823
    ## Soft_drinks          0.232244140 -0.555124311  0.16942648 -0.144367046
    ## Alcoholic_drinks    -0.463968168 -0.113536523  0.49858320 -0.115797605
    ## Confectionery       -0.029650201 -0.005949921  0.05232164 -0.003695024

``` r
plot (pca$x[,1],pca$x[,2], xlab="PC1 (67.4%)", ylab="PC2 (29%)")
text(pca$x[,1],pca$x[,2], labels=colnames(x), col=c("black","red","blue","darkgreen"))
```

![](class09_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

``` r
attributes(pca)
```

    ## $names
    ## [1] "sdev"     "rotation" "center"   "scale"    "x"       
    ## 
    ## $class
    ## [1] "prcomp"
