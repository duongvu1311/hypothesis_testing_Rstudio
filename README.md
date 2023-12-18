# hypothesis_testing_Rstudio
Using RStudio to conduct basic hypothesis testing

First, we need to load the packages.
```r
library(tidyverse)
library(gapminder) #this is the dataset that we use to explore.
```
## 1. One-sample T-test
```r
#H0: The mean life expectancy in Africa is 50 years.
#H1: The mean life expectancy in Africa is not 50 years.
gapminder %>% 
  filter(continent == "Africa") %>% 
  select(lifeExp) %>% 
  t.test(mu = 50, conf.level = 0.95)
```
