**Note**: At the time of writing, all the exercises herein are offered on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource. The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Importing Data in R (Part 2)](https://www.datacamp.com/courses/importing-data-in-r-part-2)

# 1. Importing data from databases (Part 1) 

## Establish a connection
```
# Load the DBI package
library(DBI)

# Edit dbConnect() call
con <- dbConnect(RMySQL::MySQL(), 
                 dbname = "tweater", 
                 host = "courses.csrrinzqubik.us-east-1.rds.amazonaws.com", 
                 port = 3306,
                 user = "student",
                 password = "datacamp")
```
## List the database tables
```
# Build a vector of table names: tables
tables <- dbListTables(con)

# Display structure of tables
str(tables)
```
## Import users
```
# Import the users table from tweater: users
users <- dbReadTable(con, "users")

# Print users
users
```
## Import all tables
```
# Get table names
table_names <- dbListTables(con)

# Import all tables
tables <- lapply(table_names, dbReadTable, conn = con)

# Print out tables
tables
```


# 2. Importing data from databases (Part 2) 

## Query tweater (1)
```
# Import tweat_id column of comments where user_id is 1: elisabeth
elisabeth <- dbGetQuery(con, "SELECT tweat_id FROM comments WHERE user_id = '1'")

# Print elisabeth
elisabeth
```
## Query tweater (2)
```
# Import post column of tweats where date is higher than '2015-09-21': latest
latest <- dbGetQuery(con, "SELECT post FROM tweats WHERE date > '2015-09-21'")

# Print latest
latest
```
## Query tweater (3)
```
# Create data frame specific
specific <- dbGetQuery(con, "SELECT message FROM comments WHERE tweat_id = 77 AND user_id > 4")

# Print specific
specific
```
## Query tweater (4)
```
# Create data frame short
short <- dbGetQuery(con, "SELECT id, name FROM users WHERE CHAR_LENGTH(name) < 5")

# Print short
short
```
## Send - Fetch - Clear
```
# Send query to the database
res <- dbSendQuery(con, "SELECT * FROM comments WHERE user_id > 4")

# Use dbFetch() twice
dbFetch(res, n = 2)
dbFetch(res)

# Clear res
dbClearResult(res)
```
## Be polite and ...
```
# Create the data frame  long_tweats
long_tweats <- dbGetQuery(con, "SELECT post, date FROM tweats WHERE CHAR_LENGTH(post) > 40")

# Print long_tweats
print(long_tweats)

# Disconnect from the database
dbDisconnect(con)
```


# 3. Importing data from the web (Part 1) 

## Import flat files from the web
```
# Load the readr package
library(readr)

# Import the csv file: pools
url_csv <- "http://s3.amazonaws.com/assets.datacamp.com/production/course_1478/datasets/swimming_pools.csv"
pools <- read_csv(url_csv)

# Import the txt file: potatoes
url_delim <- "http://s3.amazonaws.com/assets.datacamp.com/production/course_1478/datasets/potatoes.txt"
potatoes <- read_tsv(url_delim)

# Print pools and potatoes
pools
potatoes
```
## Secure importing
```
# Import the file using read.csv(): pools1
pools1 <- read.csv(url_csv)

# Import the file using read_csv(): pools2
pools2 <- read_csv(url_csv)

# Print the structure of pools1 and pools2
str(pools1)
str(pools2)
```
## Import Excel files from the web
```
# Load the readxl and gdata package
library(readxl)
library(gdata)

# Specification of url: url_xls
url_xls <- "http://s3.amazonaws.com/assets.datacamp.com/production/course_1478/datasets/latitude.xls"

# Import the .xls file with gdata: excel_gdata
excel_gdata <- read.xls(url_xls)

# Download file behind URL, name it local_latitude.xls
download.file(url_xls, destfile = "local_latitude.xls")

# Import the local .xls file with readxl: excel_readxl
excel_readxl <- read_excel("local_latitude.xls")
```
## Downloading any file, secure or not
```
# https URL to the wine RData file.
url_rdata <- "https://s3.amazonaws.com/assets.datacamp.com/production/course_1478/datasets/wine.RData"

# Download the wine file to your working directory
download.file(url_rdata, "wine_local.RData")

# Load the wine data into your workspace using load()
load("wine_local.RData")

# Print out the summary of the wine data
summary(wine)
```
## HTTP? httr! (1)
```
# Load the httr package
library(httr)

# Get the url, save response to resp
url <- "http://www.example.com/"
resp <- GET(url)

# Print resp
resp

# Get the raw content of resp: raw_content
raw_content <- content(resp, as = "raw")

# Print the head of raw_content
raw_content
```
## HTTP? httr! (2)
```
# Get the url
url <- "http://www.omdbapi.com/?apikey=ff21610b&t=Annie+Hall&y=&plot=short&r=json"
resp <- GET(url)

# Print resp
resp

# Print content of resp as text
content(resp, as = "text")

# Print content of resp
content(resp)
```


# 4. Importing data from the web (Part 2) 

## From JSON to R
```
# Load the jsonlite package
library(jsonlite)

# wine_json is a JSON
wine_json <- '{"name":"Chateau Migraine", "year":1997, "alcohol_pct":12.4, "color":"red", "awarded":false}'

# Convert wine_json into a list: wine
wine <- fromJSON(wine_json)

# Print structure of wine
str(wine)
```
## Quandl API
```
# Definition of quandl_url
quandl_url <- "https://www.quandl.com/api/v3/datasets/WIKI/FB/data.json?auth_token=i83asDsiWUUyfoypkgMz"

# Import Quandl data: quandl_data
quandl_data <- fromJSON(quandl_url)

# Print structure of quandl_data
str(quandl_data)
```
## OMDb API
```
# Definition of the URLs
url_sw4 <- "http://www.omdbapi.com/?apikey=ff21610b&i=tt0076759&r=json"
url_sw3 <- "http://www.omdbapi.com/?apikey=ff21610b&i=tt0121766&r=json"

# Import two URLs with fromJSON(): sw4 and sw3
sw4 <- fromJSON(url_sw4)
sw3 <- fromJSON(url_sw3)

# Print out the Title element of both lists
sw4$Title
sw3$Title

# Is the release year of sw4 later than sw3?
sw4$Year > sw3$Year
```
## JSON practice (1)
```
# Challenge 1
json1 <- '[1, 2, 3, 4, 5, 6]'
fromJSON(json1)

# Challenge 2
json2 <- '{"a":[1, 2, 3], "b":[4, 5, 6]}'
fromJSON(json2)
```
## JSON practice (2)
```
# Challenge 1
json1 <- '[[1, 2], [3, 4]]'
fromJSON(json1)

# Challenge 2
json2 <- '[{"a":1, "b":2}, {"a":3, "b":4}, {"a":5, "b":6}]'
fromJSON(json2)
```
## toJSON()
```
# URL pointing to the .csv file
url_csv <- "http://s3.amazonaws.com/assets.datacamp.com/production/course_1478/datasets/water.csv"

# Import the .csv file located at url_csv
water <- read.csv(url_csv, stringsAsFactors = FALSE)

# Convert the data file according to the requirements
water_json <- toJSON(water)

# Print out water_json
water_json
```
## Minify and prettify
```
# Convert mtcars to a pretty JSON: pretty_json
pretty_json <- toJSON(mtcars, pretty = TRUE)

# Print pretty_json
pretty_json

# Minify pretty_json: mini_json
mini_json <- minify(pretty_json)

# Print mini_json
mini_json
```


# 5. Importing data from statistical software packages 

## Import SAS data with haven
```
# Load the haven package
library(haven)

# Import sales.sas7bdat: sales
sales <- read_sas("sales.sas7bdat")

# Display the structure of sales
str(sales)
```
## Import STATA data with haven
```
# Import the data from the URL: sugar
sugar <- read_dta("http://assets.datacamp.com/production/course_1478/datasets/trade.dta")

# Structure of sugar
str(sugar)

# Convert values in Date column to dates
sugar$Date <- as.Date(as_factor(sugar$Date))

# Structure of sugar again
str(sugar)
```
## Import SPSS data with haven
```
# Import person.sav: traits
traits <- read_sav("person.sav")

# Summarize traits
summary(traits)

# Print out a subset
subset(traits, Extroversion > 40 & Agreeableness > 40)
```
## Factorize, round two
```
# Import SPSS data from the URL: work
work <- read_sav("http://s3.amazonaws.com/assets.datacamp.com/production/course_1478/datasets/employee.sav")

# Display summary of work$GENDER
summary(work$GENDER)

# Convert work$GENDER to a factor
work$GENDER <- as_factor(work$GENDER)

# Display summary of work$GENDER again
summary(work$GENDER)
```
## Import STATA data with foreign (1)
```
# Load the foreign package
library(foreign)

# Import florida.dta and name the resulting data frame florida
florida <- read.dta("florida.dta")

# Check tail() of florida
tail(florida)
```
## Import STATA data with foreign (2)
```
# Specify the file path using file.path(): path
path <- file.path("worldbank", "edequality.dta")

# Create and print structure of edu_equal_1
edu_equal_1 <- read.dta(path)
str(edu_equal_1)

# Create and print structure of edu_equal_2
edu_equal_2 <- read.dta(path, convert.factors = FALSE)
str(edu_equal_2)

# Create and print structure of edu_equal_3
edu_equal_3 <- read.dta(path, convert.underscore = TRUE)
str(edu_equal_3)
```
## Import SPSS data with foreign (1)
```
# Import international.sav as a data frame: demo
demo <- read.spss("international.sav", to.data.frame = TRUE)

# Create boxplot of gdp variable of demo
boxplot(demo$gdp)
```
## Import SPSS data with foreign (2)
```
# Import international.sav as demo_1
demo_1 <- read.spss("international.sav", to.data.frame = TRUE)

# Print out the head of demo_1
head(demo_1)

# Import international.sav as demo_2
demo_2 <- read.spss("international.sav", to.data.frame = TRUE, use.value.labels = FALSE)

# Print out the head of demo_2
head(demo_2)
```
