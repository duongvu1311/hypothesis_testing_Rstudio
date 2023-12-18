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
![Screenshot-2023-12-18-at-10-17-39-PM.png](https://i.postimg.cc/W45zxdcg/Screenshot-2023-12-18-at-10-17-39-PM.png)
As p-value < 0.05, we rejected the null hypothesis and concluded that mean life expectancy in Africa is not equal to 50 years.

## 2. Two-sample T-test
Firstly, we conduct Independent T-test to compare the mean in life expectancy of 2 different groups, which are Vietnam and Singapore.
```r
#2A. INDEPENDENT T-TEST
#Compare mean of lifeExp between Vietnam and Singapore
vietsing <- gapminder %>% 
  filter(country %in% c("Vietnam", "Singapore"))

#Independent T-test hypothesis:
#H0: The means in lifeExp in Vietnam & Singapore are the same.
#H1: The means in lifeExp in Vietnam & Singapore are different.
t.test(lifeExp ~ country, data=vietsing)
```
![Screenshot-2023-12-18-at-10-23-08-PM.png](https://i.postimg.cc/k5Z3VSrn/Screenshot-2023-12-18-at-10-23-08-PM.png)
As p-value < 0.05, we concluded that the means in life expectancy of Vietnam and Singapore are significantly different.

Then, another type of two-sample t-test is Paired T-test, which compares the mean difference of the same participants but in different times. 
```r
#2B. PAIRED T-TEST
#Mean life expectancy in Asian countries in 1957 and 2007
gapminder %>% 
  filter(year %in% c(1957, 2007) &
         continent == "Asia") %>% 
  group_by(year) %>% 
  summarise(mean_le = mean(lifeExp))

Asia <- gapminder %>% 
  filter(year %in% c(1957, 2007) &
           continent == "Asia")

#Paired t-test hypothesis:
#H0: The means in lifeExp in 1957 and 2007 in Asia are the same.
#H1: The means in lifeExp in 1957 and 2007 in Asia are different.
t.test(lifeExp ~ year, data = Asia, paired = TRUE)
```
![Screenshot-2023-12-18-at-10-28-04-PM.png](https://i.postimg.cc/bNC4sbfs/Screenshot-2023-12-18-at-10-28-04-PM.png)
Again, p-value here is less than 0.05, hence, we conclude that the mean in life expectancy of Asian countries in 1957 is significantly different from 2007.



