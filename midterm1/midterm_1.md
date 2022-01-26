---
title: "Midterm 1"
author: "Karen Kyutoku"
date: "25 January 2022"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above. You may use any resources to answer these questions (including each other), but you may not post questions to Open Stacks or external help sites. There are 15 total questions, each is worth 2 points.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

This exam is due by 12:00p on Thursday, January 27.  

## Load the tidyverse
If you plan to use any other libraries to complete this assignment then you should load them here.

```r
library(tidyverse)
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --
```

```
## v ggplot2 3.3.5     v purrr   0.3.4
## v tibble  3.1.6     v dplyr   1.0.7
## v tidyr   1.1.4     v stringr 1.4.0
## v readr   2.1.1     v forcats 0.5.1
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
#install.packages("janitor")
library("janitor")
```

```
## 
##  次のパッケージを付け加えます: 'janitor'
```

```
##  以下のオブジェクトは 'package:stats' からマスクされています: 
## 
##      chisq.test, fisher.test
```

## Questions  
Wikipedia's definition of [data science](https://en.wikipedia.org/wiki/Data_science): "Data science is an interdisciplinary field that uses scientific methods, processes, algorithms and systems to extract knowledge and insights from noisy, structured and unstructured data, and apply knowledge and actionable insights from data across a broad range of application domains."  

1. (2 points) Consider the definition of data science above. Although we are only part-way through the quarter, what specific elements of data science do you feel we have practiced? Provide at least one specific example.  

We have practiced R for data science so far. Using R, we import our data, tidy it, and transformed it into new variables. We can also calculate values in the data, such as means of a set of values. We also learned creating histograms in R to visualize our data.

2. (2 points) What is the most helpful or interesting thing you have learned so far in BIS 15L? What is something that you think needs more work or practice?  

Learning "Pipe" is helpful. It keeps codes clean and combine functions efficiently. I think I need more practice using and combining functions in pipes, including "group_by", "summarize", "filter", "select", "across", etc.

In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ElephantsMF`. These data are from Phyllis Lee, Stirling University, and are related to Lee, P., et al. (2013), "Enduring consequences of early experiences: 40-year effects on survival and success among African elephants (Loxodonta africana)," Biology Letters, 9: 20130011. [kaggle](https://www.kaggle.com/mostafaelseidy/elephantsmf).  

3. (2 points) Please load these data as a new object called `elephants`. Use the function(s) of your choice to get an idea of the structure of the data. Be sure to show the class of each variable.


```r
getwd()
```

```
## [1] "C:/Users/KAREN/Documents/GitHub/BIS15W2022_karen-kyutoku/midterm1"
```

```r
elephants <- readr::read_csv("data/ElephantsMF.csv")
```

```
## Warning in unlink(c(requestFile, responseFile)): cannot get info on 'C:/Users/
## KAREN/AppData/Local/Temp/RtmpCAFlhg/rstudio-ipc-requests-12fc3439a5e.rds',
## reason 'アクセスが拒否されました。'
```

```
## Rows: 288 Columns: 3
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (1): Sex
## dbl (2): Age, Height
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
summary(elephants)
```

```
##       Age            Height           Sex           
##  Min.   : 0.01   Min.   : 75.46   Length:288        
##  1st Qu.: 4.58   1st Qu.:160.75   Class :character  
##  Median : 9.46   Median :200.00   Mode  :character  
##  Mean   :10.97   Mean   :187.68                     
##  3rd Qu.:16.50   3rd Qu.:221.09                     
##  Max.   :32.17   Max.   :304.06
```

4. (2 points) Change the names of the variables to lower case and change the class of the variable `sex` to a factor.


```r
names(elephants)
```

```
## [1] "Age"    "Height" "Sex"
```

```r
elephants <- rename(elephants, age="Age", height="Height", sex="Sex")
names(elephants)
```

```
## [1] "age"    "height" "sex"
```

```r
elephants$sex <- as.factor(elephants$sex)
class(elephants$sex)
```

```
## [1] "factor"
```

5. (2 points) How many male and female elephants are represented in the data?


```r
elephants %>% 
  count(sex)
```

```
## # A tibble: 2 x 2
##   sex       n
##   <fct> <int>
## 1 F       150
## 2 M       138
```

6. (2 points) What is the average age all elephants in the data?


```r
mean(elephants$age)
```

```
## [1] 10.97132
```

7. (2 points) How does the average age and height of elephants compare by sex?


```r
elephants %>% 
  filter(sex=="F") %>% 
  summarize(mean_female_age=mean(age),
            mean_female_height=mean(height))
```

```
## # A tibble: 1 x 2
##   mean_female_age mean_female_height
##             <dbl>              <dbl>
## 1            12.8               190.
```

```r
elephants %>% 
  filter(sex=="M") %>% 
  summarize(mean_male_age=mean(age),
            mean_male_height=mean(height))
```

```
## # A tibble: 1 x 2
##   mean_male_age mean_male_height
##           <dbl>            <dbl>
## 1          8.95             185.
```

8. (2 points) How does the average height of elephants compare by sex for individuals over 20 years old. Include the min and max height as well as the number of individuals in the sample as part of your analysis.  


```r
elephants %>% 
  filter(sex=="F", age > 20) %>% 
  summarize(mean_height = mean(height),
            min_height = min(height),
            max_height = max(height),
            n_samples=n())
```

```
## # A tibble: 1 x 4
##   mean_height min_height max_height n_samples
##         <dbl>      <dbl>      <dbl>     <int>
## 1        232.       193.       278.        37
```

```r
elephants %>% 
  filter(sex=="M", age > 20) %>% 
  summarize(mean_height = mean(height),
            min_height = min(height),
            max_height = max(height),
            n_samples=n())
```

```
## # A tibble: 1 x 4
##   mean_height min_height max_height n_samples
##         <dbl>      <dbl>      <dbl>     <int>
## 1        270.       229.       304.        13
```

For the next series of questions, we will use data from a study on vertebrate community composition and impacts from defaunation in [Gabon, Africa](https://en.wikipedia.org/wiki/Gabon). One thing to notice is that the data include 24 separate transects. Each transect represents a path through different forest management areas.  

Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition and diversity declines along a defaunation gradient radiating from rural villages in Gabon. _Journal of Applied Ecology_. 2016. This paper, along with a description of the variables is included inside the midterm 1 folder.  

9. (2 points) Load `IvindoData_DryadVersion.csv` and use the function(s) of your choice to get an idea of the overall structure. Change the variables `HuntCat` and `LandUse` to factors.


```r
vertebrates <- readr::read_csv("data/IvindoData_DryadVersion.csv")
```

```
## Rows: 24 Columns: 26
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr  (2): HuntCat, LandUse
## dbl (24): TransectID, Distance, NumHouseholds, Veg_Rich, Veg_Stems, Veg_lian...
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
summary(vertebrates)
```

```
##    TransectID       Distance        HuntCat          NumHouseholds  
##  Min.   : 1.00   Min.   : 2.700   Length:24          Min.   :13.00  
##  1st Qu.: 5.75   1st Qu.: 5.668   Class :character   1st Qu.:24.75  
##  Median :14.50   Median : 9.720   Mode  :character   Median :29.00  
##  Mean   :13.50   Mean   :11.879                      Mean   :37.88  
##  3rd Qu.:20.25   3rd Qu.:17.683                      3rd Qu.:54.00  
##  Max.   :27.00   Max.   :26.760                      Max.   :73.00  
##    LandUse             Veg_Rich       Veg_Stems       Veg_liana     
##  Length:24          Min.   :10.88   Min.   :23.44   Min.   : 4.750  
##  Class :character   1st Qu.:13.10   1st Qu.:28.69   1st Qu.: 9.033  
##  Mode  :character   Median :14.94   Median :32.45   Median :11.940  
##                     Mean   :14.83   Mean   :32.80   Mean   :11.040  
##                     3rd Qu.:16.54   3rd Qu.:37.08   3rd Qu.:13.250  
##                     Max.   :18.75   Max.   :47.56   Max.   :16.380  
##     Veg_DBH        Veg_Canopy    Veg_Understory     RA_Apes      
##  Min.   :28.45   Min.   :2.500   Min.   :2.380   Min.   : 0.000  
##  1st Qu.:40.65   1st Qu.:3.250   1st Qu.:2.875   1st Qu.: 0.000  
##  Median :43.90   Median :3.430   Median :3.000   Median : 0.485  
##  Mean   :46.09   Mean   :3.469   Mean   :3.020   Mean   : 2.045  
##  3rd Qu.:50.58   3rd Qu.:3.750   3rd Qu.:3.167   3rd Qu.: 3.815  
##  Max.   :76.48   Max.   :4.000   Max.   :3.880   Max.   :12.930  
##     RA_Birds      RA_Elephant       RA_Monkeys      RA_Rodent    
##  Min.   :31.56   Min.   :0.0000   Min.   : 5.84   Min.   :1.060  
##  1st Qu.:52.51   1st Qu.:0.0000   1st Qu.:22.70   1st Qu.:2.047  
##  Median :57.90   Median :0.3600   Median :31.74   Median :3.230  
##  Mean   :58.64   Mean   :0.5450   Mean   :31.30   Mean   :3.278  
##  3rd Qu.:68.17   3rd Qu.:0.8925   3rd Qu.:39.88   3rd Qu.:4.093  
##  Max.   :85.03   Max.   :2.3000   Max.   :54.12   Max.   :6.310  
##   RA_Ungulate     Rich_AllSpecies Evenness_AllSpecies Diversity_AllSpecies
##  Min.   : 0.000   Min.   :15.00   Min.   :0.6680      Min.   :1.966       
##  1st Qu.: 1.232   1st Qu.:19.00   1st Qu.:0.7542      1st Qu.:2.248       
##  Median : 2.545   Median :20.00   Median :0.7760      Median :2.316       
##  Mean   : 4.166   Mean   :20.21   Mean   :0.7699      Mean   :2.310       
##  3rd Qu.: 5.157   3rd Qu.:22.00   3rd Qu.:0.8083      3rd Qu.:2.429       
##  Max.   :13.860   Max.   :24.00   Max.   :0.8330      Max.   :2.566       
##  Rich_BirdSpecies Evenness_BirdSpecies Diversity_BirdSpecies Rich_MammalSpecies
##  Min.   : 8.00    Min.   :0.5590       Min.   :1.162         Min.   : 6.000    
##  1st Qu.:10.00    1st Qu.:0.6825       1st Qu.:1.603         1st Qu.: 9.000    
##  Median :11.00    Median :0.7220       Median :1.680         Median :10.000    
##  Mean   :10.33    Mean   :0.7137       Mean   :1.661         Mean   : 9.875    
##  3rd Qu.:11.00    3rd Qu.:0.7722       3rd Qu.:1.784         3rd Qu.:11.000    
##  Max.   :13.00    Max.   :0.8240       Max.   :2.008         Max.   :12.000    
##  Evenness_MammalSpecies Diversity_MammalSpecies
##  Min.   :0.6190         Min.   :1.378          
##  1st Qu.:0.7073         1st Qu.:1.567          
##  Median :0.7390         Median :1.699          
##  Mean   :0.7477         Mean   :1.698          
##  3rd Qu.:0.7847         3rd Qu.:1.815          
##  Max.   :0.8610         Max.   :2.065
```

```r
names(vertebrates)
```

```
##  [1] "TransectID"              "Distance"               
##  [3] "HuntCat"                 "NumHouseholds"          
##  [5] "LandUse"                 "Veg_Rich"               
##  [7] "Veg_Stems"               "Veg_liana"              
##  [9] "Veg_DBH"                 "Veg_Canopy"             
## [11] "Veg_Understory"          "RA_Apes"                
## [13] "RA_Birds"                "RA_Elephant"            
## [15] "RA_Monkeys"              "RA_Rodent"              
## [17] "RA_Ungulate"             "Rich_AllSpecies"        
## [19] "Evenness_AllSpecies"     "Diversity_AllSpecies"   
## [21] "Rich_BirdSpecies"        "Evenness_BirdSpecies"   
## [23] "Diversity_BirdSpecies"   "Rich_MammalSpecies"     
## [25] "Evenness_MammalSpecies"  "Diversity_MammalSpecies"
```

```r
vertebrates <- janitor::clean_names(vertebrates)
vertebrates
```

```
## # A tibble: 24 x 26
##    transect_id distance hunt_cat num_households land_use veg_rich veg_stems
##          <dbl>    <dbl> <chr>             <dbl> <chr>       <dbl>     <dbl>
##  1           1     7.14 Moderate             54 Park         16.7      31.2
##  2           2    17.3  None                 54 Park         15.8      37.4
##  3           2    18.3  None                 29 Park         16.9      32.3
##  4           3    20.8  None                 29 Logging      12.4      29.4
##  5           4    16.0  None                 29 Park         17.1      36  
##  6           5    17.5  None                 29 Park         16.5      29.2
##  7           6    24.1  None                 29 Park         14.8      31.2
##  8           7    19.8  None                 54 Logging      13.2      32.6
##  9           8     5.78 High                 25 Neither      12.6      23.7
## 10           9     5.13 High                 73 Logging      16        27.1
## # ... with 14 more rows, and 19 more variables: veg_liana <dbl>, veg_dbh <dbl>,
## #   veg_canopy <dbl>, veg_understory <dbl>, ra_apes <dbl>, ra_birds <dbl>,
## #   ra_elephant <dbl>, ra_monkeys <dbl>, ra_rodent <dbl>, ra_ungulate <dbl>,
## #   rich_all_species <dbl>, evenness_all_species <dbl>,
## #   diversity_all_species <dbl>, rich_bird_species <dbl>,
## #   evenness_bird_species <dbl>, diversity_bird_species <dbl>,
## #   rich_mammal_species <dbl>, evenness_mammal_species <dbl>, ...
```

```r
vertebrates$hunt_cat <- as.factor(vertebrates$hunt_cat)
class(vertebrates$hunt_cat)
```

```
## [1] "factor"
```

```r
vertebrates$land_use <- as.factor(vertebrates$land_use)
class(vertebrates$land_use)
```

```
## [1] "factor"
```

10. (4 points) For the transects with high and moderate hunting intensity, how does the average diversity of birds and mammals compare?


```r
vertebrates %>% 
  filter(hunt_cat=="High"|hunt_cat=="Moderate") %>% 
  summarize(mean_bird_diversity=mean(diversity_bird_species),
            mean_mammal_diversity=mean(diversity_mammal_species))
```

```
## # A tibble: 1 x 2
##   mean_bird_diversity mean_mammal_diversity
##                 <dbl>                 <dbl>
## 1                1.64                  1.71
```

11. (4 points) One of the conclusions in the study is that the relative abundance of animals drops off the closer you get to a village. Let's try to reconstruct this (without the statistics). How does the relative abundance (RA) of apes, birds, elephants, monkeys, rodents, and ungulates compare between sites that are less than 3km from a village to sites that are greater than 25km from a village? The variable `Distance` measures the distance of the transect from the nearest village. Hint: try using the `across` operator.  


```r
vertebrates %>% 
  filter(distance<3) %>% 
  summarize(across(starts_with("ra"), mean, na.rm=T))
```

```
## # A tibble: 1 x 6
##   ra_apes ra_birds ra_elephant ra_monkeys ra_rodent ra_ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    0.12     76.6       0.145       17.3      3.90        1.87
```

```r
vertebrates %>% 
  filter(distance>25) %>% 
  summarize(across(starts_with("ra"), mean, na.rm=T))
```

```
## # A tibble: 1 x 6
##   ra_apes ra_birds ra_elephant ra_monkeys ra_rodent ra_ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    4.91     31.6           0       54.1      1.29        8.12
```

12. (4 points) Based on your interest, do one exploratory analysis on the `gabon` data of your choice. This analysis needs to include a minimum of two functions in `dplyr.`


```r
vertebrates %>% 
  filter(land_use=="Logging") %>% 
  summarize(across(starts_with("veg"), mean, na.rm=T))
```

```
## # A tibble: 1 x 6
##   veg_rich veg_stems veg_liana veg_dbh veg_canopy veg_understory
##      <dbl>     <dbl>     <dbl>   <dbl>      <dbl>          <dbl>
## 1     14.4      33.5      11.6    45.4       3.50           3.00
```

