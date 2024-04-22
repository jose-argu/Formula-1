# Formula-1


## Project Summary 

### Unveiling Insights from Formula 1 Data 

In this personal project, I delve into the captivating world of Formula 1 racing to showcase my abilities in data analytics. Through data cleaning, manipulation, and analysis in R along with visualization techniques in Tableau, I aim to uncover hidden patterns, trends, and performance insights from Formula 1 Data. 

The project encompasses a comprehensive analysis of various facets of Formula 1 racing, including lap times, race times, pit stop times, driver performances and more. Leveraging my skills in data manipulation, statistical analysis, and data visualization, I extract meaningful insights that shed light on the dynamics of Formula 1 competition.

### Key Aspects 

Key Aspects of the project include:

1. **Data Cleaning**: The data collected is cleaned to ensure accuracy and consistency, including handling missing values, removal of duplicate rows and data transformation.  
2. **Data Analysis**: Using formulas and functions, quantitative conclusions are drawn from the data in an attempt to uncover trends and patterns within the data, offering insights into driver performance and race outcomes.
3. **Visualization and Reporting**: By combining the data wrangling capablities of R with the visualization tools of Tableau, I create dynamic and informative visualization that reveal intricate patterns and trends within our clean and summarized Formula 1 Data.   


### Dataset 

* [Formula 1 World Championship (1950-2023)](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020?select=constructor_standings.csv)
> 14 CSV Files

> License: CC0: Public Domain   



## Data Processing 

### Datasets Used 

* [Constructors](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Datasets/constructors.csv)
* [Drivers](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Datasets/drivers.csv)
* [Lap Times](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Datasets/lap_times.csv)
* [Pit Stops](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Datasets/pit_stops.csv)
* [Races](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Datasets/races.csv)
* [Results](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Datasets/results.csv)


### Packages Used 

For our Analysis the following packages are used and installed in R:
* tidyr
* lubridate


```r
# instaling and loading packages

install.packages("tidyr")
install.packages("lubridate")
library(tidyr)
library(tibble)
library(dplyr)
library(purrr)
library(stringr)
library(lubridate)
```


### Data Importing 


```r
# installing datasets

circuits <- read.csv("circuits.csv")
constructor_results <-read.csv("constructor_results.csv")
constructor_standings <-read.csv("constructor_standings.csv")
constructors <- read.csv("constructors.csv")
driver_standings <- read.csv("driver_standings.csv")
drivers <- read.csv("drivers.csv")
lap_times <- read.csv("lap_times.csv")
pit_stops <- read.csv("pit_stops.csv")
qualifying_results <- read.csv("qualifying.csv")
races <- read.csv("races.csv")
results <- read.csv("results.csv")
status <- read.csv("status.csv")
```


### Data Cleaning 

```r

``` r
# checking data types

str(lap_times)
```

    ## 'data.frame':    551742 obs. of  6 variables:
    ##  $ raceId      : int  841 841 841 841 841 841 841 841 841 841 ...
    ##  $ driverId    : int  20 20 20 20 20 20 20 20 20 20 ...
    ##  $ lap         : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ position    : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ time        : chr  "1:38.109" "1:33.006" "1:32.713" "1:32.803" ...
    ##  $ milliseconds: int  98109 93006 92713 92803 92342 92605 92502 92537 93240 92572 ...
```

``` r
str(races)
```

    ## 'data.frame':    1101 obs. of  18 variables:
    ##  $ raceId     : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ year       : int  2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 ...
    ##  $ round      : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ circuitId  : int  1 2 17 3 4 6 5 9 20 11 ...
    ##  $ name       : chr  "Australian Grand Prix" "Malaysian Grand Prix" "Chinese Grand Prix" "Bahrain Grand Prix" ...
    ##  $ date       : chr  "2009-03-29" "2009-04-05" "2009-04-19" "2009-04-26" ...
    ##  $ time       : chr  "06:00:00" "09:00:00" "07:00:00" "12:00:00" ...
    ##  $ url        : chr  "http://en.wikipedia.org/wiki/2009_Australian_Grand_Prix" "http://en.wikipedia.org/wiki/2009_Malaysian_Grand_Prix" "http://en.wikipedia.org/wiki/2009_Chinese_Grand_Prix" "http://en.wikipedia.org/wiki/2009_Bahrain_Grand_Prix" ...
    ##  $ fp1_date   : chr  "\\N" "\\N" "\\N" "\\N" ...
    ##  $ fp1_time   : chr  "\\N" "\\N" "\\N" "\\N" ...
    ##  $ fp2_date   : chr  "\\N" "\\N" "\\N" "\\N" ...
    ##  $ fp2_time   : chr  "\\N" "\\N" "\\N" "\\N" ...
    ##  $ fp3_date   : chr  "\\N" "\\N" "\\N" "\\N" ...
    ##  $ fp3_time   : chr  "\\N" "\\N" "\\N" "\\N" ...
    ##  $ quali_date : chr  "\\N" "\\N" "\\N" "\\N" ...
    ##  $ quali_time : chr  "\\N" "\\N" "\\N" "\\N" ...
    ##  $ sprint_date: chr  "\\N" "\\N" "\\N" "\\N" ...
    ##  $ sprint_time: chr  "\\N" "\\N" "\\N" "\\N" ...

```


``` r
str(drivers)
```

    ## 'data.frame':    857 obs. of  9 variables:
    ##  $ driverId   : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ driverRef  : chr  "hamilton" "heidfeld" "rosberg" "alonso" ...
    ##  $ number     : chr  "44" "\\N" "6" "14" ...
    ##  $ code       : chr  "HAM" "HEI" "ROS" "ALO" ...
    ##  $ forename   : chr  "Lewis" "Nick" "Nico" "Fernando" ...
    ##  $ surname    : chr  "Hamilton" "Heidfeld" "Rosberg" "Alonso" ...
    ##  $ dob        : chr  "1985-01-07" "1977-05-10" "1985-06-27" "1981-07-29" ...
    ##  $ nationality: chr  "British" "German" "German" "Spanish" ...
    ##  $ url        : chr  "http://en.wikipedia.org/wiki/Lewis_Hamilton" "http://en.wikipedia.org/wiki/Nick_Heidfeld" "http://en.wikipedia.org/wiki/Nico_Rosberg" "http://en.wikipedia.org/wiki/Fernando_Alonso" ...

```

``` r
str(constructors)
````

    ## 'data.frame':    211 obs. of  5 variables:
    ##  $ constructorId : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ constructorRef: chr  "mclaren" "bmw_sauber" "williams" "renault" ...
    ##  $ name          : chr  "McLaren" "BMW Sauber" "Williams" "Renault" ...
    ##  $ nationality   : chr  "British" "German" "British" "French" ...
    ##  $ url           : chr  "http://en.wikipedia.org/wiki/McLaren" "http://en.wikipedia.org/wiki/BMW_Sauber" "http://en.wikipedia.org/wiki/Williams_Grand_Prix_Engineering" "http://en.wikipedia.org/wiki/Renault_in_Formula_One" ...

```

``` r
str(results)
```

    ## 'data.frame':    26080 obs. of  18 variables:
    ##  $ resultId       : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ raceId         : int  18 18 18 18 18 18 18 18 18 18 ...
    ##  $ driverId       : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ constructorId  : int  1 2 3 4 1 3 5 6 2 7 ...
    ##  $ number         : chr  "22" "3" "7" "5" ...
    ##  $ grid           : int  1 5 7 11 3 13 17 15 2 18 ...
    ##  $ position       : chr  "1" "2" "3" "4" ...
    ##  $ positionText   : chr  "1" "2" "3" "4" ...
    ##  $ positionOrder  : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ points         : num  10 8 6 5 4 3 2 1 0 0 ...
    ##  $ laps           : int  58 58 58 58 58 57 55 53 47 43 ...
    ##  $ time           : chr  "1:34:50.616" "+5.478" "+8.163" "+17.181" ...
    ##  $ milliseconds   : chr  "5690616" "5696094" "5698779" "5707797" ...
    ##  $ fastestLap     : chr  "39" "41" "41" "58" ...
    ##  $ rank           : chr  "2" "3" "5" "7" ...
    ##  $ fastestLapTime : chr  "1:27.452" "1:27.739" "1:28.090" "1:28.603" ...
    ##  $ fastestLapSpeed: chr  "218.300" "217.586" "216.719" "215.464" ...
    ##  $ statusId       : int  1 1 1 1 1 11 5 5 4 3 ...
```


```r

# changing time column to correct data type 

lap_times$posix_time <- as.POSIXct(lap_times$milliseconds / 1000, origin = "1970-01-01")

lap_times$lap_time <- format(lap_times$posix_time, format = "%H:%M:%OS3")

results$position <- as.integer(results$position)

results$milliseconds <- as.integer(results$milliseconds)

results$rank <- as.integer(results$rank)

results$fastestLapSpeed <- as.numeric(results$fastestLapSpeed)

results$posix_time <- as.POSIXct(results$milliseconds /1000, origin = "1970-01-01")

results$race_time <- format(results$posix_time, format = "%H:%M:%OS3")
```

```r
#removing unnecessary columns

lap_times <- subset(lap_times, select = -posix_time)

lap_times <- subset(lap_times, select = -time)

results <- subset(results, select = -posix_time)

results <- subset(results, select = -time)
```

```r

#renaming columns 

colnames(drivers)[colnames(drivers) == "url"] <- "driver_url"
colnames(lap_times)[colnames(lap_times) == "milliseconds"] <- "lap_milliseconds"
colnames(races)[colnames(races) == "name"] <- "circuit_name"
colnames(races)[colnames(races) == "time"] <- "time_of_race"
colnames(races)[colnames(races) == "url"] <- "race_url"
colnames(results)[colnames(results) == "milliseconds"] <- "race_milliseconds"
colnames(results)[colnames(results) == "rank"] <- "fastest_lap_rank"
colnames(constructors)[colnames(constructors) == "name"] <- "constructors_name"
colnames(constructors)[colnames(constructors) == "nationality"] <- "constructors_nationality"
colnames(pit_stops)[colnames(pit_stops) == "milliseconds"] <- "pit_stop_milliseconds"

```

## Data Analysis 

### Lap Times 

We begin our analysis by looking at our lap time data to form conclusions about how the average lap time and the fastest lap time have evolved on the race circuits over time. 
* Datasets used: lap_times, races, drivers.

* For our fastest laps data we are limited to data collected between 1996 - 2023. 

``` r
# creating lap_times_and_info table by joining lap_times, races, and drivers tables 

Lap_times_and_info <- left_join(lap_times, races, by = "raceId")

Lap_times_and_info <- left_join(Lap_times_and_info, drivers, by = "driverId")

Lap_times_and_info <- transform(Lap_times_and_info, driver_name = paste(forename, surname, sep = " "))

Lap_times_and_info <- Lap_times_and_info %>% 
  select("circuit_name", "year", "lap", "lap_time", "lap_milliseconds", "driver_name") %>% 
  arrange(year, circuit_name)

# Lap_times_and_info table used to create visualization on tableau
```

```r
head(Lap_times_and_info)


    ##           circuit_name year lap     lap_time lap_milliseconds
    ## 1 Argentine Grand Prix 1996   1 00:01:35.712            95713
    ## 2 Argentine Grand Prix 1996   2 00:01:33.247            93247
    ## 3 Argentine Grand Prix 1996   3 00:01:32.477            92478
    ## 4 Argentine Grand Prix 1996   4 00:01:31.819            91819
    ## 5 Argentine Grand Prix 1996   5 00:01:31.816            91817
    ## 6 Argentine Grand Prix 1996   6 00:01:31.936            91936
    ##          driver_name
    ## 1 Michael Schumacher
    ## 2 Michael Schumacher
    ## 3 Michael Schumacher
    ## 4 Michael Schumacher
    ## 5 Michael Schumacher
    ## 6 Michael Schumacher

```

``` r
Lap_times_summarizred <- Lap_times_and_info %>% 
  group_by(circuit_name, year) %>% 
  summarise(avg_lap_time_milliseconds = mean(lap_milliseconds), fastest_lap_time = min(lap_milliseconds), slowest_lap_time = max(lap_milliseconds))
  

    ## `summarise()` has grouped output by 'circuit_name'. You can override using the
    ## `.groups` argument.
```

``` r
head(Lap_times_summarizred)


    ## # A tibble: 6 × 5
    ## # Groups:   circuit_name [2]
    ##   circuit_name     year avg_lap_time_millise…¹ fastest_lap_time slowest_lap_time
    ##   <chr>           <int>                  <dbl>            <int>            <int>
    ## 1 70th Anniversa…  2020                 93384.            88451           119345
    ## 2 Abu Dhabi Gran…  2009                103623.           100279           132915
    ## 3 Abu Dhabi Gran…  2010                110506.           101274           166921
    ## 4 Abu Dhabi Gran…  2011                108615.           102612           174331
    ## 5 Abu Dhabi Gran…  2012                116404.           103964           169694
    ## 6 Abu Dhabi Gran…  2013                108938.           103434           139089
    ## # ℹ abbreviated name: ¹​avg_lap_time_milliseconds

```

Using the cleaned lap time data we create our visualizations. For an interactive dashboard click [here](https://public.tableau.com/app/profile/jose.argueta7119/viz/F1-LapTimes/FastestLapTimeOvertheYearsbyCircuit).   


![Average Lap Time Over the Years by Circuit](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Analysis%20Visualizations/Avg%20Lap%20Times%20Over%20the%20Years%20by%20Circuit.png) 


![Fastest Lap Time Over the Years by Circuit](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Analysis%20Visualizations/Fastest%20Lap%20Time%20Over%20the%20Years%20by%20Circuit.png) 


### Race Times

Similar to our lap time data, we sort and filter through our race time data to form conclusions about how the average race time and the fastest race times on race circuits have evolved over time.
* Datasets used: results, races. 

``` r
# creating new data frame without N/A values 

results_and_circuits <- results %>% 
  na.omit(results[!is.na(results$race_milliseconds), ])


results_and_circuits <- left_join(results_and_circuits, races, by = "raceId")


race_times_and_circuits <- results_and_circuits %>% 
  select("circuit_name", "year", "race_milliseconds", "race_time", "raceId") %>% 
  arrange(year, circuit_name)


# race_times_and_circuits used to create visualizations on Tabeleau 
```

``` r
# creating summarized race time table 

race_times_summarized <- race_times_and_circuits %>% 
  group_by(circuit_name, year) %>%
  summarise(avg_race_time_milliseconds = mean(race_milliseconds), fastest_race_time_milliseconds = min(race_milliseconds), slowest_race_time_milliseconds = max(race_milliseconds)) %>% 
  arrange(year, circuit_name)


    ## `summarise()` has grouped output by 'circuit_name'. You can override using the
    ## `.groups` argument.
```


``` r
head(race_times_summarized)


    ## # A tibble: 6 × 5
    ## # Groups:   circuit_name [6]
    ##   circuit_name           year avg_race_time_milliseconds fastest_race_time_mil…¹
    ##   <chr>                 <int>                      <dbl>                   <int>
    ## 1 Australian Grand Prix  2004                   5097063.                 5055757
    ## 2 Bahrain Grand Prix     2004                   5346881.                 5314875
    ## 3 Belgian Grand Prix     2004                   5567219.                 5555274
    ## 4 Brazilian Grand Prix   2004                   5320384.                 5281451
    ## 5 British Grand Prix     2004                   5099471.                 5082700
    ## 6 Canadian Grand Prix    2004                   5313309.                 5304803
    ## # ℹ abbreviated name: ¹​fastest_race_time_milliseconds
    ## # ℹ 1 more variable: slowest_race_time_milliseconds <int>

```

With our [race times and circuits](https://github.com/jose-argu/Formula-1/blob/03ee4c2ef88e13728906f1fde1d5528be08b16f4/F1%20Analysis%20Visualizations%20Datasets/race_times_and_circuits.csv) data we create the visualizations below. For an interactive dashboard click [here](https://public.tableau.com/app/profile/jose.argueta7119/viz/F1-RaceTimes/AverageRaceTimeOvertheYearsbyCircuit).

![Average Race Time Over the Years by Circuit](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Analysis%20Visualizations/Average%20Race%20Time%20Over%20the%20Years%20by%20Circuit.png) 

![Fastest Race Time Over the Years by Circuit](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Analysis%20Visualizations/Fastest%20Race%20Time%20Over%20the%20Years%20by%20Circuit.png) 


### Pit Stops

The rules and regulations of pit stops have also changed throughout the years, for this reason we take a closer look at the pit stop data to see if we can form any kind of conclusions. 
* Datasets used: pit_stops, races, drivers.

``` r
# joining tables 

pit_stops_and_info <- left_join(pit_stops, races, by = "raceId")

pit_stops_and_info <- left_join(pit_stops_and_info, drivers, by = "driverId")

pit_stops_and_info <- transform(pit_stops_and_info, driver_name = paste(forename, surname, sep = " "))


# filtering through rows 

pit_stops_and_info <- pit_stops_and_info %>% 
  select("circuit_name", "year", "duration", "pit_stop_milliseconds", "driver_name") %>% 
  arrange(year, circuit_name)

# pit_stops_and_info used for Tableau Visualisations
```

``` r

pit_stops_summarized <- pit_stops_and_info %>% 
  group_by(circuit_name, year) %>% 
  summarise(avg_pit_stop_ms = mean(pit_stop_milliseconds), fastest_pit_stop = min(pit_stop_milliseconds), slowest_pit_stop = max(pit_stop_milliseconds)) %>% 
  arrange(year, circuit_name)

    ## `summarise()` has grouped output by 'circuit_name'. You can override using the
    ## `.groups` argument.

```


``` r
head(pit_stops_summarized)


    ## # A tibble: 6 × 5
    ## # Groups:   circuit_name [6]
    ##   circuit_name           year avg_pit_stop_ms fastest_pit_stop slowest_pit_stop
    ##   <chr>                 <int>           <dbl>            <int>            <int>
    ## 1 Abu Dhabi Grand Prix   2011          21073.            12897            43574
    ## 2 Australian Grand Prix  2011          24343.            16867            37856
    ## 3 Belgian Grand Prix     2011          22746.            13914            47753
    ## 4 Brazilian Grand Prix   2011          21676.            14029            25481
    ## 5 British Grand Prix     2011          25964.            23137            45291
    ## 6 Canadian Grand Prix    2011          25267.            14501            51684

```

The [pit stops and info](https://github.com/jose-argu/Formula-1/blob/03ee4c2ef88e13728906f1fde1d5528be08b16f4/F1%20Analysis%20Visualizations%20Datasets/pit_stops_and_info.csv) data allows us to create the following visualizations. For an interactive dashboard click [here](https://public.tableau.com/app/profile/jose.argueta7119/viz/F1-PitStops_17137513494370/FastestPitStopsOvertheYearsbyCircuit).

![Average Pit Stop Over the Years by Circuit](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Analysis%20Visualizations/Average%20Pit%20Stop%20Duration%20Over%20the%20Years%20by%20Circuit.png) 

![Fastest Pit Stop Over the Years by Circuit](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Analysis%20Visualizations/Fastest%20Pit%20Stops%20Over%20the%20Years%20by%20Circuit.png) 


### Driver and Constructor Race Wins and Fastest Laps 

In the 70+ years of Formula 1 there has been a lot of drivers and teams who have won. We use our results data to look into two metrics; most races won and most fastest laps both by driver and constructors. 

* For our fastest laps data we are limited to data collected between 1996 - 2023.
* Datasets used: results, drivers, races, constructors. 

``` r
results_drivers_constructors_circuits <- left_join(results, drivers, by = "driverId")

results_drivers_constructors_circuits <- left_join(results_drivers_constructors_circuits, races, by = "raceId")

results_drivers_constructors_circuits <- left_join(results_drivers_constructors_circuits, constructors, by = "constructorId")

results_drivers_constructors_circuits <- transform(results_drivers_constructors_circuits, driver_name = paste(forename, surname, sep = " "))

results_drivers_constructors_circuits <- results_drivers_constructors_circuits %>% 
  select("circuit_name", "year", "position", "driver_name", "constructors_name", "race_time", "race_milliseconds", "fastestLapSpeed", "fastestLapTime", "fastest_lap_rank")
```

``` r

race_wins <- results_drivers_constructors_circuits %>% 
  filter(position == 1) %>% 
  arrange(year, circuit_name)

head(race_wins)
```

    ##         circuit_name year position     driver_name constructors_name
    ## 1 Belgian Grand Prix 1950        1     Juan Fangio        Alfa Romeo
    ## 2 British Grand Prix 1950        1     Nino Farina        Alfa Romeo
    ## 3  French Grand Prix 1950        1     Juan Fangio        Alfa Romeo
    ## 4   Indianapolis 500 1950        1 Johnnie Parsons      Kurtis Kraft
    ## 5 Italian Grand Prix 1950        1     Nino Farina        Alfa Romeo
    ## 6  Monaco Grand Prix 1950        1     Juan Fangio        Alfa Romeo
    ##      race_time race_milliseconds fastestLapSpeed fastestLapTime
    ## 1 02:47:26.000          10046000              NA            \\N
    ## 2 02:13:23.600           8003600              NA            \\N
    ## 3 02:57:52.799          10672800              NA            \\N
    ## 4 02:46:55.969          10015970              NA            \\N
    ## 5 02:51:17.399          10277400              NA            \\N
    ## 6 03:13:18.700          11598700              NA            \\N
    ##   fastest_lap_rank
    ## 1               NA
    ## 2               NA
    ## 3               NA
    ## 4               NA
    ## 5               NA
    ## 6               NA

``` r
fastest_laps <- results_drivers_constructors_circuits %>% 
  filter(fastest_lap_rank == 1) %>% 
  arrange(year, circuit_name)

head(fastest_laps)
```

    ##            circuit_name year position        driver_name constructors_name
    ## 1 Australian Grand Prix 2004        1 Michael Schumacher           Ferrari
    ## 2    Bahrain Grand Prix 2004        1 Michael Schumacher           Ferrari
    ## 3    Belgian Grand Prix 2004        1     Kimi Räikkönen           McLaren
    ## 4  Brazilian Grand Prix 2004        1 Juan Pablo Montoya          Williams
    ## 5    British Grand Prix 2004        1 Michael Schumacher           Ferrari
    ## 6   Canadian Grand Prix 2004        2 Rubens Barrichello           Ferrari
    ##      race_time race_milliseconds fastestLapSpeed fastestLapTime
    ## 1 01:24:15.756           5055757         226.933       1:24.125
    ## 2 01:28:34.875           5314875         216.074       1:30.252
    ## 3 01:32:35.274           5555274         238.931       1:45.108
    ## 4 01:28:01.451           5281451         217.038       1:11.473
    ## 5 01:24:42.699           5082700         235.049       1:18.739
    ## 6 01:28:29.911           5309911         213.246       1:13.622
    ##   fastest_lap_rank
    ## 1                1
    ## 2                1
    ## 3                1
    ## 4                1
    ## 5                1
    ## 6                1

``` r
driver_stats <- results_drivers_constructors_circuits %>% 
  group_by(driver_name) %>% 
  summarise(race_wins = sum(position == 1, na.rm = TRUE), fastest_laps = sum(fastest_lap_rank == 1, na.rm = TRUE),) %>% 
  arrange(-race_wins, -fastest_laps)

# driver_stats table used to create visualizations on Tableau

head(driver_stats)
```

    ## # A tibble: 6 × 3
    ##   driver_name        race_wins fastest_laps
    ##   <chr>                  <int>        <int>
    ## 1 Lewis Hamilton           103           63
    ## 2 Michael Schumacher        91           21
    ## 3 Sebastian Vettel          53           38
    ## 4 Alain Prost               51            0
    ## 5 Max Verstappen            45           27
    ## 6 Ayrton Senna              41            0


Using our [driver stats](https://github.com/jose-argu/Formula-1/blob/03ee4c2ef88e13728906f1fde1d5528be08b16f4/F1%20Analysis%20Visualizations%20Datasets/driver_stats.csv) data we create the following visualizations. For an interactive dashboard click [here](https://public.tableau.com/app/profile/jose.argueta7119/viz/F1-Drivers_17137515219620/DriverRaceWins).



![Driver Race Wins](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Analysis%20Visualizations/Driver%20Race%20Wins.png)


![Driver Fastest Laps](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Analysis%20Visualizations/Driver%20Fastest%20Laps.png)




``` r
constructor_stats <- results_drivers_constructors_circuits %>% 
  group_by(constructors_name) %>% 
  summarise(race_wins = sum(position == 1, na.rm = TRUE), fastest_laps = sum(fastest_lap_rank == 1, na.rm = TRUE)) %>% 
  arrange(-race_wins, -fastest_laps)

# constructor_stats used to create visualizations on Tableau 

head(constructor_stats)
```

    ## # A tibble: 6 × 3
    ##   constructors_name race_wins fastest_laps
    ##   <chr>                 <int>        <int>
    ## 1 Ferrari                 243           92
    ## 2 McLaren                 179           50
    ## 3 Mercedes                125           94
    ## 4 Williams                114            7
    ## 5 Red Bull                104           92
    ## 6 Team Lotus               45            0


The [constructor stats](https://github.com/jose-argu/Formula-1/blob/03ee4c2ef88e13728906f1fde1d5528be08b16f4/F1%20Analysis%20Visualizations%20Datasets/constructor_stats.csv) data allows us to create the visualizations below. For an interactive dashboard click [here](https://public.tableau.com/app/profile/jose.argueta7119/viz/F1-Constructors_17137562550130/ConstructorsRaceWins#1).


![Constructor Race Wins](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Analysis%20Visualizations/Constructors%20Race%20Wins.png)

![Constructor Fastest Laps](https://github.com/jose-argu/Formula-1/blob/106fe6b3437c3ed50fb7dd00907db46c497e676e/F1%20Analysis%20Visualizations/Constructors%20Fastest%20Laps.png)



## Results 


### Lap Times


After our analysis of our data, we now attempt to draw results beginning with the lap time data. 


``` r
most_recent_lap_times <- Lap_times_and_info %>% 
  group_by(circuit_name) %>% 
  filter(year == max(year))


oldest_lap_times <- Lap_times_and_info %>% 
  group_by(circuit_name) %>% 
  filter(year == min(year))


most_recent_lap_times <- most_recent_lap_times %>% 
  select("circuit_name", "year", "lap_time", "lap_milliseconds")

oldest_lap_times <- oldest_lap_times %>% 
  select("circuit_name", "year", "lap_time", "lap_milliseconds")


colnames(most_recent_lap_times)[colnames(most_recent_lap_times) == "year"] <- "MR_year"
colnames(most_recent_lap_times)[colnames(most_recent_lap_times) == "lap_time"] <- "MR_lap_time"
colnames(most_recent_lap_times)[colnames(most_recent_lap_times) == "lap_milliseconds"] <- "MR_lap_milliseconds"

colnames(oldest_lap_times)[colnames(oldest_lap_times) == "year"] <- "oldest_year"
colnames(oldest_lap_times)[colnames(oldest_lap_times) == "lap_time"] <- "oldest_lap_time"
colnames(oldest_lap_times)[colnames(oldest_lap_times) == "lap_milliseconds"] <- "oldest_lap_milliseconds"



MR_average_lap_times <- most_recent_lap_times %>% 
  group_by(circuit_name, MR_year) %>% 
  summarise(MR_avg_lap_time = mean(MR_lap_milliseconds))
```

    ## `summarise()` has grouped output by 'circuit_name'. You can override using the
    ## `.groups` argument.

``` r
oldest_average_lap_times <- oldest_lap_times %>% 
  group_by(circuit_name, oldest_year) %>% 
  summarise(oldest_average_lap_time = mean(oldest_lap_milliseconds))
```

    ## `summarise()` has grouped output by 'circuit_name'. You can override using the
    ## `.groups` argument.

``` r
MR_fastest_lap_time <- most_recent_lap_times %>% 
  group_by(circuit_name, MR_year) %>% 
  summarise(MR_fastest_lap_time = min(MR_lap_milliseconds))
```

    ## `summarise()` has grouped output by 'circuit_name'. You can override using the
    ## `.groups` argument.

``` r
oldest_fastest_lap_time <-oldest_lap_times %>% 
  group_by(circuit_name, oldest_year) %>% 
  summarise(oldest_fastest_lap_time = min(oldest_lap_milliseconds))
```

    ## `summarise()` has grouped output by 'circuit_name'. You can override using the
    ## `.groups` argument.

``` r
average_lap_time_difference <- left_join(MR_average_lap_times, oldest_average_lap_times, by = "circuit_name")

# average_lap_time_difference used for visualizations

head(average_lap_time_difference)
```

    ## # A tibble: 6 × 5
    ## # Groups:   circuit_name [6]
    ##   circuit_name        MR_year MR_avg_lap_time oldest_year oldest_average_lap_t…¹
    ##   <chr>                 <int>           <dbl>       <int>                  <dbl>
    ## 1 70th Anniversary G…    2020          93384.        2020                 93384.
    ## 2 Abu Dhabi Grand Pr…    2022          92205.        2009                103623.
    ## 3 Argentine Grand Pr…    1998          92766.        1996                 98447.
    ## 4 Australian Grand P…    2023         147649.        1996                 99021.
    ## 5 Austrian Grand Prix    2023          73294.        1997                 74986.
    ## 6 Azerbaijan Grand P…    2023         110503.        2017                149325.
    ## # ℹ abbreviated name: ¹​oldest_average_lap_time

``` r
fastest_lap_time_difference <- left_join(MR_fastest_lap_time, oldest_fastest_lap_time, by = "circuit_name")


# fastest_lap_time_difference used for visualizations

head(fastest_lap_time_difference)
```

    ## # A tibble: 6 × 5
    ## # Groups:   circuit_name [6]
    ##   circuit_name    MR_year MR_fastest_lap_time oldest_year oldest_fastest_lap_t…¹
    ##   <chr>             <int>               <int>       <int>                  <int>
    ## 1 70th Anniversa…    2020               88451        2020                  88451
    ## 2 Abu Dhabi Gran…    2022               88391        2009                 100279
    ## 3 Argentine Gran…    1998               88179        1996                  89413
    ## 4 Australian Gra…    2023               80235        1996                  93421
    ## 5 Austrian Grand…    2023               67012        1997                  71814
    ## 6 Azerbaijan Gra…    2023              103370        2017                 103441
    ## # ℹ abbreviated name: ¹​oldest_fastest_lap_time


Using the [average lap time difference](https://github.com/jose-argu/Formula-1/blob/3e3a886e7b72ab7345b8b2fd08cb7a577af55caa/F1%20Results%20Visualization%20Datasets/average_lap_time_difference.csv) and our [fastest lap time difference](https://github.com/jose-argu/Formula-1/blob/3e3a886e7b72ab7345b8b2fd08cb7a577af55caa/F1%20Results%20Visualization%20Datasets/fastest_lap_time_difference.csv) data, we create our visualizations and draw our conclusions. For an interactive dashboard click [average lap time difference](https://public.tableau.com/app/profile/jose.argueta7119/viz/AverageLapTimeDifferencefromMostRecentRacetoOldestRace/AverageLapTimeDifference) or [fastest lap time difference](https://public.tableau.com/app/profile/jose.argueta7119/viz/FastestLapTimeDifferencefromMostRecentRacetoOldestRace/FastestLapTimeDifference).


![Average Lap Time Difference From Most Recent Race to Oldest Race](https://github.com/jose-argu/Formula-1/blob/3e3a886e7b72ab7345b8b2fd08cb7a577af55caa/F1%20Results%20Visualizations/Average%20Lap%20Time%20Difference.png)

21 of 42 Grand Prix appear to have gotten quicker. The three races that have improved the most in average lap time are the:

* Korean Grand Prix
* Saudi Arabian Grand Prix
* Azerbaijan Grand Prix


![Fastest Lap Time Difference From Most Recent Race to Oldest Race](https://github.com/jose-argu/Formula-1/blob/3e3a886e7b72ab7345b8b2fd08cb7a577af55caa/F1%20Results%20Visualizations/Fastest%20Lap%20Time%20Difference.png)


15 of 42 Grand Prix appear to have gotten slower. The three circuits with laps that appear to have gotten slowest over time are the:

* Australian Grand Prix
* United States Grand Prix
* European Grand Prix 




### Race Times

Next, we want to see the time difference between the most recent race time and the oldest recorded race time. 

``` r
MR_race_times <- race_times_summarized %>% 
  group_by(circuit_name) %>% 
  filter(year == max(year))


oldest_race_times <- race_times_summarized %>% 
  group_by(circuit_name) %>% 
  filter(year == min(year))


colnames(MR_race_times)[colnames(MR_race_times) == "year"] <- "MR_year"
colnames(MR_race_times)[colnames(MR_race_times) == "avg_race_time_milliseconds"] <- "MR_avg_race_time_milliseconds"
colnames(MR_race_times)[colnames(MR_race_times) == "fastest_race_time_milliseconds"] <- "MR_fastest_race_time_milliseconds"
colnames(MR_race_times)[colnames(MR_race_times) == "slowest_race_time_milliseconds"] <- "MR_slowest_race_time_milliseconds"

colnames(oldest_race_times)[colnames(oldest_race_times) == "year"] <- "oldest_year"
colnames(oldest_race_times)[colnames(oldest_race_times) == "avg_race_time_milliseconds"] <- "oldest_avg_race_time_milliseconds"
colnames(oldest_race_times)[colnames(oldest_race_times) == "fastest_race_time_milliseconds"] <- "oldest_fastest_race_time_milliseconds"
colnames(oldest_race_times)[colnames(oldest_race_times) == "slowest_race_time_milliseconds"] <- "oldest_slowest_race_time_milliseconds"


race_time_differences <- left_join(MR_race_times, oldest_race_times, by = "circuit_name")


# race_time_differences used for visualizations
```

To create the following visualization we use the [race time differences](https://github.com/jose-argu/Formula-1/blob/3e3a886e7b72ab7345b8b2fd08cb7a577af55caa/F1%20Results%20Visualization%20Datasets/race_time_differences.csv) data. For an interactive dashboard click [here](https://public.tableau.com/app/profile/jose.argueta7119/viz/RaceTimeDifferencesfromMostRecentRacetoOldestRace/AverageRaceTimeDifferencesFromMostRecenttoOldestRace).


![Average Race Time Difference from Most Recent Race to Oldest Race](https://github.com/jose-argu/Formula-1/blob/3e3a886e7b72ab7345b8b2fd08cb7a577af55caa/F1%20Results%20Visualizations/Average%20Race%20Time%20Differences%20From%20Most%20Recent%20to%20Oldest%20Race.png)

13 of 40 races appear to have gotten quicker with a negative delta average race time difference. The 3 races that have gotten the quickest are the:

* Korean Grand Prix
* Saudi Arabian Grand Prix
* Azerbaijan Grand Prix


21 of 40 races have gotten slower from the oldest race to the most recent race, with the top 3 slowest average race time difference being: 

* Japanese Grand Prix
* Australian Grand Prix
* German Grand Prix 


![Fastest Race Time Difference from Most Recent Race to Oldest Race](https://github.com/jose-argu/Formula-1/blob/3e3a886e7b72ab7345b8b2fd08cb7a577af55caa/F1%20Results%20Visualizations/Fastest%20Race%20Tine%20Differences%20From%20Most%20Recent%20Race%20to%20Oldest%20Race.png)


13 of 40 races have seen the fastest race time improve from the oldest race to the most recent race. 


21 of 40 races have see the fastest race time get slower from the oldest race to the most recent race.  




### Pit Stops

We measure the change in duration of pitstops over time by circuit. 

``` r
oldest_pit_stops <- pit_stops_and_info %>% 
  group_by(circuit_name) %>% 
  filter(year == min(year))


MR_pit_stop <- pit_stops_and_info %>% 
  group_by(circuit_name) %>% 
  filter(year == max(year))
  


colnames(oldest_pit_stops)[colnames(oldest_pit_stops) == "year"] <- "oldest_year"
colnames(oldest_pit_stops)[colnames(oldest_pit_stops) == "duration"] <- "oldest_duration"
colnames(oldest_pit_stops)[colnames(oldest_pit_stops) == "pit_stop_milliseconds"] <- "oldest_pit_stop_milliseconds"

colnames(MR_pit_stop)[colnames(MR_pit_stop) == "year"] <- "MR_year"
colnames(MR_pit_stop)[colnames(MR_pit_stop) == "duration"] <- "MR_duration"
colnames(MR_pit_stop)[colnames(MR_pit_stop) == "pit_stop_milliseconds"] <- "MR_pit_stop_milliseconds"



oldest_pit_stop_info <- oldest_pit_stops %>% 
  group_by(circuit_name, oldest_year) %>% 
  summarise(oldest_avg_pit_stop_duration_ms = mean(oldest_pit_stop_milliseconds), oldest_fastest_pit_stop_duration_ms = min(oldest_pit_stop_milliseconds))
```

    ## `summarise()` has grouped output by 'circuit_name'. You can override using the
    ## `.groups` argument.

``` r
MR_pit_stop_info <- MR_pit_stop %>% 
  group_by(circuit_name, MR_year) %>% 
  summarise(MR_avg_pit_stop_duration_ms = mean(MR_pit_stop_milliseconds), MR_fastest_pit_stop_duration = min(MR_pit_stop_milliseconds))
```

    ## `summarise()` has grouped output by 'circuit_name'. You can override using the
    ## `.groups` argument.

``` r
pit_stop_duration_difference <- left_join(MR_pit_stop_info, oldest_pit_stop_info, by = "circuit_name")


# pit_stop_duration_difference used for visualizations
```

Our [pit stop duration difference](https://github.com/jose-argu/Formula-1/blob/3e3a886e7b72ab7345b8b2fd08cb7a577af55caa/F1%20Results%20Visualization%20Datasets/pit_stop_duration_difference.csv) data creates the following visualizations. For an interactive dashboard click [here](https://public.tableau.com/app/profile/jose.argueta7119/viz/PitStopDurationDifferenceFromMostRecentRacetoOldestRace/AveragePitStopDurationFromMostRecentRacetoOldestRace#1).


![Average Pit Stop Duration Difference from Most Recent Race to Oldest Race](https://github.com/jose-argu/Formula-1/blob/3e3a886e7b72ab7345b8b2fd08cb7a577af55caa/F1%20Results%20Visualizations/Average%20Pit%20Stop%20Duration%20From%20Most%20Recent%20Race%20to%20Oldest%20Race.png)

For the most part, the average pit stop duration time is very similar among all circuits except for the following, which may indicate an accident at the most recent grand prix or at the oldest grand prix for that circuit:

* Australian Grand Prix
* Japanese Grand Prix
* French Grand Prix
* Italian Grand Prix
* Azerbaijan Grand Prix
* Saudi Arabian Grand Prix


![Fastest Pit Stop Duration Difference from Most Recent Race to Oldest Race](https://github.com/jose-argu/Formula-1/blob/3e3a886e7b72ab7345b8b2fd08cb7a577af55caa/F1%20Results%20Visualizations/Fastest%20Pit%20Stop%20Duration%20From%20Most%20Recent%20Race%20to%20Oldest%20Race.png)




The biggest surprise might be the fastest pit stop duration time from the oldest grand prix to the most recent grand prix, as an overwhelming amount of circuits have actually had the pit stop duration time increase rather than decrease. 

* 24 of 39 circuits have had their pit stop duration time increase.
* 9 of 30 circuits have had their pit stop duration time decrease.

