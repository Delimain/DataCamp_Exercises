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


# 3. Functions

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


# 4. The apply family 

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
