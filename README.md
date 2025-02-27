
<!-- README.md is generated from README.Rmd. Please edit the README.Rmd file -->

# Lab report \#1

Follow the instructions posted at
<https://ds202-at-isu.github.io/labs.html> for the lab assignment. The
work is meant to be finished during the lab time, but you have time
until Monday evening to polish things.

Include your answers in this document (Rmd file). Make sure that it
knits properly (into the md file). Upload both the Rmd and the md file
to your repository.

All submissions to the github repo will be automatically uploaded for
grading once the due date is passed. Submit a link to your repository on
Canvas (only one submission per team) to signal to the instructors that
you are done with your submission.

``` r
# install.packages("classdata")
# install.packages("ggplot2")
library(ggplot2)
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
library(classdata)
ames
```

    ## # A tibble: 6,935 × 16
    ##    `Parcel ID` Address     Style Occupancy `Sale Date` `Sale Price` `Multi Sale`
    ##    <chr>       <chr>       <fct> <fct>     <date>             <dbl> <chr>       
    ##  1 0903202160  1024 RIDGE… 1 1/… Single-F… 2022-08-12        181900 <NA>        
    ##  2 0907428215  4503 TWAIN… 1 St… Condomin… 2022-08-04        127100 <NA>        
    ##  3 0909428070  2030 MCCAR… 1 St… Single-F… 2022-08-15             0 <NA>        
    ##  4 0923203160  3404 EMERA… 1 St… Townhouse 2022-08-09        245000 <NA>        
    ##  5 0520440010  4507 EVERE… <NA>  <NA>      2022-08-03        449664 <NA>        
    ##  6 0907275030  4512 HEMIN… 2 St… Single-F… 2022-08-16        368000 <NA>        
    ##  7 0535105180  511 25TH S… 1 St… Single-F… 2022-08-03             0 <NA>        
    ##  8 0907428446  4510 TWAIN… 1 St… Condomin… 2022-08-16        110000 <NA>        
    ##  9 0527301030  3409 EISEN… 1 St… Single-F… 2022-08-08        350000 <NA>        
    ## 10 0531363050  5426 KANSA… 1 St… Single-F… 2022-08-03        242000 <NA>        
    ## # ℹ 6,925 more rows
    ## # ℹ 9 more variables: YearBuilt <dbl>, Acres <dbl>,
    ## #   `TotalLivingArea (sf)` <dbl>, Bedrooms <dbl>,
    ## #   `FinishedBsmtArea (sf)` <dbl>, `LotArea(sf)` <dbl>, AC <chr>,
    ## #   FirePlace <chr>, Neighborhood <fct>

``` r
ames <- ames
```

*Step 1* The variables contain strings, dates, and various pertinent
numeric information. -Parcel ID is the unique variable to identify the
building that was sold. - Address is the address. - Style contains the
number of stories in a housewith other relevant information. - Occupancy
addresses the housing density. - Sale Date is the date the house was
sold. - Sale Price is the main variable; it’s how much the house sold
for. - Year Built is the year each building was made. - Acres is the
property’s acreage.

*Step 2* The main variable seems to be the price; most people care a lot
more about the price than any other feature when purchasing a building.

*Step 3*

``` r
  ames2 <- ames %>% filter(`Sale Price` > 10, na.rm = TRUE)
  ggplot(ames2, aes(x = `Sale Price`)) + geom_histogram() + scale_x_log10()
```

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

*Step 4* Naomi will analyze the relationship between house cost and
total living area. Brandon will analyze the relationship between house
cost and year built. Cole will analyze the relationship between house
cost and acreage.

``` r
ames3 <- ames2 %>% filter(`LotArea(sf)` > 10, na.rm = TRUE)
  ggplot(ames3, aes(x = `Sale Price`, y = `LotArea(sf)`)) + scale_x_log10() + geom_point(shape = 8) + scale_y_log10()
```

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- --> *Step 4(Cole
Flickinger)* The range itself is homes within the cost of a few hundred
dollars all the way to a few million dollars with square footages
spanning from a couple hundred square feet all the way up to the tens of
thousands. Notably, the houses appear to mostly cost around upwards of
\$100,000 while the square footage seems to often be a little less than
10,000 square foot with a few outlier houses going for around the same
cost. There is not as strong of an upward trend of housing cost in
comparison to square-footage as I initially expected. This does explain
the extremely low cost house by itself in the graph that was shown
during the histogram. Notably, making sense that this low cost house
would also have an extremely small square-footage.

``` r
amesAge <- ames %>% filter(YearBuilt > 0, `Sale Price` > 0)
ggplot(amesAge, aes(x = YearBuilt)) + geom_histogram()
```

![](README_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
ggplot(amesAge, aes(x = log10(`Sale Price`), y = YearBuilt)) + geom_point()
```

![](README_files/figure-gfm/unnamed-chunk-4-2.png)<!-- -->  
Brandon Merrick Step 4: The Year Built ranges from about 1880 to 2020
with more houses generally existing for later years.  
There appears to only be a small effect when comparing Age to Price
where the majority cluster around the same area and newer houses having
more variability to both be above and below average  
This does not seem to describe any oddities  
