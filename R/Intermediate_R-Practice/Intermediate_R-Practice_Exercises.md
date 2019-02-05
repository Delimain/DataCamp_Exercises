**Note**: At the time of writing, all the exercises herein are offered on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource. The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Intermediate R - Practice](https://www.datacamp.com/courses/intermediate-r-practice)

# 1. Conditionals and Control Flow

## Grades analysis in R
```
# me, other_199, and previous_4 are available in your workspace

# Merge me and other_199: my_class
my_class <- c(me, other_199)

# cbind() my_class and previous_4: last_5
last_5 <- cbind(my_class, previous_4)

# Name last_5 appropriately
nms <- paste0("year_", 1:5)
colnames(last_5) <- nms
```
## Explore your data
```
# Build histogram of my_class
hist(my_class)

# Generate summary of last_5
summary(last_5)

# Build boxplot of last_5
boxplot(last_5)
```
## Basic queries
```
# Is your grade equal to 72?
me == 72

# Which grades in your class are higher than 75?
my_class > 75

# Which grades in the last 5 years are below or equal to 64?
last_5 <= 64
```
## Build aggregates
```
# How many grades in your class are higher than 75?
sum(my_class > 75)

# How many students in your class scored strictly higher than you?
sum(my_class > me)

# What's the proportion of grades below or equal to 64 in the last 5 years?
mean(last_5 <= 64)
```
## Logical operator
```
# Is your grade greater than 87 and smaller than or equal to 89?
me > 87 & me <= 89

# Which grades in your class are below 60 or above 90?
my_class < 60 | my_class > 90
```
## Build aggregates (2)
```
# What's the proportion of grades in your class that is average?
mean(my_class >= 70 & my_class <= 85)

# How many students in the last 5 years had a grade of 80 or 90?
sum(last_5 == 80 | last_5 == 90)
```
## if, else: DIY
```
# Define n_smart
n_smart <- sum(my_class >= 80)

# Code the if-else construct
if(n_smart > 50){
  print("smart class")
} else{
  print("rather average")
}
```
## else if
```
# Define prop_less
prop_less <- mean(my_class < me)

# Code the control construct
if(prop_less > 0.9) {
  print("you're among the best 10 percent")
} else if(prop_less > 0.8) {
  print("you're among the best 20 percent")
} else{
  print("need more analysis")
}
```
## Embed if-else clauses
```
# Embedded control structure: fix the error
if (mean(my_class) < 75) {
  if (mean(my_class) > me) {
    print("average year, but still smarter than me")
  } else {
    print("average year, but I'm not that bad")
  }
} else {
  if (mean(my_class) > me) {
    print("smart year, even smarter than me")
  } else {
    print("smart year, but I am smarter")
  }
}
```
## Operations and controls expertise
```
# Create top_grades
top_grades <- my_class[my_class >= 85]

# Create worst_grades
worst_grades <- my_class[my_class < 65]

# Write conditional statement
if(length(top_grades) > length(worst_grades)) {
  print("top grades prevail")
}
```


# 2. Loops

## Scanning Logs in R
```
# logs is already available in your workspace

# Print the structure of logs
str(logs)

# Use list subsetting to print the details part of 11th logs entry
logs[11]

# Print the class of the timestamp component of the first entry
class(logs[[1]]$timestamp)
```
## While: start easy
```
# Initialize the iterator i to be 1
i <- 1

# Code the while loop
while (logs[[i]]$success == TRUE) {
  print(i)
  i <- i +1
}
```
## Adapt the while loop
```
# Adapt the while loop
i <- 1
while (logs[[i]]$success) {
  print(logs[[i]]$details$message)
  i <- i + 1
}
```
## While: different approach
```
# Initialize i and found
i <- 1
found <- FALSE

# Code the while loop
while (found == FALSE) {
  if (logs[[i]]$success == FALSE && logs[[i]]$details$location == "waste") {
    print("found")
    found <- TRUE
  } else {
    print("still looking")
    i <- i + 1
  }
}
```
## The for loop
```
# Code a for loop that prints the timestamp of each log
for (i in 1:length(logs)) {
  print(logs[[i]]$timestamp)
}
```
## Going through the list
```
# Make the printout conditional: only if success
for (log in logs) {
  if(log$success == TRUE) {
    print(log$timestamp)
  }
}
```
## Adapt the logs list
```
# Finish the for loop: add date element for each entry
for (i in 1:length(logs)) {
  logs[[i]]$date <- as.Date(logs[[i]]$timestamp)
}

# Print first 6 elements in logs
head(logs)
```
## Collect all failures
```
# Intialize empty list: failures
failures <- list()

# Finish the for loop: add each failure to failures
for (log in logs) {
  if (log$success == FALSE) {
    failures <- c(failures, list(log))
  }
}

# Display the structure of failures
str(failures)
```


# 3. Functions

## Using functions
```
# Call max() on timestamps
max(timestamps)

# What is the date of the latest timestamp?
as.Date(max(timestamps))
```
## Optional Arguments
```
# Print out timestamps
# A faulty version of timestamps is available in your workspace

timestamps

# Call max() on timestamps, no additional arguments
max(timestamps)

# Call max() on timestamps, specify na.rm
max(timestamps, na.rm = TRUE)
```
## Extract log information (1)
```
# for loop to extract timestamp; put this inside function body below
info <- c()
for (log in logs) {
 info <- c(info, log$timestamp)
}

# Build a function extract_info(): use for loop, add return statement
extract_info <- function(x) {
  info <- c()
  for (log in x) {
    info <- c(info, log$timestamp)
  }
  return(info)
}

# Call extract_info() on logs
extract_info(logs)
```
## Extract log information (2)
```
# Adapt the extract_info() function.
extract_info <- function(x, property) {
  info <- c()
  for (log in x) {
   info <- c(info, log[[property]])
  }
  return(info)
}

# Call extract_info() on logs, set property to "timestamp"
extract_info(logs, "timestamp")

# Call extract_info() on logs, set property to "success"
extract_info(logs, "success")
```
## Extract log information (3)
```
# Add default value for property argument
extract_info <- function(x, property = "success") {
  info <- c()
  for (log in x) {
   info <- c(info, log[[property]])
  }
  return(info)
}

# Call extract_info() on logs, don't specify property
extract_info(logs)

# Call extract_info() on logs, set property to "timestamp"
extract_info(logs, property = "timestamp")
```
## Extract log information (4)
```
# Adapt extract_info():
# - add argument with default value
# - change function body
extract_info <- function(x, property = "success", include_all = TRUE) {
  info <- c()
  for (log in x) {
    if(include_all || !log$success) {
    # add if construct around the line below
    info <- c(info, log[[property]])
    }
  }
  return(info)
}

# Call extract_info() on logs, no additional arguments
extract_info(logs)

# Call extract_info() on logs, set include_all to FALSE
extract_info(logs, include_all = FALSE)
```
## Extract log information (5)
```
# Definition of the extract_info() function
extract_info <- function(x, property = "success", include_all = TRUE) {
  info <- c()
  for (log in x) {
    if (include_all || !log$success) {
     info <- c(info, log[[property]])
    }
  }
  return(info)
}

# Generate vector of messages
extract_info(logs, property = c("details", "message"))

# Generate vector of locations for failed log entries
extract_info(logs, property = c("details", "location"), include_all = FALSE)
```
## Over to you
```
# Write the function compute_fail_pct
compute_fail_pct <- function(x){
  failures <- 0
  for(i in 1:length(x)){
    if(!logs[[i]]$success){
      failures <- failures + 1
    }
  }
  return(100 * failures / length(x))
}
# Call compute_fail_pct() on logs
compute_fail_pct(logs)
```


# 4. The apply family 

## lapply refresher
```
# Call length() on each element of logs
lapply(logs, length)

# Call class() on each element of logs
lapply(logs, class)
```
## lapply on logs (1)
```
# Define get_timestamp()
get_timestamp <- function(x) {
  return(x$timestamp)
}

# Apply get_timestamp() over all elements in logs
lapply(logs, get_timestamp)
```
## lapply on logs (2)
```
# Have lapply() use an anonymous function
lapply(logs, function(x) {
  x$timestamp
})
```
## lapply on logs (3)
```
# Replace the anonymous function with `[[` 
lapply(logs, `[[`, "timestamp")
```
## sapply refresher
```
# Call length() on each element of logs using sapply()
sapply(logs, length)

# Definition of get_timestamp
get_timestamp <- function(x) {
  x$timestamp
}

# Get vector of log entries' timestamps
sapply(logs, get_timestamp)
```
## sapply on logs (1)
```
# Use sapply() to select the success element from each log: results
results <- sapply(logs, `[[`, "success")

# Call mean() on results
mean(results)

# Use sapply() to select the details element from each log
sapply(logs, `[[`, "details")
```
## sapply on logs (2)
```
# Implement function get_failure_loc
get_failure_loc <- function(x) {
  if (x$success) {
    return(NULL)
  } else {
    return(x$details$location)
  }
}

# Use sapply() to call get_failure_loc on logs
sapply(logs, get_failure_loc)
```
## vapply refresher
```
# Convert the sapply call to vapply
vapply(logs, length, integer(1))

# Convert the sapply call to vapply
vapply(logs, `[[`, logical(1), "success")
```
## vapply on logs (1)
```
# Convert the sapply() call to a vapply() or lapply() call
vapply(logs, `[[`, character(1), c("details", "message"))

# Convert the sapply() call to a vapply() or lapply() call
lapply(logs, function(x) { x$details })
```
## Loop it the way you want it
```
# Return vector with uppercase version of message elements in log entries
toupper(vapply(logs, `[[`, character(1), c("details", "message")))
```


# 5. Utilities

## Titanic
```
# Import titanic from csv
titanic <- read.csv("titanic.csv")

# Call dim on titanic
dim(titanic)

# Generate histogram of Age column
hist(titanic$Age)
```
## Exploratory queries
```
# Print out total value of fares
sum(titanic$Fare)

# Print out proportion of passengers that survived
mean(titanic$Survived)
```
## Infer gender from name (1)
```
# Extract the name column from titanic
pass_names <- titanic$Name

# Create the logical vector is_man
is_man <- grepl(", Mr\\.", pass_names)

# Count the number of men
sum(is_man)

# Count number of men based on gender
sum(titanic$Sex == "male")
```
## Infer gender from name (2)
```
# Extract the name column from titanic
pass_names <- titanic$Name

# Create titles
titles <- gsub("^.*, (.*?)\\..*$", "\\1", pass_names)

# Call unique() on titles
unique(titles)
```
## Infer gender from name (3)
```
pass_names <- titanic$Name
titles <- paste(",", c("Mr\\.", "Master", "Don", "Rev", "Dr\\.", "Major", "Sir", "Col", "Capt", "Jonkheer"))

# Finish the vapply() command
hits <- vapply(titles,
               FUN = grepl,
               FUN.VALUE = logical(length(pass_names)),
               pass_names)

# Calculate the sum() of hits
sum(hits)

# Count number of men based on gender
sum(titanic$Sex == "male")
```
## Reformat passenger names
```
convert_name <- function(name) {
  # women: take name from inside parentheses
  if (grepl("\\(.*?\\)", name)) {
    gsub("^.*?\\((.*?)\\)$", "\\1", name)
  # men: take name before comma and after title
  } else {
    # Finish the gsub() function
    gsub("^(.*?),\\s[a-zA-Z\\.]*?\\s(.*?)$", "\\2 \\1", name)
  }
}

# Call convert_name on name
clean_pass_names <- vapply(pass_names, FUN = convert_name,
                           FUN.VALUE = character(1), USE.NAMES = FALSE)

# Print out clean_pass_names
clean_pass_names
```
## Add birth dates
```
# Have a look at head() of dob1 and dob2
head(dob1)
head(dob2)

# Convert dob1 to dob1d, convert dob2 to dob2d
dob1d <- as.Date(dob1)
dob2d <- as.Date(dob2, "%B %d,%Y")

# Combine dob1d and dob2d into single vector: birth_dates
birth_dates <- c(dob1d, dob2d)
```
## Average age
```
# titanic, dob1 and dob2 are preloaded
dob1d <- as.Date(dob1)
dob2d <- as.Date(dob2, format = "%B %d, %Y")
birth_dates <- c(dob1d, dob2d)
disaster_date <- as.Date("1912-04-15")

# Add birth_dates to titanic (column Birth)
titanic$Birth <- birth_dates

# Create subset: survivors
survivors <- subset(titanic, Survived == 1)

# Calculate average age of survivors
mean(disaster_date - survivors$Birth, na.rm = TRUE)
```
