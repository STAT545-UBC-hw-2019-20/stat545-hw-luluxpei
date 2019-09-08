Gapminder Exploration
================
Lulu Pei
08/09/2019

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

With this basic understanding of the type of data that is contained
within this dataframe, let’s perform some exploratory data analysis\!

## *Analysis*

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
`gdpPercap`) are continuous. To obtain summaries of each variable, we
must consider the categorical and continuous variables separately.

Let’s first consider the continuous variables: `lifeExp`, `pop`, and
`gdpPercap`. The most efficient summary to obtain for continuous
variables is the 5-number summary, providing information on the mean,
median, minimum and maximum values, as well as quantile values.

``` r
summary(gapminder[,4:6])
```

``` 
    lifeExp           pop              gdpPercap       
 Min.   :23.60   Min.   :6.001e+04   Min.   :   241.2  
 1st Qu.:48.20   1st Qu.:2.794e+06   1st Qu.:  1202.1  
 Median :60.71   Median :7.024e+06   Median :  3531.8  
 Mean   :59.47   Mean   :2.960e+07   Mean   :  7215.3  
 3rd Qu.:70.85   3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
 Max.   :82.60   Max.   :1.319e+09   Max.   :113523.1  
```

From the 5-number summaries of each variable, we can make some
inferences about their distribution. Because the `mean` and `median` for
`lifeExp` are approximately equal, we can conclude that the distribution
for `lifeExp` is roughly symmetric and normally distributed. Regarding
both the `pop` and `gdpPercap` variables, the `mean` is greater than the
`median`, suggesting that the distributions of these variables are
positively skewed with larger values being more spread out than smaller
values.

Now, let’s consider the categorical variables: `country`, `continent`,
and `year`. The most efficient way to summarize such variables is
through the use of contingency tables.

``` r
table(gapminder$country)
```

``` 

             Afghanistan                  Albania                  Algeria 
                      12                       12                       12 
                  Angola                Argentina                Australia 
                      12                       12                       12 
                 Austria                  Bahrain               Bangladesh 
                      12                       12                       12 
                 Belgium                    Benin                  Bolivia 
                      12                       12                       12 
  Bosnia and Herzegovina                 Botswana                   Brazil 
                      12                       12                       12 
                Bulgaria             Burkina Faso                  Burundi 
                      12                       12                       12 
                Cambodia                 Cameroon                   Canada 
                      12                       12                       12 
Central African Republic                     Chad                    Chile 
                      12                       12                       12 
                   China                 Colombia                  Comoros 
                      12                       12                       12 
        Congo, Dem. Rep.              Congo, Rep.               Costa Rica 
                      12                       12                       12 
           Cote d'Ivoire                  Croatia                     Cuba 
                      12                       12                       12 
          Czech Republic                  Denmark                 Djibouti 
                      12                       12                       12 
      Dominican Republic                  Ecuador                    Egypt 
                      12                       12                       12 
             El Salvador        Equatorial Guinea                  Eritrea 
                      12                       12                       12 
                Ethiopia                  Finland                   France 
                      12                       12                       12 
                   Gabon                   Gambia                  Germany 
                      12                       12                       12 
                   Ghana                   Greece                Guatemala 
                      12                       12                       12 
                  Guinea            Guinea-Bissau                    Haiti 
                      12                       12                       12 
                Honduras         Hong Kong, China                  Hungary 
                      12                       12                       12 
                 Iceland                    India                Indonesia 
                      12                       12                       12 
                    Iran                     Iraq                  Ireland 
                      12                       12                       12 
                  Israel                    Italy                  Jamaica 
                      12                       12                       12 
                   Japan                   Jordan                    Kenya 
                      12                       12                       12 
        Korea, Dem. Rep.              Korea, Rep.                   Kuwait 
                      12                       12                       12 
                 Lebanon                  Lesotho                  Liberia 
                      12                       12                       12 
                   Libya               Madagascar                   Malawi 
                      12                       12                       12 
                Malaysia                     Mali               Mauritania 
                      12                       12                       12 
               Mauritius                   Mexico                 Mongolia 
                      12                       12                       12 
              Montenegro                  Morocco               Mozambique 
                      12                       12                       12 
                 Myanmar                  Namibia                    Nepal 
                      12                       12                       12 
             Netherlands              New Zealand                Nicaragua 
                      12                       12                       12 
                   Niger                  Nigeria                   Norway 
                      12                       12                       12 
                    Oman                 Pakistan                   Panama 
                      12                       12                       12 
                Paraguay                     Peru              Philippines 
                      12                       12                       12 
                  Poland                 Portugal              Puerto Rico 
                      12                       12                       12 
                 Reunion                  Romania                   Rwanda 
                      12                       12                       12 
   Sao Tome and Principe             Saudi Arabia                  Senegal 
                      12                       12                       12 
                  Serbia             Sierra Leone                Singapore 
                      12                       12                       12 
         Slovak Republic                 Slovenia                  Somalia 
                      12                       12                       12 
            South Africa                    Spain                Sri Lanka 
                      12                       12                       12 
                   Sudan                Swaziland                   Sweden 
                      12                       12                       12 
             Switzerland                    Syria                   Taiwan 
                      12                       12                       12 
                Tanzania                 Thailand                     Togo 
                      12                       12                       12 
     Trinidad and Tobago                  Tunisia                   Turkey 
                      12                       12                       12 
                  Uganda           United Kingdom            United States 
                      12                       12                       12 
                 Uruguay                Venezuela                  Vietnam 
                      12                       12                       12 
      West Bank and Gaza              Yemen, Rep.                   Zambia 
                      12                       12                       12 
                Zimbabwe 
                      12 
```

``` r
table(gapminder$continent)
```

``` 

  Africa Americas     Asia   Europe  Oceania 
     624      300      396      360       24 
```

``` r
table(gapminder$year)
```

``` 

1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 2002 2007 
 142  142  142  142  142  142  142  142  142  142  142  142 
```

From the output, we can see that each country is represented 12 times in
the dataset, which reflects the 12 year points at which data was
collected. Each year point is represented 142 times in the dataset,
reflecting the 142 countries included in the `gapminder` dataset. We can
also observe the country distribution by continent. To do this, we must
take `continent` frequencies and divide by the number of year points to
remove duplicating countries.

``` r
table(gapminder$continent) / 12
```

``` 

  Africa Americas     Asia   Europe  Oceania 
      52       25       33       30        2 
```

This command allows us to conclude that the `gapminder` dataset contains
population data from 52 countries in Africa, 25 countries in the
Americas, 33 countries in Asia, 30 countries in Europe, and 2 countries
in Oceania, representing a total of 142 countries globally.
