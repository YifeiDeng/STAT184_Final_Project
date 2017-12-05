# STAT184_Final_Project
Final Project for STAT 184
---
title: "Final Project Draft"
author: "Yifei Deng"
date: "November 24th, 2017"
output: 
  html_document:
    code_folding: hide
    latex_engine: xelatex
    fig_height: 3
    fig_width: 5
---
<!-- Don't edit in between this line and the one below -->
```{r include=FALSE}
# Don't delete this chunk if you are using the DataComputing package
library(DataComputing)
library(rvest)
library(lubridate)
library(mosaicData)
library(mosaic)
library(tidyr)
library(readr)
```
*Source file* 
```{r, results='asis', echo=FALSE}
includeSourceDocuments()
```
<!-- Don't edit the material above this line -->
###About the Data Set

####Reason

The primary reason that I chose this climate data set is because Shenzhen is my homwtown back in China and I lived there for about nearly 20 years. And it was an incident that I found this [website](https://en.tutiempo.net/climate/ws-594930.html) from the [link](https://www.datasciencecentral.com/profiles/blogs/great-github-list-of-public-data-sets) from the final project pdf that it actually show every single years climate for Shenzhen from 1957 to 2017. Since the weather in Shenzhen is so unpredictable from my own experience, I really interested in wrangling this data set and see what I could cram out from it or at least to see some visualized data from it.

####Description

This dataset contains 15 climate attributions as well as day on 670 individual days from January 2016 to end of the October 2017 from Shenzhen, a tropical area and economic special zone in China.

####Variable Description

Variables            | Definition
---------------------|-------------------------------------------------
`Aver_temp`          | Average Temperature (\degree C)
`Max_temp`           | Maximum temperature (\degree C)
`Min_temp`           | Minimum temperature (\degree C)
`Atom_press_sea`     | Atmospheric pressure at sea level (hPa)
`Aver_hum`           | Average relative humidity (%)
`Total_rain_or_snow` | Total rainfall and / or snowmelt (mm)
`Aver_vis`           | Average visibility (Km)
`Aver_windsp`        | Average wind speed (Km/h)
`Max_sus_windsp`     | Maximum sustained wind speed (Km/h)
`Max_windsp`         | Maximum speed of wind (Km/h)
`Rain_or_dizz`       | Indica whether there was rain or drizzle (In the monthly average, the total days it rained)
`Snow`               | Indica if it snowed (In the monthly average, the total days it snowed)
`Storm`              | Indicates whether there storm (In the monthly average, Total days with thunderstorm)
`Fog`                | Indicates whether there was fog (In the monthly average, Total days with fog)

####Reference

[Raw Data](https://en.tutiempo.net/climate/ws-594930.html)

###Data Scraping Steps

**Successfully scrape raw data for climate in 2016 to 2017/10 Shenzhen from the page**

```{r}
#Get the xpath for the table (actually the same as for each month data from 2017 and 2016)
xpath <- '//*[@id="ColumnaIzquierda"]/div/div[4]/table'
```

```{r}
#for 2016

#Get the data from January------
page1 <- "https://en.tutiempo.net/climate/01-2016/ws-594930.html"

table_list1 <- 
  page1 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Jan <- table_list1[[1]]

Jan <- Jan[-c(32, 33), ]

#Get the data from February------
page2 <- "https://en.tutiempo.net/climate/02-2016/ws-594930.html"

table_list2 <- 
  page2 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Feb <- table_list2[[1]]

Feb <- Feb[-c(30, 31), ]
#Get the data from March------
page3 <- "https://en.tutiempo.net/climate/03-2016/ws-594930.html"

table_list3 <- 
  page3 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Mar <- table_list3[[1]]

Mar <- Mar[-c(32, 33), ]

#Get the data from April------
page4 <- "https://en.tutiempo.net/climate/04-2016/ws-594930.html"

table_list4 <- 
  page4 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Apr <- table_list4[[1]]

Apr <- Apr[-c(31, 32), ]
#Get the data from May------
page5 <- "https://en.tutiempo.net/climate/05-2016/ws-594930.html"

table_list5 <- 
  page5 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

May <- table_list5[[1]]

May <- May[-c(32, 33), ]
#Get the data from June------
page6 <- "https://en.tutiempo.net/climate/06-2016/ws-594930.html"

table_list6 <- 
  page6 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

June <- table_list6[[1]]

June <- June[-c(31, 32), ]
#Get the data from July------
page7 <- "https://en.tutiempo.net/climate/07-2016/ws-594930.html"

table_list7 <- 
  page7 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

July <- table_list7[[1]]

July <- July[-c(32, 33), ]
#Get the data from August------
page8 <- "https://en.tutiempo.net/climate/08-2016/ws-594930.html"

table_list8 <- 
  page8 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Aug <- table_list8[[1]]

Aug <- Aug[-c(32, 33), ]
#Get the data from September------
page9 <- "https://en.tutiempo.net/climate/09-2016/ws-594930.html"

table_list9 <- 
  page9 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Sep <- table_list9[[1]]

Sep <- Sep[-c(31, 32), ]
#Get the data from October------
page10 <- "https://en.tutiempo.net/climate/10-2016/ws-594930.html"

table_list10 <- 
  page10 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Oct <- table_list10[[1]]

Oct <- Oct[-c(32, 33), ]
#Get the data from November------
page11 <- "https://en.tutiempo.net/climate/11-2016/ws-594930.html"

table_list11 <- 
  page11 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Nov <- table_list11[[1]]

Nov <- Nov[-c(31, 32), ]
#Get the data from December------
page12 <- "https://en.tutiempo.net/climate/12-2016/ws-594930.html"

table_list12 <- 
  page12 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Dec <- table_list12[[1]]

Dec <- Dec[-c(32, 33), ]



```

```{r}
#for 2017

#Get the data from January------
page1_1 <- "https://en.tutiempo.net/climate/01-2017/ws-594930.html"

table_list1_1 <- 
  page1_1 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Jan1 <- table_list1_1[[1]]

Jan1 <- Jan1[-c(32, 33), ]

#Get the data from Februray------
page1_2 <- "https://en.tutiempo.net/climate/02-2017/ws-594930.html"

table_list1_2 <- 
  page1_2 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Feb1 <- table_list1_2[[1]]

Feb1 <- Feb1[-c(29, 30), ]


#Get the data from March------
page1_3 <- "https://en.tutiempo.net/climate/03-2017/ws-594930.html"

table_list1_3 <- 
  page1_3 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Mar1 <- table_list1_3[[1]]

Mar1 <- Mar1[-c(32, 33), ]
#Get the data from April------
page1_4 <- "https://en.tutiempo.net/climate/04-2017/ws-594930.html"

table_list1_4 <- 
  page1_4 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Apr1 <- table_list1_4[[1]]

Apr1 <- Apr1[-c(31, 32), ]
#Get the data from May------
page1_5 <- "https://en.tutiempo.net/climate/05-2017/ws-594930.html"

table_list1_5 <- 
  page1_5 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

May1 <- table_list1_5[[1]]

May1 <- May1[-c(32, 33), ]
#Get the data from June------
page1_6 <- "https://en.tutiempo.net/climate/06-2017/ws-594930.html"

table_list1_6 <- 
  page1_6 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

June1 <- table_list1_6[[1]]

June1 <- June1[-c(31, 32), ]
#Get the data from July------
page1_7 <- "https://en.tutiempo.net/climate/07-2017/ws-594930.html"

table_list1_7 <- 
  page1_7 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

July1 <- table_list1_7[[1]]

July1 <- July1[-c(32, 33), ]
#Get the data from August------
page1_8 <- "https://en.tutiempo.net/climate/08-2017/ws-594930.html"

table_list1_8 <- 
  page1_8 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Aug1 <- table_list1_8[[1]]

Aug1 <- Aug1[-c(32, 33), ]
#Get the data from September------
page1_9 <- "https://en.tutiempo.net/climate/09-2017/ws-594930.html"

table_list1_9 <- 
  page1_9 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Sep1 <- table_list1_9[[1]]

Sep1 <- Sep1[-c(31, 32), ]
#Get the data from October------
page1_10 <- "https://en.tutiempo.net/climate/10-2017/ws-594930.html"

table_list1_10 <- 
  page1_10 %>%
  read_html() %>%
  html_nodes(xpath = xpath) %>%
  html_table(fill = TRUE)

Oct1 <- table_list1_10[[1]]

Oct1 <- Oct1[-c(32, 33), ]
```

**Combine the data from 2016 to 2017/10 in Shenzhen to one whole year data set**
```{r,message=FALSE}
#Combine this 2016 and 2017 climate data for each month into one whole year data set------
Weather_ShenZhen <-
  Jan %>%
  full_join(Feb) %>%
  full_join(Mar) %>%
  full_join(Apr) %>%
  full_join(May) %>%
  full_join(June) %>%
  full_join(July) %>%
  full_join(Aug) %>%
  full_join(Sep) %>%
  full_join(Oct) %>%
  full_join(Nov) %>%
  full_join(Dec) %>%
  full_join(Jan1) %>%
  full_join(Feb1) %>%
  full_join(Mar1) %>%
  full_join(Apr1) %>%
  full_join(May1) %>%
  full_join(June1) %>%
  full_join(July1) %>%
  full_join(Aug1) %>%
  full_join(Sep1) %>%
  full_join(Oct1)


#Revise the names for the data set to its reality names------
Weather_ShenZhen <-
  Weather_ShenZhen %>%
  mutate(Date = seq(as.Date("2016/1/1"), as.Date("2017/10/31"), by = "day")) %>%
  rename(Aver_temp = "T", Max_temp = "TM", Min_temp = "Tm", Atom_press_sea = "SLP", Aver_hum = "H", Total_rain_or_snow = "PP", Aver_vis = "VV", Aver_windsp = "V", Max_sus_windsp = "VM", Max_windsp = "VG", Rain_or_driz = "RA", Snow = "SN", Storm = "TS", Fog = "FG")

Weather_ShenZhen = Weather_ShenZhen[,-c(1)]
```

**Write out the data set so that we could work on it easily without revising it**
```{r}
write.csv(Weather_ShenZhen, "~/Desktop/STAT184/Final Project/Weather_ShenZhen.csv")
```

***

###Preparation

```{r}
#Set work directory
setwd("~/Desktop/STAT184/Final Project") 

#Read in the data set we just scraped
Weather = read.csv("~/Desktop/STAT184/Final Project/Weather_ShenZhen.csv")

#Delete the first column with the order numbers and the column with the snow varaible, since Shenzhen is located in the tropical area (no snow exist)
Weather <- Weather[,-c(1)]
Weather <- Weather[,-c(12)]
```

***

###Start

```{r}
#inspect the first few obeservations of the data set
head(Weather)

#Inspect the variables by using str() and summary() command
str(Weather)
summary(Weather)
```

***
###1. Fundamental Exploratory Analysis

**Firstly, we want to know the average temperature during these two year period. And show the specific date that the temperature would exceed this average with the count of it**

```{r,warning=FALSE,message=FALSE}
#Calculate out the mean value of the temperature during the date range 
Weather %>%
  mutate(num_Aver_temp = tidyr::extract_numeric(Aver_temp)) %>%
  na.omit() %>%
  summarise(Aver_temp_two = sum(num_Aver_temp)/nrow(Weather))

#Use the threhold(i.e. mean temperature) to show the specific date that the temperature would exceed this average
Spec_date <-
  Weather %>%
  na.omit() %>%
  filter(readr::parse_number(Aver_temp) > 23.99806) %>%
  select(Date,Aver_temp)

#inspect the first few date with temperature greater than the average temperature during the two-year-period
head(Spec_date)

#show the count of the dates that have the greater temperature
nrow(Spec_date)
```

**Secondly, we want to know the most frequent weather conditons in Shenzhen**

```{r}
Weather %>%
  filter(Storm == "o") %>%
  summarise(count_storm = sum(n()))

Weather %>%
  filter(Fog == "o") %>%
  summarise(count_fog = sum(n()))

Weather %>%
  filter(Rain_or_driz == "o") %>%
  summarise(count_rain = sum(n()))
```

`Conclusion:`

From above report, we could conclude that the most frequent weather conditions is rain or drizzle in Shenzhen.

**Thirdly, we want to know 

```{r}
Weather %>%
  mutate(dayof_year = lubridate::yday(Date)) %>%
  ggplot(aes(x = dayof_year,y=Aver_hum)) +
  geom_point()

Weather %>%
   mutate(month = month(ymd(Date))) %>%
   ggplot(aes(x = month, group = Conditions)) +
   geom_bar(aes(color=Conditions,fill=Conditions),alpha=0.5)

```

**Lastly, we want to know whether the change of temperature during each day would be different under the condition of single,mixture or no weather conditions and any possible weather condition**

```{r,warning=FALSE,message=FALSE,fig.width=13,fig.height=6}
#First we will need to create a factor variable with different levels
Weather <-
  Weather %>%
  mutate(Conditions = 
           ifelse(Rain_or_driz == "o"&Storm == "o"&Fog == "o",
                  "Rain_or_driz & Storm &Fog", 
                  ifelse(Rain_or_driz == "o"& Fog == "o",
                         "Rain_or_driz & Fog",
                         ifelse(Rain_or_driz == "o"&Storm == "o",
                                "Rain_or_driz & Storm",
                                ifelse(Rain_or_driz == "o", 
                                       "Rain_or_driz",
                                       ifelse(Storm == "o",
                                              "Storm",
                                              ifelse(Fog == "o",
                                                     "Fog","-")))))))

#inspect the data set
head(Weather)

#Now,create the boxplot for each possible weather conditions
Weather %>%
  na.omit() %>%
  mutate(diff = tidyr::extract_numeric(Max_temp)-tidyr::extract_numeric(Min_temp)) %>%
  ggplot(aes(x = Conditions, y = diff)) +
  geom_boxplot() +
  xlab("Weather Conditions") +
  ylab("Temperature Change (Celsius)")

#We could then create an factor variables with 3 levels with no weather condition, single weather & mixture of weather based on the conditions variable we just created
Weather <-
  Weather %>%
  na.omit() %>%
  mutate(Single_no_Mix = 
           ifelse(Conditions == grep("-", Conditions, value = TRUE),
                  "No Weather Condition",
                  ifelse(Conditions ==grep("^[R][^&-]*$",Conditions, value = TRUE),
                         "Single",
                         ifelse(Conditions == grep("^[Fog]",Conditions, value = TRUE),
                                "Single",
                                ifelse(Conditions == grep("^[Storm]", Conditions, value = TRUE),
                                       "Single",
                                       "Mixture of Weather")))))
#inspect the data set
head(Weather)

#Now,recreate another boxplot and see the differences between no weather, single weather and mixture of Weather 
Weather %>%
  na.omit() %>%
  mutate(diff = tidyr::extract_numeric(Max_temp)-tidyr::extract_numeric(Min_temp)) %>%
  ggplot(aes(x = Single_no_Mix, y = diff)) +
  geom_boxplot() +
  xlab("Weather Conditions") +
  ylab("Temperature Change (Celsius)")
```

`Observations:`

**From the boxplot of any possible weather conditions**

* From the box plot, the change of temperature during each day would be mostly different under the condition of any possible weather conditions, except between raining or drizzle and the mixture of raining or drizzle & Fog (since they have close mean and variability). 

* In addition, since the average temperature change of raining or drizzle and mixture of raining or drizzle & Fog are nearly the same, we could also say that Fog would have small influence on the change of temperature.

**From the boxplot of no,snigle and mixture weather conditions**

* The change of temperature during each day would be different under the condition of single, mixture or no weather conditions

***

###2. Correlations Between certain variables?

####Part 1

**In this part, we want to investigate whether there is correlation between Average temperature and Atmospheric pressure at sea level in the area of Shenzhen taking into considerations single, mixture of weather or no weather conditions**

```{r,warning=FALSE,fig.width=16,fig.height=6}
Weather %>%
  ggplot(aes(x=Aver_temp,y=Atom_press_sea)) +
  geom_point(aes(shape = Conditions)) +
  facet_wrap( ~ Single_no_Mix) +
  theme(axis.text.x=element_text(angle=60,hjust=1,size=16),axis.text.y=element_text(size=16),axis.title=element_text(size=16,face="bold"))
```

`Observations`:

Based on the graphs provided above, we could conclude that there is a seemly negative correlation between the average temperature and the atmosphere pressure at the sea level in Shenzhen in any of the conditions provided. (i.e. as the average temperature increase, the atmosphere pressure at the sea level would possibly decrease in the region in Shenzhen)

####Part 2

**Next, as many people may have concerned that there was always a rumor saying that the change of temperature would have a hugly impact on the humdity from which the effects would show significances in many tropical area like Shenzhen. Thus, in this part we want to test the validity of this statement**

```{r, warning=FALSE, message=FALSE,fig.width=10,fig.height=10}
#In this part, we first define the change in temperature and next we omit the NA and then we create a plot frame and plot with difference of the temperture V.S. the average relative humidity to see the relationship.
Weather %>%
  mutate(diff = tidyr::extract_numeric(Max_temp)-tidyr::extract_numeric(Min_temp)) %>%
  na.omit() %>%
  ggplot(aes(x=diff,y=Aver_hum)) +
  geom_point() +
  theme(axis.text.x=element_text(angle=60,hjust=1,size=16),axis.text.y=element_text(size=16),axis.title=element_text(size=16,face="bold"))
```


`Conclusion`:

According to the diff V.S. Average relative humidity plot, we could conclude that the change of temperature would indeed have a hugely impact on the humidity, however, in a negative way. (i.e. as the change of the temperature increase, the average relative humidity would decrease correspondingly in Shenzhen)

***

###3. When did the humidity would Change?

```{r,fig.width=10,fig.height=10}
#The general pattern during the two-year-peroid
Weather %>%
  mutate(dayof_year = lubridate::yday(Date)) %>%
  ggplot(aes(x = dayof_year,y=Aver_hum)) +
  geom_point()

#To check whether the pattern is accurate, check the plot with the whole year
Weather %>%
  ggplot(aes(x = Date,y=Aver_hum)) +
  geom_point()

#Check!(repeated within the same pattern)
```

`Observations`:

Generally, from the plot, we could see that in Shenzhen, the relative humidity would remain constantly high from Summer to the mid of Fall(100th to 250th day of year). And during the start and end of the year, the average humidity would remain unstable which could possibly caused by the rainy season or typhoon or any other factors.

***



