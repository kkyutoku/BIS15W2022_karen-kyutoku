---
title: "Lab 6 Homework"
author: "Karen Kyutoku"
date: "23 January 2022"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv(file = "data/FAO_1950to2012_111914.csv")
```

```
## Rows: 17692 Columns: 71
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

```r
names(fisheries)
```

```
##  [1] "Country"                 "Common name"            
##  [3] "ISSCAAP group#"          "ISSCAAP taxonomic group"
##  [5] "ASFIS species#"          "ASFIS species name"     
##  [7] "FAO major fishing area"  "Measure"                
##  [9] "1950"                    "1951"                   
## [11] "1952"                    "1953"                   
## [13] "1954"                    "1955"                   
## [15] "1956"                    "1957"                   
## [17] "1958"                    "1959"                   
## [19] "1960"                    "1961"                   
## [21] "1962"                    "1963"                   
## [23] "1964"                    "1965"                   
## [25] "1966"                    "1967"                   
## [27] "1968"                    "1969"                   
## [29] "1970"                    "1971"                   
## [31] "1972"                    "1973"                   
## [33] "1974"                    "1975"                   
## [35] "1976"                    "1977"                   
## [37] "1978"                    "1979"                   
## [39] "1980"                    "1981"                   
## [41] "1982"                    "1983"                   
## [43] "1984"                    "1985"                   
## [45] "1986"                    "1987"                   
## [47] "1988"                    "1989"                   
## [49] "1990"                    "1991"                   
## [51] "1992"                    "1993"                   
## [53] "1994"                    "1995"                   
## [55] "1996"                    "1997"                   
## [57] "1998"                    "1999"                   
## [59] "2000"                    "2001"                   
## [61] "2002"                    "2003"                   
## [63] "2004"                    "2005"                   
## [65] "2006"                    "2007"                   
## [67] "2008"                    "2009"                   
## [69] "2010"                    "2011"                   
## [71] "2012"
```

```r
dim(fisheries)
```

```
## [1] 17692    71
```

```r
anyNA(fisheries)
```

```
## [1] TRUE
```

```r
summary(fisheries)
```

```
##    Country          Common name        ISSCAAP group#  ISSCAAP taxonomic group
##  Length:17692       Length:17692       Min.   :11.00   Length:17692           
##  Class :character   Class :character   1st Qu.:33.00   Class :character       
##  Mode  :character   Mode  :character   Median :36.00   Mode  :character       
##                                        Mean   :37.38                          
##                                        3rd Qu.:38.00                          
##                                        Max.   :77.00                          
##  ASFIS species#     ASFIS species name FAO major fishing area
##  Length:17692       Length:17692       Min.   :18.00         
##  Class :character   Class :character   1st Qu.:31.00         
##  Mode  :character   Mode  :character   Median :37.00         
##                                        Mean   :45.34         
##                                        3rd Qu.:57.00         
##                                        Max.   :88.00         
##    Measure              1950               1951               1952          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1953               1954               1955               1956          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1957               1958               1959               1960          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1961               1962               1963               1964          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1965               1966               1967               1968          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1969               1970               1971               1972          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1973               1974               1975               1976          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1977               1978               1979               1980          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1981               1982               1983               1984          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1985               1986               1987               1988          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1989               1990               1991               1992          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1993               1994               1995               1996          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1997               1998               1999               2000          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2001               2002               2003               2004          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2005               2006               2007               2008          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2009               2010               2011               2012          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
## 
```

2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
install.packages("janitor")
```

```
## Warning: パッケージ 'janitor' は使用中のため、インストールされません
```

```r
library("janitor")
```


```r
fisheries <- janitor::clean_names(fisheries)
fisheries
```

```
## # A tibble: 17,692 x 71
##    country common_name    isscaap_group_nu~ isscaap_taxonomic_~ asfis_species_n~
##    <chr>   <chr>                      <dbl> <chr>               <chr>           
##  1 Albania Angelsharks, ~                38 Sharks, rays, chim~ 10903XXXXX      
##  2 Albania Atlantic boni~                36 Tunas, bonitos, bi~ 1750100101      
##  3 Albania Barracudas nei                37 Miscellaneous pela~ 17710001XX      
##  4 Albania Blue and red ~                45 Shrimps, prawns     2280203101      
##  5 Albania Blue whiting(~                32 Cods, hakes, haddo~ 1480403301      
##  6 Albania Bluefish                      37 Miscellaneous pela~ 1702021301      
##  7 Albania Bogue                         33 Miscellaneous coas~ 1703926101      
##  8 Albania Caramote prawn                45 Shrimps, prawns     2280100117      
##  9 Albania Catsharks, nu~                38 Sharks, rays, chim~ 10801003XX      
## 10 Albania Common cuttle~                57 Squids, cuttlefish~ 3210200202      
## # ... with 17,682 more rows, and 66 more variables: asfis_species_name <chr>,
## #   fao_major_fishing_area <dbl>, measure <chr>, x1950 <chr>, x1951 <chr>,
## #   x1952 <chr>, x1953 <chr>, x1954 <chr>, x1955 <chr>, x1956 <chr>,
## #   x1957 <chr>, x1958 <chr>, x1959 <chr>, x1960 <chr>, x1961 <chr>,
## #   x1962 <chr>, x1963 <chr>, x1964 <chr>, x1965 <chr>, x1966 <chr>,
## #   x1967 <chr>, x1968 <chr>, x1969 <chr>, x1970 <chr>, x1971 <chr>,
## #   x1972 <chr>, x1973 <chr>, x1974 <chr>, x1975 <chr>, x1976 <chr>, ...
```

```r
fisheries$country <- as.factor(fisheries$country)
class(fisheries$country)
```

```
## [1] "factor"
```

```r
fisheries$isscaap_group_number <- as.factor(fisheries$isscaap_group_number)
class(fisheries$isscaap_group_number)
```

```
## [1] "factor"
```

```r
fisheries$asfis_species_number <- as.factor(fisheries$asfis_species_number)
class(fisheries$asfis_species_number)
```

```
## [1] "factor"
```

```r
fisheries$fao_major_fishing_area <- as.factor(fisheries$fao_major_fishing_area)
class(fisheries$fao_major_fishing_area)
```

```
## [1] "factor"
```

We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!

```r
fisheries_tidy <- fisheries %>% 
  pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
               names_to = "year",
               values_to = "catch",
               values_drop_na = TRUE) %>%  
  mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```

```r
library(tidyverse)
```

3. How many countries are represented in the data? Provide a count and list their names.

```r
fisheries_tidy %>% 
  count(country)
```

```
## # A tibble: 203 x 2
##    country                 n
##    <fct>               <int>
##  1 Albania               934
##  2 Algeria              1561
##  3 American Samoa        556
##  4 Angola               2119
##  5 Anguilla              129
##  6 Antigua and Barbuda   356
##  7 Argentina            3403
##  8 Aruba                 172
##  9 Australia            8183
## 10 Bahamas               423
## # ... with 193 more rows
```

4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
fisheries_tidy %>% 
  select(country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch)
```

```
## # A tibble: 376,771 x 6
##    country isscaap_taxonomic_group asfis_species_n~ asfis_species_n~  year catch
##    <fct>   <chr>                   <chr>            <fct>            <dbl> <dbl>
##  1 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        1995    NA
##  2 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        1996    53
##  3 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        1997    20
##  4 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        1998    31
##  5 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        1999    30
##  6 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        2000    30
##  7 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        2001    16
##  8 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        2002    79
##  9 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        2003     1
## 10 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        2004     4
## # ... with 376,761 more rows
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

```r
fisheries_tidy %>% 
  summarize(distinct_species = n_distinct(asfis_species_number))
```

```
## # A tibble: 1 x 1
##   distinct_species
##              <int>
## 1             1551
```

6. Which country had the largest overall catch in the year 2000?

```r
fisheries_tidy %>% 
  select(country, catch, year) %>% 
  filter(year==2000) %>% 
  arrange(desc(catch))
```

```
## # A tibble: 8,793 x 3
##    country                  catch  year
##    <fct>                    <dbl> <dbl>
##  1 China                     9068  2000
##  2 Peru                      5717  2000
##  3 Russian Federation        5065  2000
##  4 Viet Nam                  4945  2000
##  5 Chile                     4299  2000
##  6 China                     3288  2000
##  7 China                     2782  2000
##  8 United States of America  2438  2000
##  9 China                     1234  2000
## 10 Philippines                999  2000
## # ... with 8,783 more rows
```

7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?

```r
fisheries_tidy %>% 
  select(country, asfis_species_name, year, catch) %>% 
  filter(asfis_species_name == "Sardina pilchardus") %>%
  filter(between(year, 1990, 2000)) %>% 
  group_by(country) %>% 
  summarize(total_catch = sum(catch, na.rm=T)) %>% 
  arrange(desc(total_catch))
```

```
## # A tibble: 37 x 2
##    country               total_catch
##    <fct>                       <dbl>
##  1 Morocco                      7470
##  2 Spain                        3507
##  3 Russian Federation           1639
##  4 Ukraine                      1030
##  5 France                        966
##  6 Portugal                      818
##  7 Greece                        528
##  8 Italy                         507
##  9 Serbia and Montenegro         478
## 10 Denmark                       477
## # ... with 27 more rows
```

8. Which five countries caught the most cephalopods between 2008-2012?

```r
fisheries_tidy_focused <- fisheries_tidy%>% 
  filter(str_detect(isscaap_taxonomic_group, "Squids"))
fisheries_tidy_focused
```

```
## # A tibble: 14,532 x 10
##    country common_name       isscaap_group_nu~ isscaap_taxonom~ asfis_species_n~
##    <fct>   <chr>             <fct>             <chr>            <fct>           
##  1 Albania Common cuttlefish 57                Squids, cuttlef~ 3210200202      
##  2 Albania Common cuttlefish 57                Squids, cuttlef~ 3210200202      
##  3 Albania Common cuttlefish 57                Squids, cuttlef~ 3210200202      
##  4 Albania Common cuttlefish 57                Squids, cuttlef~ 3210200202      
##  5 Albania Common cuttlefish 57                Squids, cuttlef~ 3210200202      
##  6 Albania Common cuttlefish 57                Squids, cuttlef~ 3210200202      
##  7 Albania Common cuttlefish 57                Squids, cuttlef~ 3210200202      
##  8 Albania Common cuttlefish 57                Squids, cuttlef~ 3210200202      
##  9 Albania Common cuttlefish 57                Squids, cuttlef~ 3210200202      
## 10 Albania Common cuttlefish 57                Squids, cuttlef~ 3210200202      
## # ... with 14,522 more rows, and 5 more variables: asfis_species_name <chr>,
## #   fao_major_fishing_area <fct>, measure <chr>, year <dbl>, catch <dbl>
```


```r
fisheries_tidy_focused %>% 
  select(country, year, catch) %>%
  filter(between(year, 2008, 2012)) %>% 
  group_by(country) %>% 
  summarize(total_catch = sum(catch, na.rm=T)) %>% 
  arrange(desc(total_catch))
```

```
## # A tibble: 122 x 2
##    country                  total_catch
##    <fct>                          <dbl>
##  1 China                           8349
##  2 Korea, Republic of              3480
##  3 Peru                            3422
##  4 Japan                           3248
##  5 Chile                           2775
##  6 United States of America        2417
##  7 Indonesia                       1622
##  8 Taiwan Province of China        1394
##  9 Spain                           1147
## 10 France                          1138
## # ... with 112 more rows
```

9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)

```r
fisheries_tidy%>% 
  filter(year>=2008 & year<=2012)%>% 
  group_by(asfis_species_name) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange(desc(catch_total))
```

```
## # A tibble: 1,472 x 2
##    asfis_species_name    catch_total
##    <chr>                       <dbl>
##  1 Osteichthyes               107808
##  2 Theragra chalcogramma       41075
##  3 Engraulis ringens           35523
##  4 Katsuwonus pelamis          32153
##  5 Trichiurus lepturus         30400
##  6 Clupea harengus             28527
##  7 Thunnus albacares           20119
##  8 Scomber japonicus           14723
##  9 Gadus morhua                13253
## 10 Thunnus alalunga            12019
## # ... with 1,462 more rows
```
Theragra chalcogramma.

10. Use the data to do at least one analysis of your choice.

```r
fisheries_tidy %>% 
  filter(country =="Japan") %>% 
  group_by(asfis_species_name) %>% 
  arrange(desc(catch))
```

```
## # A tibble: 15,429 x 10
## # Groups:   asfis_species_name [217]
##    country common_name     isscaap_group_nu~ isscaap_taxonomic~ asfis_species_n~
##    <fct>   <chr>           <fct>             <chr>              <fct>           
##  1 Japan   Japanese pilch~ 35                Herrings, sardine~ 1210501301      
##  2 Japan   Alaska pollock~ 32                Cods, hakes, hadd~ 1480401601      
##  3 Japan   Japanese pilch~ 35                Herrings, sardine~ 1210501301      
##  4 Japan   Japanese pilch~ 35                Herrings, sardine~ 1210501301      
##  5 Japan   Alaska pollock~ 32                Cods, hakes, hadd~ 1480401601      
##  6 Japan   Japanese pilch~ 35                Herrings, sardine~ 1210501301      
##  7 Japan   Alaska pollock~ 32                Cods, hakes, hadd~ 1480401601      
##  8 Japan   Japanese pilch~ 35                Herrings, sardine~ 1210501301      
##  9 Japan   Japanese pilch~ 35                Herrings, sardine~ 1210501301      
## 10 Japan   Japanese pilch~ 35                Herrings, sardine~ 1210501301      
## # ... with 15,419 more rows, and 5 more variables: asfis_species_name <chr>,
## #   fao_major_fishing_area <fct>, measure <chr>, year <dbl>, catch <dbl>
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
