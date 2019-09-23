---
title: "Assignment 2 - `dplyr` exploration"
author: "Lulu Pei"
date: "22/09/2019"
output: 
  html_document:
    toc: TRUE
    keep_md: TRUE
---

# Overview

Before playing around with the various `dplyr` commands, we must define a dataset. In this case, we will be looking at the `gapminder` dataset. To access the `gapminder` dataset, we need to load the `gapminder` package. To be able to call and use `dplyr` commands, we must load the `tidyverse` package as well. 


```r
library(gapminder)
library(tidyverse)
```

<br>

# Question 1 - Basic `dplyr`

## _1.1 - Filtering_

Filter `gapminder` data to contain only observations from Canada, the United States, and Mexico in the 1970s.


```r
gapminder %>%
  filter(country == 'Canada' | country == 'United States' | country == 'Mexico',
         year >= 1970 & year < 1980) %>%
  knitr::kable()
```



country         continent    year   lifeExp         pop   gdpPercap
--------------  ----------  -----  --------  ----------  ----------
Canada          Americas     1972    72.880    22284500   18970.571
Canada          Americas     1977    74.210    23796400   22090.883
Mexico          Americas     1972    62.361    55984294    6809.407
Mexico          Americas     1977    65.032    63759976    7674.929
United States   Americas     1972    71.340   209896000   21806.036
United States   Americas     1977    73.380   220239000   24072.632

## _1.2 - Selecting_

Let's select only `country` and `gdpPercap` variables from our filtered subset of the `gapminder` dataset.


```r
gapminder %>%
  filter(country == 'Canada' | country == 'United States' | country == 'Mexico',
         year >= 1970 & year < 1980) %>%
  select(country, gdpPercap) %>%
  knitr::kable()
```



country          gdpPercap
--------------  ----------
Canada           18970.571
Canada           22090.883
Mexico            6809.407
Mexico            7674.929
United States    21806.036
United States    24072.632

## _1.3 - Mutating_

Suppose we want to look at all the countries that have ever experienced a drop in life expectancy between 1952 and 2007. Let's define a new variable `lifeExp_change`, equaling the difference between life expectancy at one time point and life expectancy at the time point before.


```r
gapminder %>%
  group_by(country) %>%
  mutate(lifeExp_change = lifeExp - lag(lifeExp, order_by = year)) %>%
  filter(lifeExp_change < 0) %>%
  DT::datatable()
```

<!--html_preserve--><div id="htmlwidget-e5795dfdec95bfd981b2" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-e5795dfdec95bfd981b2">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52","53","54","55","56","57","58","59","60","61","62","63","64","65","66","67","68","69","70","71","72","73","74","75","76","77","78","79","80","81","82","83","84","85","86","87","88","89","90","91","92","93","94","95","96","97","98","99","100","101","102"],["Albania","Angola","Benin","Botswana","Botswana","Botswana","Bulgaria","Bulgaria","Bulgaria","Burundi","Cambodia","Cambodia","Cameroon","Cameroon","Cameroon","Central African Republic","Central African Republic","Central African Republic","Chad","Chad","China","Congo, Dem. Rep.","Congo, Dem. Rep.","Congo, Dem. Rep.","Congo, Dem. Rep.","Congo, Rep.","Congo, Rep.","Cote d'Ivoire","Cote d'Ivoire","Cote d'Ivoire","Croatia","Czech Republic","Denmark","El Salvador","El Salvador","Eritrea","Gabon","Gabon","Gabon","Ghana","Hungary","Hungary","Iraq","Iraq","Iraq","Jamaica","Jamaica","Kenya","Kenya","Kenya","Korea, Dem. Rep.","Korea, Dem. Rep.","Korea, Dem. Rep.","Lesotho","Lesotho","Lesotho","Liberia","Malawi","Malawi","Montenegro","Mozambique","Mozambique","Myanmar","Namibia","Namibia","Netherlands","Nigeria","Nigeria","Norway","Poland","Poland","Puerto Rico","Romania","Romania","Rwanda","Rwanda","Serbia","Sierra Leone","Slovak Republic","Somalia","South Africa","South Africa","South Africa","Swaziland","Swaziland","Swaziland","Tanzania","Tanzania","Togo","Trinidad and Tobago","Trinidad and Tobago","Uganda","Uganda","Uganda","Uganda","Zambia","Zambia","Zambia","Zambia","Zimbabwe","Zimbabwe","Zimbabwe"],["Europe","Africa","Africa","Africa","Africa","Africa","Europe","Europe","Europe","Africa","Asia","Asia","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Asia","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Europe","Europe","Europe","Americas","Americas","Africa","Africa","Africa","Africa","Africa","Europe","Europe","Asia","Asia","Asia","Americas","Americas","Africa","Africa","Africa","Asia","Asia","Asia","Africa","Africa","Africa","Africa","Africa","Africa","Europe","Africa","Africa","Asia","Africa","Africa","Europe","Africa","Africa","Europe","Europe","Europe","Americas","Europe","Europe","Africa","Africa","Europe","Africa","Europe","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Americas","Americas","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa"],[1992,1987,2002,1992,1997,2002,1977,1992,1997,1992,1972,1977,1992,1997,2002,1992,1997,2002,1997,2002,1962,1982,1987,1992,1997,1992,1997,1992,1997,2002,1982,1972,1982,1977,1982,1982,1997,2002,2007,2002,1982,1992,1992,1997,2002,1992,2002,1992,1997,2002,1992,1997,2002,1997,2002,2007,1992,1997,2002,2002,2002,2007,2002,1997,2002,1972,1997,2002,1987,1977,1987,1992,1987,1992,1987,1992,1982,1992,1972,1992,1997,2002,2007,1997,2002,2007,1992,1997,2002,1997,2002,1977,1982,1992,1997,1987,1992,1997,2002,1992,1997,2002],[71.581,39.906,54.406,62.745,52.556,46.634,70.81,71.19,70.32,44.736,40.317,31.22,54.314,52.199,49.856,49.396,46.066,43.308,51.573,50.525,44.50136,47.784,47.412,45.548,42.587,56.433,52.962,52.044,47.991,46.832,70.46,70.29,74.63,56.696,56.604,43.89,60.461,56.761,56.735,58.453,69.39,69.17,59.461,58.811,57.046,71.766,72.047,59.285,54.407,50.992,69.978,67.727,66.662,55.558,44.593,42.592,40.802,47.495,45.009,73.981,44.026,42.082,59.908,58.909,51.479,73.75,47.464,46.608,75.89,70.67,70.98,73.911,69.53,69.36,44.02,23.599,70.162,38.333,70.35,39.658,60.236,53.365,49.339,54.289,43.869,39.613,50.44,48.466,57.561,69.465,68.976,50.35,49.849,48.825,44.578,50.821,46.1,40.238,39.193,60.377,46.809,39.989],[3326498,7874230,7026113,1342614,1536536,1630347,8797022,8658506,8066057,5809236,7450606,6978607,12467171,14195809,15929988,3265124,3696513,4048013,7562011,8835739,665770000,30646495,35481645,41672143,47798986,2409073,2800947,12772596,14625967,16252726,4413368,9862158,5117810,4282586,4474873,2637297,1126189,1299304,1454867,20550751,10705535,10348684,17861905,20775703,24001816,2378618,2664659,25020539,28263827,31386842,20711375,21585105,22215365,1982823,2046772,2012649,1912974,10419991,11824495,720230,18473780,19951656,45598081,1774766,1972153,13329874,106207839,119901274,4186147,34621254,37740710,3585176,22686371,22797027,6349365,7290203,9032824,4260884,4593433,6099799,42835005,44433622,43997828,1054486,1130269,1133066,26605473,30686889,4977378,1138101,1101832,11457758,12939400,18252190,21210254,7272406,8381163,9417789,10595811,10704340,11404948,11926563],[2497.437901,2430.208311,1372.877931,7954.111645,8647.142313,11003.60508,7612.240438,6302.623438,5970.38876,631.6998778,421.6240257,524.9721832,1793.163278,1694.337469,1934.011449,747.9055252,740.5063317,738.6906068,1004.961353,1156.18186,487.6740183,673.7478181,672.774812,457.7191807,312.188423,4016.239529,3484.164376,1648.073791,1786.265407,1648.800823,13221.82184,13108.4536,21688.04048,5138.922374,4098.344175,524.8758493,14722.84188,12521.71392,13206.48452,1111.984578,12545.99066,10535.62855,3745.640687,3076.239795,4390.717312,7404.923685,6994.774861,1341.921721,1360.485021,1287.514732,3726.063507,1690.756814,1646.758151,1186.147994,1275.184575,1569.331442,636.6229191,692.2758103,665.4231186,6557.194282,633.6179466,823.6856205,611,3899.52426,4072.324751,18794.74567,1624.941275,1615.286395,31540.9748,9508.141454,9082.351172,14641.58711,9696.273295,6598.409903,847.991217,737.0685949,15181.0927,1068.696278,9674.167626,926.9602964,7479.188244,7710.946444,9269.657808,3876.76846,4128.116943,4513.480643,825.682454,789.1862231,886.2205765,8792.573126,11460.60023,843.7331372,682.2662268,644.1707969,816.559081,1213.315116,1210.884633,1071.353818,1071.613938,693.4207856,792.4499603,672.0386227],[-0.418999999999997,-0.0360000000000014,-0.371000000000002,-0.877000000000002,-10.189,-5.922,-0.0900000000000034,-0.150000000000006,-0.870000000000005,-3.475,-5.098,-9.097,-0.670999999999999,-2.115,-2.343,-1.089,-3.33,-2.758,-0.150999999999996,-1.048,-6.0476,-0.0200000000000031,-0.372,-1.864,-2.961,-1.037,-3.471,-2.611,-4.053,-1.159,-0.180000000000007,-0.0899999999999892,-0.0600000000000023,-1.511,-0.0919999999999987,-0.644999999999996,-0.905000000000001,-3.7,-0.0260000000000034,-0.102999999999994,-0.560000000000002,-0.409999999999997,-5.583,-0.649999999999999,-1.765,-0.00399999999999068,-0.215000000000003,-0.054000000000002,-4.878,-3.415,-0.669000000000011,-2.25099999999999,-1.065,-4.127,-10.965,-2.001,-5.225,-1.925,-2.486,-1.464,-2.318,-1.944,-0.420000000000002,-3.09,-7.43,-0.0699999999999932,-0.00800000000000267,-0.856000000000002,-0.0799999999999983,-0.179999999999993,-0.339999999999989,-0.718999999999994,-0.129999999999995,-0.170000000000002,-2.198,-20.421,-0.137999999999991,-1.673,-0.63000000000001,-4.843,-1.652,-6.871,-4.026,-4.185,-10.42,-4.256,-1.095,-1.974,-0.829000000000001,-0.396999999999991,-0.489000000000004,-0.665999999999997,-0.501000000000005,-2.684,-4.247,-1,-4.721,-5.862,-1.045,-1.974,-13.568,-6.82]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>country<\/th>\n      <th>continent<\/th>\n      <th>year<\/th>\n      <th>lifeExp<\/th>\n      <th>pop<\/th>\n      <th>gdpPercap<\/th>\n      <th>lifeExp_change<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[3,4,5,6,7]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

We can see that many countries have experienced a drop in life expectancy at some point between 1952 and 2007; however, what if we are only interested in countries that have experienced an overall life expectancy drop between the most recent year (2007) and the earliest year (1952).


```r
gapminder %>%
  filter(year == 1952 | year == 2007) %>%
  group_by(country) %>%
  mutate(lifeExp_change = lifeExp - lag(lifeExp)) %>%
  filter(lifeExp_change < 0) %>%
  knitr::kable()
```



country     continent    year   lifeExp        pop   gdpPercap   lifeExp_change
----------  ----------  -----  --------  ---------  ----------  ---------------
Swaziland   Africa       2007    39.613    1133066   4513.4806           -1.794
Zimbabwe    Africa       2007    43.487   12311143    469.7093           -4.964

From this output, we can see that the only countries that experienced an overall decline in life expectancy were Swaziland and Zimbabwe, with a decline of 1.794 and 4.964 years, respectively.

## _1.4 - Slicing_

Now, let's filter the `gapminder` dataset to show the maximum GDP per capita experienced by each country.


```r
gapminder %>%
  select(country, gdpPercap) %>%
  group_by(country) %>%
  slice(which.max(gdpPercap)) %>%
  rename(max_gdpPercap = gdpPercap) %>%
  DT::datatable()
```

<!--html_preserve--><div id="htmlwidget-56a885701b6aab72856d" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-56a885701b6aab72856d">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52","53","54","55","56","57","58","59","60","61","62","63","64","65","66","67","68","69","70","71","72","73","74","75","76","77","78","79","80","81","82","83","84","85","86","87","88","89","90","91","92","93","94","95","96","97","98","99","100","101","102","103","104","105","106","107","108","109","110","111","112","113","114","115","116","117","118","119","120","121","122","123","124","125","126","127","128","129","130","131","132","133","134","135","136","137","138","139","140","141","142"],["Afghanistan","Albania","Algeria","Angola","Argentina","Australia","Austria","Bahrain","Bangladesh","Belgium","Benin","Bolivia","Bosnia and Herzegovina","Botswana","Brazil","Bulgaria","Burkina Faso","Burundi","Cambodia","Cameroon","Canada","Central African Republic","Chad","Chile","China","Colombia","Comoros","Congo, Dem. Rep.","Congo, Rep.","Costa Rica","Cote d'Ivoire","Croatia","Cuba","Czech Republic","Denmark","Djibouti","Dominican Republic","Ecuador","Egypt","El Salvador","Equatorial Guinea","Eritrea","Ethiopia","Finland","France","Gabon","Gambia","Germany","Ghana","Greece","Guatemala","Guinea","Guinea-Bissau","Haiti","Honduras","Hong Kong, China","Hungary","Iceland","India","Indonesia","Iran","Iraq","Ireland","Israel","Italy","Jamaica","Japan","Jordan","Kenya","Korea, Dem. Rep.","Korea, Rep.","Kuwait","Lebanon","Lesotho","Liberia","Libya","Madagascar","Malawi","Malaysia","Mali","Mauritania","Mauritius","Mexico","Mongolia","Montenegro","Morocco","Mozambique","Myanmar","Namibia","Nepal","Netherlands","New Zealand","Nicaragua","Niger","Nigeria","Norway","Oman","Pakistan","Panama","Paraguay","Peru","Philippines","Poland","Portugal","Puerto Rico","Reunion","Romania","Rwanda","Sao Tome and Principe","Saudi Arabia","Senegal","Serbia","Sierra Leone","Singapore","Slovak Republic","Slovenia","Somalia","South Africa","Spain","Sri Lanka","Sudan","Swaziland","Sweden","Switzerland","Syria","Taiwan","Tanzania","Thailand","Togo","Trinidad and Tobago","Tunisia","Turkey","Uganda","United Kingdom","United States","Uruguay","Venezuela","Vietnam","West Bank and Gaza","Yemen, Rep.","Zambia","Zimbabwe"],[978.0114388,5937.029526,6223.367465,5522.776375,12779.37964,34435.36744,36126.4927,29796.04834,1391.253792,33692.60508,1441.284873,3822.137084,7446.298803,12569.85177,9065.800825,10680.79282,1217.032994,631.6998778,1713.778686,2602.664206,36319.23501,1193.068753,1704.063724,13171.63885,4959.114854,7006.580419,1937.577675,905.8602303,4879.507522,9645.06142,2602.710169,14619.22272,8948.102923,22833.30851,35278.41874,3694.212352,6025.374752,7429.455877,5581.180998,5728.353514,12154.08975,913.47079,690.8055759,33207.0844,30470.0167,21745.57328,884.7552507,32170.37442,1327.60891,27538.41188,5186.050003,945.5835837,838.1239671,2011.159549,3548.330846,39724.97867,18008.94444,36180.78919,2452.210407,3540.651564,11888.59508,14688.23507,40675.99635,25523.2771,28569.7197,7433.889293,31656.06806,4519.461171,1463.249282,4106.525293,23348.13973,113523.1329,10461.05868,1569.331442,803.0054535,21951.21176,1748.562982,759.3499101,12451.6558,1042.581557,1803.151496,10956.99112,11977.57496,3095.772271,11732.51017,3820.17523,823.6856205,944,4811.060429,1091.359778,36797.93332,25185.00911,5486.371089,1054.384891,2013.977305,49357.19017,22316.19287,2605.94758,9809.185636,4258.503604,7408.905561,3190.481016,15389.92468,20509.64777,19328.70901,7670.122558,10808.47561,881.5706467,1890.218117,34167.7626,1712.472136,15870.87851,1465.010784,47143.17964,18678.31435,25768.25759,1450.992513,9269.657808,28821.0637,3970.095407,2602.394995,4513.480643,33859.74835,37506.41907,4184.548089,28718.27684,1107.482182,7458.396327,1649.660188,18008.50924,7092.923025,8458.276384,1056.380121,33203.26128,42951.65309,10611.46299,13143.95095,2441.576404,7110.667619,2280.769906,1777.077318,799.3621758]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>country<\/th>\n      <th>max_gdpPercap<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":2},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

This output allows us to determine in which year a country had its maximum GDP per capita, and what the life expectancy, population, and GDP per capita was at that time. 
<br>

## _1.5 - Plotting_

Let's investigate the relationship between life expectancy and GDP per capita in Canada. To do this, we will create a scatterplot using `ggplot2`. 


```r
gapminder %>%
  filter(country == "Canada") %>%
  ggplot(aes(gdpPercap, lifeExp)) +
  geom_point(colour = "orange", size = 2) +
  scale_x_log10() +
  xlab("GDP per capita (log(US$))") +
  ylab("Life expectancy at birth (years)")
```

<img src="hw02_dplyr_exploration_files/figure-html/unnamed-chunk-6-1.png" style="display: block; margin: auto;" />

From this plot, we can see that in Canada, life expectancy has been increasing relatively linearly with the log transform of GDP per capita between the years of 1952 and 2007.

<br>

# Question 2 - Variable Exploration

To perform individual variable exploration using `dplyr` we will choose one categorical variable and one quantitative variable to explore. Let's say we want to analyze `continent` as the categorical variable and `population` as the quantitative variable.

## _2.1 - Categorical_ 

The categorical variable we are interested in exploring is `continent`. To start off, let's first investigate which continents are represented in our `gapminder` dataset. 


```r
levels(gapminder$continent)
```

```
[1] "Africa"   "Americas" "Asia"     "Europe"   "Oceania" 
```

Categorical variable exploration is usually performed through the generation of frequency tables - let's generate one for the `continent` variable. 


```r
gapminder %>%
  count(continent) %>%
  knitr::kable()
```



continent      n
----------  ----
Africa       624
Americas     300
Asia         396
Europe       360
Oceania       24

This command prints out the number of observations for each continent in our dataset. However, by looking at the `gapminder` dataset, we see that each country contributes 12 observations (represeting 12 time points) to the dataset. Suppose we want to know how many countries are in each continent for the `gapminder` dataset. To determine this, we need to remove replicates of the same country. The simpliest way to achieve this is to consider continent counts at each time point.


```r
gapminder %>%
  group_by(year) %>%
  count(continent) %>%
  DT::datatable()
```

<!--html_preserve--><div id="htmlwidget-ce43042c47d95d4f0afd" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-ce43042c47d95d4f0afd">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52","53","54","55","56","57","58","59","60"],[1952,1952,1952,1952,1952,1957,1957,1957,1957,1957,1962,1962,1962,1962,1962,1967,1967,1967,1967,1967,1972,1972,1972,1972,1972,1977,1977,1977,1977,1977,1982,1982,1982,1982,1982,1987,1987,1987,1987,1987,1992,1992,1992,1992,1992,1997,1997,1997,1997,1997,2002,2002,2002,2002,2002,2007,2007,2007,2007,2007],["Africa","Americas","Asia","Europe","Oceania","Africa","Americas","Asia","Europe","Oceania","Africa","Americas","Asia","Europe","Oceania","Africa","Americas","Asia","Europe","Oceania","Africa","Americas","Asia","Europe","Oceania","Africa","Americas","Asia","Europe","Oceania","Africa","Americas","Asia","Europe","Oceania","Africa","Americas","Asia","Europe","Oceania","Africa","Americas","Asia","Europe","Oceania","Africa","Americas","Asia","Europe","Oceania","Africa","Americas","Asia","Europe","Oceania","Africa","Americas","Asia","Europe","Oceania"],[52,25,33,30,2,52,25,33,30,2,52,25,33,30,2,52,25,33,30,2,52,25,33,30,2,52,25,33,30,2,52,25,33,30,2,52,25,33,30,2,52,25,33,30,2,52,25,33,30,2,52,25,33,30,2,52,25,33,30,2]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>year<\/th>\n      <th>continent<\/th>\n      <th>n<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[1,3]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

We see that country distirbution does not change from year to year - there are the same number of countries in each of the 5 continents: Africa, the Americas, Asia, Europe, and Oceania. In our dataset, 52 countries are represented from Africa, 25 countries from the Americas, 33 countries from Asia, 30 countries from Europe, and 2 countries from Oceania. Let's view this data graphically using a bar graph - because continent counts do not change between years, it is sufficient to plot data from a single time point.


```r
gapminder %>%
  group_by(year) %>%
  filter(year==2007) %>%
  ggplot(aes(continent)) +
  geom_bar(fill = "orange", alpha = 0.7) +
  ylab("Number of Countries") +
  xlab("Continent")
```

<img src="hw02_dplyr_exploration_files/figure-html/unnamed-chunk-10-1.png" style="display: block; margin: auto;" />

## _2.2 - Quantitative_

Quantitative variable exploration is usually performed through the generation of 5-number summaries: min, 1st quartile, median, 3rd quartile, max. Let's generate a variation of the 5-number summary for the `pop` variable, including a measure of spread. 


```r
gapminder %>%
  summarise("min_pop (million)" = min(pop)/(10^6), "mean_pop (million)" = mean(pop)/(10^6), 
            "median_pop (million)" = median(pop)/(10^6), "max_pop (million)" = max(pop)/(10^6), 
            "sd_pop (million)" = sd(pop)/(10^6)) %>%
  knitr::kable()
```



 min_pop (million)   mean_pop (million)   median_pop (million)   max_pop (million)   sd_pop (million)
------------------  -------------------  ---------------------  ------------------  -----------------
          0.060011             29.60121               7.023595            1318.683           106.1579

From the output, we can observe the minimum and maximum values for population as well as the median and mean values and the standard deviation. We observe a deviation between population mean and population median, suggesting that the distribution is skewed with greater density towards lower values (`mean_pop` > `median_pop`).

However, these values are difficult to interpret because they refer to the population distribution across all countries between 1952 and 2007. It may be more informative if we investigated the change in population distribution from year to year, for example. 


```r
gapminder %>%
  select(year, pop) %>%  
  group_by(year) %>%
  summarise("min_pop (million)" = min(pop)/(10^6), "mean_pop (million)" = mean(pop)/(10^6), 
            "median_pop (million)" = median(pop)/(10^6), "max_pop (million)" = max(pop)/(10^6), 
            "sd_pop (million)" = sd(pop)/(10^6)) %>%
  knitr::kable()
```



 year   min_pop (million)   mean_pop (million)   median_pop (million)   max_pop (million)   sd_pop (million)
-----  ------------------  -------------------  ---------------------  ------------------  -----------------
 1952            0.060011             16.95040               3.943953            556.2635           58.10086
 1957            0.061325             18.76341               4.282942            637.4080           65.50429
 1962            0.065345             20.42101               4.686039            665.7700           69.78865
 1967            0.070787             22.65830               5.170176            754.5500           78.37548
 1972            0.076595             25.18998               5.877997            862.0300           88.64682
 1977            0.086796             27.67638               6.404037            943.4550           97.48109
 1982            0.098593             30.20730               7.007320           1000.2810          105.09865
 1987            0.110812             33.03857               7.774862           1084.0350          114.75618
 1992            0.125911             35.99092               8.688686           1164.9700          124.50259
 1997            0.145608             38.83947               9.735064           1230.0750          133.41739
 2002            0.170372             41.45759              10.372919           1280.4000          140.84828
 2007            0.199579             44.02122              10.517531           1318.6831          147.62140

From these summary statistics, we can see that there is a lot of variation in the `pop` variable (large standard deviation values). This is to be expected due to the large variation in population size across countries in the world. To visualize this graphically, we can plot side-by-side boxplots representing global population data at each time point.


```r
gapminder %>%
  mutate(year = factor(year)) %>%
  ggplot(aes(year, pop)) +
  geom_boxplot() +
  scale_y_log10("Population (log scale)") +
  xlab("Year")
```

<img src="hw02_dplyr_exploration_files/figure-html/unnamed-chunk-13-1.png" style="display: block; margin: auto;" />

From this graph, we can observe a relatively consistent slow linear increase in log-transformed population over time, suggesting that between 1952 and 2007, global population has been steadily increasing. 

<br>

# Question 3 - Plot Exploration

## _3.1 - Scatterplot_

The first plot type that we are going to explore is the scatterplot. Suppose we want to group the `gapminder` dataset by continent, and then plot the relationship between life expectancy at birth and GDP per capita.


```r
gapminder %>%
  group_by(continent) %>%
  ggplot(aes(x = gdpPercap, y = lifeExp, colour = continent)) +
  geom_point(alpha = 0.7) +
  scale_x_log10() +
  ylab("Life expectancy at birth (year)") +
  xlab("GDP per capita (log(US$))")
```

<img src="hw02_dplyr_exploration_files/figure-html/unnamed-chunk-14-1.png" style="display: block; margin: auto;" />

From the scatterplot, we can see that life expectancy and GDP per capita are roughly positively correlated, following a linear relationship. Not only does life expectancy tend to increase with GDP per capita, we can also observe that countries in Europe and Oceania tend to have higher life expectancy and GDP whereas countries in Africa tend to have lower life expectancy and GDP. Countries in the Americas and Asia seem to have more varied distributions of life expectancy and GDP with more discrepancy between countries.

## _3.2 - Time Series_

The second plot type we are going to explore is a time series. Suppose we want to investigate how population has changed over time between 1952 and 2007 in Canada, France, and Australia. We can visualize this through making a time series plot and fitting a trendline. 


```r
gapminder %>%
  filter(country == "Canada" | country == "France" | country == "Australia") %>%
  ggplot(aes(x = year, y = pop, col = country)) +
  geom_point(size = 2) +
  geom_line(size = 1) +
  xlab("Year") +
  ylab("Population") +
  theme(legend.title=element_blank())
```

<img src="hw02_dplyr_exploration_files/figure-html/unnamed-chunk-15-1.png" style="display: block; margin: auto;" />

From observing the trendlines, we can observe that all countries have experienced roughly linear increases in population over time. Canada and France seem to have similar rates of population increase, while the rate of increase in population is slower in Australia. Between 1952 and 2007, Canada and France have experienced an increase in population of approximately 20 million people, while Australia's population has increased by approximately 10 million people. 

# Bonus - Recycling

Evaluation of the following command:


```r
filter(gapminder, country == c("Rwanda", "Afghanistan")) %>%
  DT::datatable()
```

<!--html_preserve--><div id="htmlwidget-c57191c4634d2eab1a84" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-c57191c4634d2eab1a84">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12"],["Afghanistan","Afghanistan","Afghanistan","Afghanistan","Afghanistan","Afghanistan","Rwanda","Rwanda","Rwanda","Rwanda","Rwanda","Rwanda"],["Asia","Asia","Asia","Asia","Asia","Asia","Africa","Africa","Africa","Africa","Africa","Africa"],[1957,1967,1977,1987,1997,2007,1952,1962,1972,1982,1992,2002],[30.332,34.02,38.438,40.822,41.763,43.828,40,43,44.6,46.218,23.599,43.413],[9240934,11537966,14880372,13867957,22227415,31889923,2534927,3051242,3992121,5507565,7290203,7852401],[820.8530296,836.1971382,786.11336,852.3959448,635.341351,974.5803384,493.3238752,597.4730727,590.5806638,881.5706467,737.0685949,785.6537648]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>country<\/th>\n      <th>continent<\/th>\n      <th>year<\/th>\n      <th>lifeExp<\/th>\n      <th>pop<\/th>\n      <th>gdpPercap<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[3,4,5,6]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

The analyst's goal was to obtain a subset of the `gapminder` dataset, containing data from Rwanda and Afghanistan. However, the output of the above command only returns 12 observations when there should have been 24 (12 observations for each country representing the 12 time points between 1952 and 2007). Each year should have both a Rwanda observation and an Afghanistan observation; however, in our subset, each year is only represented by one country. This suggests that the subsetted data is incomplete. 

To correctly obtain all data from Rwanda and Afghanistan, we can use the logical "or" operator (denoted as "|" in `dplyr`). The code below will return a dataframe that contains all observations from either Rwanda or Afghanistan.


```r
filter(gapminder, country == "Rwanda" | country == "Afghanistan") %>%
  DT::datatable()
```

<!--html_preserve--><div id="htmlwidget-afdfb1616ee283363770" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-afdfb1616ee283363770">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24"],["Afghanistan","Afghanistan","Afghanistan","Afghanistan","Afghanistan","Afghanistan","Afghanistan","Afghanistan","Afghanistan","Afghanistan","Afghanistan","Afghanistan","Rwanda","Rwanda","Rwanda","Rwanda","Rwanda","Rwanda","Rwanda","Rwanda","Rwanda","Rwanda","Rwanda","Rwanda"],["Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Asia","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa","Africa"],[1952,1957,1962,1967,1972,1977,1982,1987,1992,1997,2002,2007,1952,1957,1962,1967,1972,1977,1982,1987,1992,1997,2002,2007],[28.801,30.332,31.997,34.02,36.088,38.438,39.854,40.822,41.674,41.763,42.129,43.828,40,41.5,43,44.1,44.6,45,46.218,44.02,23.599,36.087,43.413,46.242],[8425333,9240934,10267083,11537966,13079460,14880372,12881816,13867957,16317921,22227415,25268405,31889923,2534927,2822082,3051242,3451079,3992121,4657072,5507565,6349365,7290203,7212583,7852401,8860588],[779.4453145,820.8530296,853.10071,836.1971382,739.9811058,786.11336,978.0114388,852.3959448,649.3413952,635.341351,726.7340548,974.5803384,493.3238752,540.2893983,597.4730727,510.9637142,590.5806638,670.0806011,881.5706467,847.991217,737.0685949,589.9445051,785.6537648,863.0884639]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>country<\/th>\n      <th>continent<\/th>\n      <th>year<\/th>\n      <th>lifeExp<\/th>\n      <th>pop<\/th>\n      <th>gdpPercap<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[3,4,5,6]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

From this output, we see that we are left with a dataframe of the correct dimensions (24 observations) with all data from Rwanda and Afghanistan between 1952 and 2007. 
