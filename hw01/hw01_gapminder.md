Gapminder Exploration
================
Lulu Pei
12/09/2019

  - [*Overview*](#overview)
  - [*Subsetting Dataset*](#subsetting-dataset)
  - [*Analysis*](#analysis)
  - [*Conclusion*](#conclusion)

## *Overview*

In this document, we will be performing some basic data exploration
using the `gapminder` dataset.

First, let’s load packages. We will need to load the `gapminder` package
to access the `gapminder` data set.

``` r
library(gapminder)
```

What exactly does the `gapminder` dataset contain? Let’s find out by
taking a look at the dataset description excerpt provided by R.

``` r
?gapminder
```

From this excerpt we can see that the dataset contains yearly
population, life expectancy, and GDP per capita data for 142 countries
representing 5 continents.

Here are the first 10 lines of the dataset to present an overview:

``` r
head(gapminder, 10)
```

    # A tibble: 10 x 6
       country     continent  year lifeExp      pop gdpPercap
       <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
     1 Afghanistan Asia       1952    28.8  8425333      779.
     2 Afghanistan Asia       1957    30.3  9240934      821.
     3 Afghanistan Asia       1962    32.0 10267083      853.
     4 Afghanistan Asia       1967    34.0 11537966      836.
     5 Afghanistan Asia       1972    36.1 13079460      740.
     6 Afghanistan Asia       1977    38.4 14880372      786.
     7 Afghanistan Asia       1982    39.9 12881816      978.
     8 Afghanistan Asia       1987    40.8 13867957      852.
     9 Afghanistan Asia       1992    41.7 16317921      649.
    10 Afghanistan Asia       1997    41.8 22227415      635.

Prior to performing any specific analysis, let’s obtain some summary
statistics for the variables contained in this dataset.

``` r
summary(gapminder)
```

``` 
        country        continent        year         lifeExp     
 Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
 Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
 Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
 Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
 Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
 Australia  :  12                  Max.   :2007   Max.   :82.60  
 (Other)    :1632                                                
      pop              gdpPercap       
 Min.   :6.001e+04   Min.   :   241.2  
 1st Qu.:2.794e+06   1st Qu.:  1202.1  
 Median :7.024e+06   Median :  3531.8  
 Mean   :2.960e+07   Mean   :  7215.3  
 3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
 Max.   :1.319e+09   Max.   :113523.1  
                                       
```

From the above output, we can read off 5-number summaries for the
continuous variables - `lifeExp`, `pop`, and `gdpPercap` - and frequency
data for the categorical variables - `country`, `continent`, and `year`.

With this basic understanding of the type of data that is contained
within this dataframe, let’s perform some exploratory data analysis\!

## *Subsetting Dataset*

Through observing the dataset, we can see that each country has
population data ranging from 1952 to 2007 in increments of 5 years. This
is a large dataset, so let’s breakdown the type of data that we are
dealing with.

``` r
str(gapminder)
```

    Classes 'tbl_df', 'tbl' and 'data.frame':   1704 obs. of  6 variables:
     $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
     $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
     $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
     $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
     $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
     $ gdpPercap: num  779 821 853 836 740 ...

From the output of this command, we can see that the `gapminder` dataset
contains 6 variables - three of which (`country`, `continent`, and
`year`) are categorical, and three of which (`lifeExp`, `pop`,
`gdpPercap`) are continuous. Suppose we are interested in investigating
how `lifeExp`, `pop` and `gdpPercap` variables have changed over time in
Canada. For simplicity, let’s select three time points: 1952, 1977, and
2007.

We will define dataframes `past` to contain all observations from 1952,
`mid` to contain all observations from 1977, and `present` to contain
all observations from 2007.

``` r
past <- subset(gapminder, year==1952)

mid <- subset(gapminder, year==1977)

present <- subset(gapminder, year==2007)
```

## *Analysis*

Now that we have all the prep work done, let’s begin our analysis\!
Starting with 1952, what were the population characteristics in Canada?

``` r
past[which(past$country=="Canada"), 4:6]
```

    # A tibble: 1 x 3
      lifeExp      pop gdpPercap
        <dbl>    <int>     <dbl>
    1    68.8 14785584    11367.

From this output we can observe that in 1952, Canada had a life
expectancy at birth of 68.8 years, a population of 14,785,584 people,
and a GDP per capita of US$11,367.

Now, let’s take a look at 1977.

``` r
mid[which(mid$country=="Canada"), 4:6]
```

    # A tibble: 1 x 3
      lifeExp      pop gdpPercap
        <dbl>    <int>     <dbl>
    1    74.2 23796400    22091.

In 1977, Canada had a life expectancy at birth of 74.2 years, a
population of 23,796,400 people, and a GDP per capita of US$22,091.

Finally, let’s analyze the most recent time point, 2007.

``` r
present[which(present$country=="Canada"), 4:6]
```

    # A tibble: 1 x 3
      lifeExp      pop gdpPercap
        <dbl>    <int>     <dbl>
    1    80.7 33390141    36319.

Using the same technique, we observe that in 2007, Canada had a
population of 33,390,141 people, with a life expectancy at birth of 80.7
years and a GDP per capita of US$36,319.

## *Conclusion*

Through this basic analysis of the Canadian subset of the `gapminder` dataset, we
can infer that the population characteristics of Canada have been
increasing relatively linearly between the years of 1952 and 2007.
Population increases by approximately 10 million people every 20 years,
while life expectancy increases by 6 years and GDP per capita increases
by approximately US$11,000.
