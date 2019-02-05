**Note**: At the time of writing, all the exercises herein are offered on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource. The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Introduction to Data](https://www.datacamp.com/courses/introduction-to-data)

# 1. Language of data 

## Loading data into R
```
# Load data
data(email50)

# View the structure of the data
str(email50)
```
## Identify variable types
```
#load packages
library(dplyr)

# Glimpse email50
glimpse(email50)
```
## Filtering based on a factor
```
# Subset of emails with big numbers: email50_big
email50_big <- email50 %>%
  filter(number == "big")

# Glimpse the subset
glimpse(email50_big)
```
## Complete filtering based on a factor
```
# Table of the number variable
table(email50_big$number)

# Drop levels
email50_big$number <- droplevels(email50_big$number)

# Another table of the number variable
table(email50_big$number)
```
## Discretize a different variable
```
# Calculate median number of characters: med_num_char
med_num_char <- median(email50$num_char)

# Create num_char_cat variable in email50
email50_fortified <- email50 %>%
  mutate(num_char_cat = ifelse(num_char < med_num_char, "below median", "at or above median"))
  
# Count emails in each category
email50_fortified %>%
  count(num_char_cat)
```
## Combining levels of a different factor
```
# Create number_yn column in email50
email50_fortified <- email50 %>%
  mutate(
    number_yn = case_when(
      # if number is "none", make number_yn "no"
      number == "none" ~ "no", 
      # if number is not "none", make number_yn "yes"
      number != "none" ~ "yes"  
    )
  )
  

# Visualize the distribution of number_yn
ggplot(email50_fortified, aes(x = number_yn)) +
  geom_bar()
```
## Visualizing numerical and categorical data
```
# Load ggplot2
library(ggplot2)

# Scatterplot of exclaim_mess vs. num_char
ggplot(email50, aes(x = num_char, y = exclaim_mess, color = factor(spam))) +
  geom_point()
```


# 2. Study types and cautionary tales 

## Identify type of study: Countries
```
# Load data
data(gapminder)

# Glimpse data
glimpse(gapminder)

# Identify type of study: observational or experimental
type_of_study <- "observational"
```
## Number of males and females admitted
```
# Count number of male and female applicants admitted
ucb_admit %>%
  count(Gender, Admit)
```
## Proportion of males admitted overall
```
ucb_admission_counts %>%
  # Group by gender
  group_by(Gender) %>%
  # Create new variable
  mutate(prop = n / sum(n)) %>%
  # Filter for admitted
  filter(Admit == "Admitted")
```
## Proportion of males admitted for each department
```
ucb_admission_counts <- ucb_admit %>%
  # Counts by department, then gender, then admission status
  count(Dept, Gender, Admit)

# See the result
ucb_admission_counts

ucb_admission_counts  %>%
  # Group by department, then gender
  group_by(Dept, Gender) %>%
  # Create new variable
  mutate(prop = n / sum(n)) %>%
  # Filter for male and admitted
  filter(Gender == "Male", Admit == "Admitted")
```


# 3. Sampling strategies and experimental design 

## Simple random sample in R
```
# Simple random sample: states_srs
states_srs <- us_regions %>%
  sample_n(size = 8)

# Count states by region
states_srs %>%
  count(region)
```
## Stratified sample in R
```
# Stratified sample
states_str <- us_regions %>%
  group_by(region) %>%
  sample_n(size = 2)

# Count states by region
states_str %>%
  group_by(region) %>%
  count()
```


# 4. Case study 

## Inspect the data
```
# Inspect evals
glimpse(evals)
```
## Identify variable types
```
# Inspect variable types
glimpse(evals)

# Remove non-factor variables from the vector below
cat_vars <- c("rank", "ethnicity", "gender", "language",
              "cls_level", "cls_profs", "cls_credits",
              "pic_outfit", "pic_color")
```
## Recode a variable
```
# Recode cls_students as cls_type
evals_fortified <- evals %>%
  mutate(cls_type = case_when(
         cls_students <= 18 ~ "small",
         cls_students >= 19 & cls_students <= 59 ~ "midsize",
         cls_students >= 60 ~ "large"
    )
  )
```
## Create a scatterplot
```
# Scatterplot of score vs. bty_avg
ggplot(evals, aes(x = bty_avg, y = score)) +
  geom_point()
```
## Create a scatterplot, with an added layer
```
# Scatterplot of score vs. bty_avg colored by cls_type
ggplot(evals, aes(x = bty_avg, y = score, color = cls_type)) +
  geom_point()
```
