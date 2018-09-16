hw01\_gapminder data exploration
================
JennyHuang
2018-09-16

### Load data

We will use gapminder for this data exploration assginment

``` r
library(gapminder)
```

### Exploration of data frames

Here are some ways to get familiar with the data frames

``` r
head(gapminder)
```

    ## # A tibble: 6 x 6
    ##   country     continent  year lifeExp      pop gdpPercap
    ##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Afghanistan Asia       1952    28.8  8425333      779.
    ## 2 Afghanistan Asia       1957    30.3  9240934      821.
    ## 3 Afghanistan Asia       1962    32.0 10267083      853.
    ## 4 Afghanistan Asia       1967    34.0 11537966      836.
    ## 5 Afghanistan Asia       1972    36.1 13079460      740.
    ## 6 Afghanistan Asia       1977    38.4 14880372      786.

``` r
tail(gapminder)
```

    ## # A tibble: 6 x 6
    ##   country  continent  year lifeExp      pop gdpPercap
    ##   <fct>    <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Zimbabwe Africa     1982    60.4  7636524      789.
    ## 2 Zimbabwe Africa     1987    62.4  9216418      706.
    ## 3 Zimbabwe Africa     1992    60.4 10704340      693.
    ## 4 Zimbabwe Africa     1997    46.8 11404948      792.
    ## 5 Zimbabwe Africa     2002    40.0 11926563      672.
    ## 6 Zimbabwe Africa     2007    43.5 12311143      470.

``` r
str(gapminder)
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    1704 obs. of  6 variables:
    ##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
    ##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
    ##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
    ##  $ gdpPercap: num  779 821 853 836 740 ...

``` r
class(gapminder)
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

``` r
ncol(gapminder)
```

    ## [1] 6

``` r
nrow(gapminder)
```

    ## [1] 1704

``` r
summary(gapminder)
```

    ##         country        continent        year         lifeExp     
    ##  Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
    ##  Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
    ##  Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
    ##  Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
    ##  Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
    ##  Australia  :  12                  Max.   :2007   Max.   :82.60  
    ##  (Other)    :1632                                                
    ##       pop              gdpPercap       
    ##  Min.   :6.001e+04   Min.   :   241.2  
    ##  1st Qu.:2.794e+06   1st Qu.:  1202.1  
    ##  Median :7.024e+06   Median :  3531.8  
    ##  Mean   :2.960e+07   Mean   :  7215.3  
    ##  3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
    ##  Max.   :1.319e+09   Max.   :113523.1  
    ## 

### Explore Variables

Here is a demonstration to select and filter data

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
Continent=filter(gapminder, continent=="Asia")
Time=Continent$year
pop=Continent$pop
gdp=Continent$gdpPercap
```

### Visualizing data

This is a basic plot relationship between gdp per cap and life
expectancy in
Asia

``` r
plot(lifeExp~gdp,Continent, type="l")
```

![](hw01_gapminder_data_exploration_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

Now, let’s use ggplot to demonstrate more informative graph with all
continents

``` r
library(ggplot2)
ggplot(gapminder, aes(x=gdpPercap, y=lifeExp, color=continent))+geom_point() # show continents in different color 
```

![](hw01_gapminder_data_exploration_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

The points are all clustered with all year (1952-2007) presented. Let’s
explore one year (e.g. 2002) data to see more clear pattern within each
continent.

First, “min” and “max” function can be used to explore data range. For
example:

``` r
min(gapminder$year)
```

    ## [1] 1952

``` r
max(gapminder$year)
```

    ## [1] 2007

Here we plot relationship between gdp per cap and life expectancy

``` r
dat=subset(gapminder, year==2002)
ggplot(dat, aes(x=gdpPercap, y=lifeExp, color=continent))+geom_point()+
  xlab("GDP per capita") + 
  ylab("Life expectancy (Years)") + ## change to more readable label
  scale_x_log10() # change to a log scale
```

![](hw01_gapminder_data_exploration_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->
