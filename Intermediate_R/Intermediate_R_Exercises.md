**Note**: At the time of writing, all the exercises herein are offered on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource. The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Intermediate R](https://www.datacamp.com/courses/intermediate-r)

# 1. Conditionals and Control Flow

## Equality
```
# Comparison of logicals
T == F

# Comparison of numerics
(-6 * 14) != (17 - 101)

# Comparison of character strings
"useR" == "user"

# Compare a logical with a numeric
T == 1
```
## Greater and less than
```
# Comparison of numerics
(-6 * 5 + 2) >= (-10 + 1)

# Comparison of character strings
"raining" <= "raining dogs"

# Comparison of logicals
T > F
```
## Compare vectors
```
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)
facebook <- c(17, 7, 5, 16, 8, 13, 14)

# Popular days
linkedin > 15

# Quiet days
linkedin <= 5

# LinkedIn more popular than Facebook
linkedin > facebook
```
## Compare matrices
```
# The social data has been created for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)
facebook <- c(17, 7, 5, 16, 8, 13, 14)
views <- matrix(c(linkedin, facebook), nrow = 2, byrow = TRUE)

# When does views equal 13?
views == 13

# When is views less than or equal to 14?
views <= 14
```
## & and |
```
# The linkedin and last variable are already defined for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)
last <- tail(linkedin, 1)

# Is last under 5 or above 10?
last < 5 | last > 10

# Is last between 15 (exclusive) and 20 (inclusive)?
last > 15 & last <= 20
```
## & and | (2)
```
# linkedin exceeds 10 but facebook below 10
linkedin > 10 & facebook < 10

# When were one or both visited at least 12 times?
linkedin >= 12 | facebook >= 12

# When is views between 11 (exclusive) and 14 (inclusive)?
views > 11 & views <= 14
```
## Blend it all together
```
# li_df is pre-loaded in your workspace

# Select the second column, named day2, from li_df: second
second <- li_df$day2

# Build a logical vector, TRUE if value in second is extreme: extremes
extremes <- second > 25 | second < 5

# Count the number of TRUEs in extremes
sum(extremes)

# Solve it with a one-liner
sum(li_df$day2 > 25 | li_df$day2 < 5)
```
## The if statement
```
# Variables related to your last day of recordings
medium <- "LinkedIn"
num_views <- 14

# Examine the if statement for medium
if (medium == "LinkedIn") {
  print("Showing LinkedIn information")
}

# Write the if statement for num_views
if(num_views > 15){
  print("You're popular!")
}
```
## Add an else
```
# Variables related to your last day of recordings
medium <- "LinkedIn"
num_views <- 14

# Control structure for medium
if (medium == "LinkedIn") {
  print("Showing LinkedIn information")
  } else{
    print("Unknown medium")
  }

# Control structure for num_views
if (num_views > 15) {
  print("You're popular!")
  } else{
    print("Try to be more visible!")
  }  
```
## Customize further: else if
```
# Variables related to your last day of recordings
medium <- "LinkedIn"
num_views <- 14

# Control structure for medium
if (medium == "LinkedIn") {
  print("Showing LinkedIn information")
} else if (medium == "Facebook") {
  # Add code to print correct string when condition is TRUE
print("Showing Facebook information")
} else {
  print("Unknown medium")
}

# Control structure for num_views
if (num_views > 15) {
  print("You're popular!")
} else if (num_views <= 15 & num_views > 10) {
  # Add code to print correct string when condition is TRUE
print("Your number of views is average")
} else {
  print("Try to be more visible!")
}
```
## Take control!
```
# Variables related to your last day of recordings
li <- 15
fb <- 9

# Code the control-flow construct
if (li >= 15 & fb >= 15) {
  sms <- 2 * (li + fb)
} else if (li < 10 & fb < 10) {
  sms <- 0.5 * (li + fb)
} else {
  sms <- li + fb
}

# Print the resulting sms to the console
sms
```


# 2. Loops

## Write a while loop
```
# Initialize the speed variable
speed <- 64

# Code the while loop
while ( speed > 30) {
  print("Slow down!")
  speed <- speed - 7
}

# Print out the speed variable
speed
```
## Throw in more conditionals
```
# Initialize the speed variable
speed <- 64

# Extend/adapt the while loop
while (speed > 30) {
  print(paste("Your speed is", speed))
  if (speed > 48 ) {
    print("Slow down big time!")
    speed <- speed - 11
  } else {
    print("Slow down!")
    speed <- speed - 6
  }
}
```
## Stop the while loop: break
```
# Initialize the speed variable
speed <- 88

while (speed > 30) {
  print(paste("Your speed is", speed))
  
  # Break the while loop when speed exceeds 80
  if ( speed > 80) {
    break
  }
  
  if (speed > 48) {
    print("Slow down big time!")
    speed <- speed - 11
  } else {
    print("Slow down!")
    speed <- speed - 6
  }
}
```
## Build a while loop from scratch
```
# Initialize i as 1 
i <- 1

# Code the while loop
while (i <= 10) {
  print(3 * i)
  if ((3 * i) %% 8 == 0) {
    break
  }
  i <- i + 1
}
```
## Loop over a vector
```
# The linkedin vector has already been defined for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)

# Loop version 1
for(views in linkedin){
  print(views)
}

# Loop version 2
for(i in 1:length(linkedin)){
  print(linkedin[i])
}
```
## Loop over a list
```
# The nyc list is already specified
nyc <- list(pop = 8405837, 
            boroughs = c("Manhattan", "Bronx", "Brooklyn", "Queens", "Staten Island"), 
            capital = FALSE)

# Loop version 1
for(deets in nyc){
  print(deets)
}

# Loop version 2
for(i in 1:length(nyc)){
  print(nyc[[i]])
}
```
## Loop over a matrix
```
# The tic-tac-toe matrix ttt has already been defined for you

# define the double for loop
for (i in 1:nrow(ttt)) {
  for (j in 1:ncol(ttt)) {
    print(paste("On row", i, "and column", j, "the board contains", ttt[i,j]))
  }
}
```
## Mix it up with control flow
```
# The linkedin vector has already been defined for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)

# Code the for loop with conditionals
for (li in linkedin) {
  if (li > 10) {
    print("You're popular!")
  } else {
    print("Be more visible!")
  }
  print(li)
}
```
## Next, you break it
```
# The linkedin vector has already been defined for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)

# Adapt/extend the for loop
for (li in linkedin) {
  if (li > 10) {
    print("You're popular!")
  } else {
    print("Be more visible!")
  }
  
  # Add if statement with break
  if(li > 16){
    print("This is ridiculous, I'm outta here!")
    break
  }
  
  # Add if statement with next
  if(li < 5){
    print("This is too embarrassing!")
    next
  }
  
  print(li)
}
```
## Build a for loop from scratch
```
# Pre-defined variables
rquote <- "r's internals are irrefutably intriguing"
chars <- strsplit(rquote, split = "")[[1]]

# Initialize rcount
rcount <- 0

# Finish the for loop
for (char in chars) {
  if(char == "r"){
    rcount <- rcount + 1
  }
  if(char == "u"){
    break
  }
}

# Print out rcount
rcount
```


# 3. Functions

## Function documentation
```
# Consult the documentation on the mean() function
?mean

# Inspect the arguments of the mean() function
args(mean)
```
## Use a function
```
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)
facebook <- c(17, 7, 5, 16, 8, 13, 14)

# Calculate average number of views
avg_li=mean(linkedin)
avg_fb=mean(facebook)

# Inspect avg_li and avg_fb
avg_li
avg_fb
```
## Use a function (2)
```
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)
facebook <- c(17, 7, 5, 16, 8, 13, 14)

# Calculate the mean of the sum
avg_sum <- mean(linkedin + facebook)

# Calculate the trimmed mean of the sum
avg_sum_trimmed <- mean(linkedin + facebook, trim = 0.2)

# Inspect both new variables
avg_sum
avg_sum_trimmed
```
## Use a function (3)
```
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, NA, 17, 14)
facebook <- c(17, NA, 5, 16, 8, 13, 14)

# Basic average of linkedin
mean(linkedin)

# Advanced average of linkedin
mean(linkedin, na.rm = TRUE)
```
## Functions inside functions
```
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, NA, 17, 14)
facebook <- c(17, NA, 5, 16, 8, 13, 14)

# Calculate the mean absolute deviation
mean(abs(linkedin - facebook), na.rm = TRUE)
```
## Write your own function
```
# Create a function pow_two()
pow_two <- function(x){
  x ^ 2
}

# Use the function
pow_two(12)

# Create a function sum_abs()
sum_abs <- function(a, b){
  sum(abs(a), abs(b))
}

# Use the function
sum_abs(-2, 3)
```
## Write your own function (2)
```
# Define the function hello()
hello <- function(){
  print("Hi there!")
  return(TRUE)
}
# Call the function hello()
hello()
```
## Write your own function (3)
```
# Finish the pow_two() function
pow_two <- function(x, print_info = TRUE) {
  y <- x ^ 2
  if(print_info == TRUE){
    print(paste(x, "to the power two equals", y))
  }
  return(y)
}
```
## R you functional?
```
# Define the interpret function
interpret <- function(num_views) {
  if (num_views > 15) {
    print("You're popular!")
    return(num_views)
  } else {
      print("Try to be more visible!")
      return(0)
  }
}

# Call the interpret function twice
interpret(linkedin[1])
interpret(facebook[2])
```
## R you functional? (2)
```
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)
facebook <- c(17, 7, 5, 16, 8, 13, 14)

# The interpret() can be used inside interpret_all()
interpret <- function(num_views) {
  if (num_views > 15) {
    print("You're popular!")
    return(num_views)
  } else {
    print("Try to be more visible!")
    return(0)
  }
}

# Define the interpret_all() function
# views: vector with data to interpret
# return_sum: return total number of views on popular days?
interpret_all <- function(views, return_sum = TRUE) {
  count <- 0

  for (v in views) {
    count <- count + interpret(v)
  }

  if (return_sum == TRUE) {
    return(count)
  } else {
    return(NULL)
  }
}

# Call the interpret_all() function on both linkedin and facebook
interpret_all(linkedin)
interpret_all(facebook)
```
## Load an R Package
```
# Load the ggplot2 package
library(ggplot2)

# Retry the qplot() function
qplot(mtcars$wt, mtcars$hp)

# Check out the currently attached packages again
search()
```


# 4. The apply family 

## Use lapply with a built-in R function
```
# The vector pioneers has already been created for you
pioneers <- c("GAUSS:1777", "BAYES:1702", "PASCAL:1623", "PEARSON:1857")

# Split names from birth year
split_math <- strsplit(pioneers, split = ":")

# Convert to lowercase strings: split_low
split_low <- lapply(split_math, tolower)

# Take a look at the structure of split_low
str(split_low)
```
## Use lapply with your own function
```
# Code from previous exercise:
pioneers <- c("GAUSS:1777", "BAYES:1702", "PASCAL:1623", "PEARSON:1857")
split <- strsplit(pioneers, split = ":")
split_low <- lapply(split, tolower)

# Write function select_first()
select_first <- function(x) {
  x[1]
}

# Apply select_first() over split_low: names
names <- lapply(split_low, select_first)

# Write function select_second()
select_second <- function(x){
  x[2]
}

# Apply select_second() over split_low: years
years <- lapply(split_low, select_second)
```
## lapply and anonymous functions
```
# split_low has been created for you
split_low

# Transform: use anonymous function inside lapply
names <- lapply(split_low, function(x){x[1]})

# Transform: use anonymous function inside lapply
years <- lapply(split_low, function(x){x[2]})
```
## Use lapply with additional arguments
```
# Definition of split_low
pioneers <- c("GAUSS:1777", "BAYES:1702", "PASCAL:1623", "PEARSON:1857")
split <- strsplit(pioneers, split = ":")
split_low <- lapply(split, tolower)

# Generic select function
select_el <- function(x, index) {
  x[index]
}

# Use lapply() twice on split_low: names and years
names <- lapply(split_low, select_el, index = 1)
years <- lapply(split_low, select_el, index = 2)
```
## How to use sapply
```
# temp has already been defined in the workspace

# Use lapply() to find each day's minimum temperature
lapply(temp, min)

# Use sapply() to find each day's minimum temperature
sapply(temp, min)

# Use lapply() to find each day's maximum temperature
lapply(temp, max)

# Use sapply() to find each day's maximum temperature
sapply(temp, max)
```
## sapply with your own function
```
# temp is already defined in the workspace

# Finish function definition of extremes_avg
extremes_avg <- function(x) {
  (min(x) + max(x)) / 2
}

# Apply extremes_avg() over temp using sapply()
sapply(temp, extremes_avg)

# Apply extremes_avg() over temp using lapply()
lapply(temp, extremes_avg)
```
## sapply with function returning vector
```
# temp is already available in the workspace

# Create a function that returns min and max of a vector: extremes
extremes <- function(x) {
  c(min = min(x), max = max(x))
}

# Apply extremes() over temp with sapply()
sapply(temp, extremes)

# Apply extremes() over temp with lapply()
lapply(temp, extremes)
```
## sapply can't simplify, now what?
```
# temp is already prepared for you in the workspace

# Definition of below_zero()
below_zero <- function(x) {
  return(x[x < 0])
}

# Apply below_zero over temp using sapply(): freezing_s
freezing_s=sapply(temp, below_zero)

# Apply below_zero over temp using lapply(): freezing_l
freezing_l=lapply(temp, below_zero)

# Are freezing_s and freezing_l identical?
identical(freezing_l, freezing_s)
```
## sapply with functions that return NULL
```
# temp is already available in the workspace

# Definition of print_info()
print_info <- function(x) {
  cat("The average temperature is", mean(x), "\n")
}

# Apply print_info() over temp using sapply()
sapply(temp, print_info)

# Apply print_info() over temp using lapply()
lapply(temp, print_info)
```
## Use vapply
```
# temp is already available in the workspace

# Definition of basics()
basics <- function(x) {
  c(min = min(x), mean = mean(x), max = max(x))
}

# Apply basics() over temp using vapply()
vapply(temp, basics, numeric(3))
```
## Use vapply (2)
```
# temp is already available in the workspace

# Definition of the basics() function
basics <- function(x) {
  c(min = min(x), mean = mean(x), median = median(x), max = max(x))
}

# Fix the error:
vapply(temp, basics, numeric(4))
```
## From sapply to vapply
```
# temp is already defined in the workspace

# Convert to vapply() expression
sapply(temp, max)
vapply(temp, max, numeric(1))

# Convert to vapply() expression
sapply(temp, function(x, y) {mean(x) > y}, y = 5)
vapply(temp, function(x, y) {mean(x) > y}, y = 5, logical(1))
```


# 5. Utilities

## 
```

```
## 
```

```
## 
```

```
## 
```

```
## 
```

```
## 
```

```
## 
```

```
## 
```

```
## 
```

```
## 
```

```
## 
```

```
## 
```

```
## 
```

```
## 
```

```
