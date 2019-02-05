**Note**: At the time of writing, all the exercises herein are offered on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource. The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Data Manipulation in R with dplyr](https://www.datacamp.com/courses/dplyr-data-manipulation-r-tutorial)

# 1. Introduction to dplyr and tbls

## Load the dplyr and hflights package
```
# Load the dplyr package
library(dplyr)

# Load the hflights package
library(hflights)

# Call both head() and summary() on hflights
head(hflights)
summary(hflights)
```
## Convert data.frame to tibble
```
# Convert the hflights_df data.frame into a hflights tbl
hflights <- tbl_df(hflights_df)

# Display the hflights tbl
hflights

# Create the object carriers
carriers <- hflights$UniqueCarrier
```
## Changing labels of hflights, part 1 of 2
```
# Both the dplyr and hflights packages are loaded into workspace
lut <- c("AA" = "American", "AS" = "Alaska", "B6" = "JetBlue", "CO" = "Continental", 
         "DL" = "Delta", "OO" = "SkyWest", "UA" = "United", "US" = "US_Airways", 
         "WN" = "Southwest", "EV" = "Atlantic_Southeast", "F9" = "Frontier", 
         "FL" = "AirTran", "MQ" = "American_Eagle", "XE" = "ExpressJet", "YV" = "Mesa")

# Add the Carrier column to hflights
hflights$Carrier <- lut[hflights$UniqueCarrier]

# Glimpse at hflights
glimpse(hflights)
```
## Changing labels of hflights, part 2 of 2
```
# The lookup table
lut <- c("A" = "carrier", "B" = "weather", "C" = "FFA", "D" = "security", "E" = "not cancelled")

# Add the Code column
hflights$Code <- lut[hflights$CancellationCode]

# Glimpse at hflights
glimpse(hflights)
```


# 2. Select and mutate 

## Choosing is not losing! The select verb
```
# Print out a tbl with the four columns of hflights related to delay
select(hflights, ActualElapsedTime, AirTime, ArrDelay, DepDelay)

# Print out the columns Origin up to Cancelled of hflights
select(hflights, Origin: Cancelled)

# Answer to last question: be concise!
select(hflights, Year: DayOfWeek, ArrDelay: Diverted)
```
## Helper functions for variable selection
```
# Print out a tbl containing just ArrDelay and DepDelay
select(hflights, ArrDelay, DepDelay)

# Print out a tbl as described in the second instruction, using both helper functions and variable names
select(hflights, UniqueCarrier, ends_with("Num"), starts_with("Cancell"))

# Print out a tbl as described in the third instruction, using only helper functions.
select(hflights, ends_with("Time"), ends_with("Delay"))
```
## Comparison to base R
```
# Finish select call so that ex1d matches ex1r
ex1r <- hflights[c("TaxiIn", "TaxiOut", "Distance")]
ex1d <- select(hflights, starts_with("Taxi"), Distance)

# Finish select call so that ex2d matches ex2r
ex2r <- hflights[c("Year", "Month", "DayOfWeek", "DepTime", "ArrTime")]
ex2d <- select(hflights, Year: ArrTime, -DayofMonth)

# Finish select call so that ex3d matches ex3r
ex3r <- hflights[c("TailNum", "TaxiIn", "TaxiOut")]
ex3d <- select(hflights, starts_with("Ta"))
```
## Mutating is creating
```
# Add the new variable ActualGroundTime to a copy of hflights and save the result as g1.
g1 <- mutate(hflights, ActualGroundTime = ActualElapsedTime - AirTime)

# Add the new variable GroundTime to g1. Save the result as g2.
g2 <- mutate(g1, GroundTime = TaxiIn + TaxiOut)

# Add the new variable AverageSpeed to g2. Save the result as g3.
g3 <- mutate(g2, AverageSpeed = (60 * Distance) / AirTime)

# Print out g3
g3
```
## Add multiple variables using mutate
```
# Add a second variable loss_ratio to the dataset: m1
m1 <- mutate(hflights, loss = ArrDelay - DepDelay, loss_ratio = loss / DepDelay)

# Add the three variables as described in the third instruction: m2
m2 <- mutate(hflights, TotalTaxi = TaxiIn + TaxiOut, 
             ActualGroundTime = ActualElapsedTime - AirTime, 
             Diff = TotalTaxi - ActualGroundTime)
```


# 3. Filter and arrange 

## Logical operators
```
# All flights that traveled 3000 miles or more
filter(hflights, Distance >= 3000)

# All flights flown by one of JetBlue, Southwest, or Delta
filter(hflights, UniqueCarrier == "JetBlue" | UniqueCarrier == "Southwest" | UniqueCarrier == "Delta")

# All flights where taxiing took longer than flying
filter(hflights, (TaxiIn + TaxiOut) > AirTime)
```
## Combining tests using boolean operators
```
# All flights that departed before 5am or arrived after 10pm
filter(hflights, DepTime < 500 | ArrTime > 2200)

# All flights that departed late but arrived ahead of schedule
filter(hflights, DepDelay > 0, ArrDelay < 0)

# All flights that were cancelled after being delayed
filter(hflights, Cancelled == 1, DepDelay > 0)
```
## Blend together what you've learned!
```
# Select the flights that had JFK as their destination: c1
c1 <- filter(hflights, Dest == "JFK")

# Combine the Year, Month and DayofMonth variables to create a Date column: c2
c2 <- mutate(c1, Date = paste(Year, Month, DayofMonth, sep = "-"))

# Print out a selection of columns of c2
select(c2, Date, DepTime, ArrTime, TailNum)
```
## Arranging your data
```
# Definition of dtc
dtc <- filter(hflights, Cancelled == 1, !is.na(DepDelay))

# Arrange dtc by departure delays
arrange(dtc, DepDelay)

# Arrange dtc so that cancellation reasons are grouped
arrange(dtc, CancellationCode)

# Arrange dtc according to carrier and departure delays
arrange(dtc, UniqueCarrier, DepDelay)
```
## Reverse the order of arranging
```
# Arrange according to carrier and decreasing departure delays
arrange(hflights, UniqueCarrier, desc(DepDelay))

# Arrange flights by total delay (normal order).
arrange(hflights, ArrDelay + DepDelay)
```


# 4. Summarize and the pipe operator 

## The syntax of summarize
```
# Print out a summary with variables min_dist and max_dist
summarize(hflights, min_dist = min(Distance), max_dist = max(Distance))

# Print out a summary with variable max_div
filter(hflights, Diverted == 1) %>%
  summarize(max_div = max(Distance))
```
## Aggregate functions
```
# Remove rows that have NA ArrDelay: temp1
temp1 <- filter(hflights, ArrDelay != "NA")

# Generate summary about ArrDelay column of temp1
summarize(temp1, earliest = min(ArrDelay), average = mean(ArrDelay), latest = max(ArrDelay), sd = sd(ArrDelay))

# Keep rows that have no NA TaxiIn and no NA TaxiOut: temp2
temp2 <- filter(hflights, TaxiIn != "NA", TaxiOut != "NA")

# Print the maximum taxiing difference of temp2 with summarize()
summarize(temp2, max_taxi_diff = max(abs(TaxiIn - TaxiOut)))
```
## dplyr aggregate functions
```
# Generate summarizing statistics for hflights
summarize(hflights,
          n_obs = n(),
          n_carrier = n_distinct(UniqueCarrier),
          n_dest = n_distinct(Dest))

# All American Airline flights
aa <- filter(hflights, UniqueCarrier == "American")

# Generate summarizing statistics for aa 
summarize(aa, n_flights = n(), n_canc = sum(Cancelled), avg_delay = mean(ArrDelay, na.rm = TRUE))
```
## Overview of syntax
```
# Write the 'piped' version of the English sentences.
hflights %>%
  mutate(diff = TaxiOut - TaxiIn) %>%
  filter(diff != "NA") %>%
  summarize(avg = mean(diff))
```
## Drive or fly? Part 1 of 2
```
# Chain together mutate(), filter() and summarize()
hflights %>%
  mutate(RealTime = ActualElapsedTime + 100, mph = 60 * Distance/ RealTime) %>%
  filter(mph != "NA", mph < 70) %>%
  summarize(n_less = n(), n_dest = n_distinct(Dest), min_dist = min(Distance), max_dist = max(Distance))
```
## Drive or fly? Part 2 of 2
```
# Finish the command with a filter() and summarize() call
hflights %>%
  mutate(
    RealTime = ActualElapsedTime + 100, 
    mph = 60 * Distance / RealTime
  ) %>%
  filter(
    mph < 105 |
    Cancelled == 1 |
    Diverted == 1
  ) %>%
  summarize(
    n_non = n(),
    n_dest = n_distinct(Dest),
    min_dist = min(Distance),
    max_dist = max(Distance)
  )
```
## Advanced piping exercise
```
# Count the number of overnight flights
hflights %>%
  filter(
    DepTime != "NA",
    ArrTime != "NA",
    DepTime > ArrTime
  ) %>%
  summarize(num = n())
```


# 5. Group_by and working with databases 

## Unite and conquer using group_by
```
# Make an ordered per-carrier summary of hflights
hflights %>%
  group_by(UniqueCarrier) %>%
  summarize(
    p_canc = 100 * mean(Cancelled == 1),
    avg_delay = mean(ArrDelay, na.rm = TRUE)
  ) %>%
  arrange(avg_delay, p_canc)
```
## Combine group_by with mutate
```
# Ordered overview of average arrival delays per carrier
hflights %>%
  filter(
    ArrDelay != "NA", 
    ArrDelay > 0
  )%>%
  group_by(UniqueCarrier) %>%
  summarize(avg = mean(ArrDelay)) %>%
  mutate(rank = rank(avg)) %>%
  arrange(rank)
```
## Advanced group_by exercises
```
# How many airplanes only flew to one destination?
hflights %>%
  group_by(TailNum) %>%
  summarize(ndest = n_distinct(Dest)) %>%
  filter(ndest == 1) %>%
  summarize(nplanes = sum(ndest))

# Find the most visited destination for each carrier
hflights %>%
  group_by(UniqueCarrier, Dest) %>%
  summarize(n = n()) %>%
  mutate(rank = rank(desc(n))) %>%
  filter(rank == 1)
```
## dplyr deals with different types
```
# Use summarize to calculate n_carrier
hflights2 %>%
  summarize(n_carrier = n_distinct(UniqueCarrier))
```
## dplyr and mySQL databases
```
# Set up a connection to the mysql database
my_db <- src_mysql(dbname = "dplyr", 
                   host = "courses.csrrinzqubik.us-east-1.rds.amazonaws.com", 
                   port = 3306, 
                   user = "student",
                   password = "datacamp")

# Reference a table within that source: nycflights
nycflights <- tbl(my_db, "dplyr")

# glimpse at nycflights
glimpse(nycflights)

# Ordered, grouped summary of nycflights
nycflights %>%
  group_by(carrier) %>%
  summarize(
    n_flights = n(),
    avg_delay = mean(arr_delay)
  ) %>%
  arrange(avg_delay)
```
