**Note**: At the time of writing, all the exercises herein are offered on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource. The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Data Analysis in R, the data.table Way](https://www.datacamp.com/courses/data-table-data-manipulation-r-tutorial)

# 1. Data.table novice

## Create and subset a data.table
```
library(data.table)

# Create my_first_data_table
my_first_data_table <- data.table(x = c("a", "b", "c", "d", "e"), 
                                  y = c(1, 2, 3, 4, 5))  
  
# Create a data.table using recycling
DT <- data.table(a = c(1L, 2L), b = LETTERS[1:4])

# Print the third row to the console
DT[3, ]

# Print the second and third row to the console without using commas
DT[2:3]
```
## Getting to know a data.table
```
# Print the second to last row of DT using .N
DT[.N-1]

# Print the column names of DT
names(DT)

# Print the number or rows and columns of DT
dim(DT)

# Print a new data.table containing rows 2, 2, and 3 of DT
DT[c(2, 2, 3), ]
```
## Subsetting data.tables
```
# Subset rows 1 and 3, and columns B and C
DT[c(1, 3), .(B, C)]

# Assign to ans the correct value
ans <- DT[, .(B, val = A * C)]
  
# Fill in the blanks such that ans2 equals target
target <- data.table(B = c("a", "b", "c", "d", "e", 
                           "a", "b", "c", "d", "e"), 
                     val = as.integer(c(6:10, 1:5)))
ans2 <- DT[, .(B, val = target[, val])]
```
## The by basics
```
# iris is already available in your workspace

# Convert iris to a data.table: DT
DT <- data.table(iris)

# For each Species, print the mean Sepal.Length
DT[, mean(Sepal.Length), by = Species]

# Print mean Sepal.Length, grouping by first letter of Species
DT[, mean(Sepal.Length), by = substr(Species, 1, 1)]
```
## Using .N and by
```
# Group the specimens by Sepal area (to the nearest 10 cm2) and count how many occur in each group
DT[, .N, by = 10 * round(Sepal.Length * Sepal.Width / 10)]

# Now name the output columns `Area` and `Count`
DT[, .(Count = .N), by = .(Area = 10 * round(Sepal.Length * Sepal.Width / 10))]
```
## Return multiple numbers in j
```
# Create the data.table DT
DT <- data.table(A = rep(letters[2:1], each = 4L), 
                 B = rep(1:4, each = 2L), 
                 C = sample(8))

# Create the new data.table, DT2
DT2 <- DT[, .(C = cumsum(C)), by = .(A, B)]

# Select from DT2 the last two values from C while you group by A
DT2[, .(C = tail(C, 2)), by = A]
```


# 2. Data.table yeoman 

## Chaining, the basics
```
# Combine the two steps in a one-liner
DT[, .(C = cumsum(C)), by = .(A, B)][, .(C = tail(C, 2)), by = A]
```
## Chaining your iris dataset
```
# Perform chained operations on DT
DT[, .(Sepal.Length = median(Sepal.Length), 
       Sepal.Width = median(Sepal.Width), 
       Petal.Length = median(Petal.Length),
       Petal.Width = median(Petal.Width)), 
   by = Species][order(Species, decreasing = TRUE)]
```
## Programming time vs readability
```
# Mean of columns
DT[, lapply(.SD, mean), by = x]

# Median of columns
DT[, lapply(.SD, median), by = x]
```
## Introducing .SDcols
```
# Calculate the sum of the Q columns
DT[, lapply(.SD, sum), .SDcols = 2:4]

# Calculate the sum of columns H1 and H2 
DT[, lapply(.SD, sum), .SDcols = paste0("H", 1:2)]

# Select all but the first row of groups 1 and 2, returning only the grp column and the Q columns
DT[, lapply(.SD, `[`, -1) , .SDcols = paste0("Q", 1:3), by = grp]
```
## Mixing it together: lapply, .SD, .SDcols and .N
```
# Sum of all columns and the number of rows
DT[, c(lapply(.SD, sum), list(N = .N)), .SDcols = c("x", "y", "z"), by = x]

# Cumulative sum of column x and y while grouping by x and z > 8
DT[, lapply(.SD, cumsum), .SDcols = c("x", "y"), by = .(by1 = x, by2 = z > 8)]
```
## Adding, updating and removing columns
```
# The data.table DT
DT <- data.table(A = letters[c(1, 1, 1, 2, 2)], B = 1:5)

# Add column by reference: Total
DT[, Total := sum(B), by = A]

# Add 1 to column B
DT[c(2,4), B := B + 1L]

# Add a new column Total2
DT[2:4, Total2 := sum(B), by = A]

# Remove the Total column
DT[, Total := NULL]

# Select the third column using `[[`
DT[[3]]
```
## The functional form
```
# A data.table DT has been created for you
DT <- data.table(A = c(1, 1, 1, 2, 2), B = 1:5)

# Update B, add C and D
DT[, `:=`(B = B + 1, C = A + B, D = 2)]

# Delete my_cols
my_cols <- c("B", "C")
DT[, (my_cols) := NULL]

# Delete column 2 by number
DT[, 2 := NULL]
```
## Ready, set(), go!
```
# Set the seed
set.seed(1)

# Check the DT that is made available to you
DT

# For loop with set
for(i in 1:3)set(DT, sample(1:10, 3, replace = FALSE), 1L + i, NA)

# Change the column names to lowercase
setnames(DT, names(DT), tolower(names(DT)))

# Print the resulting DT to the console
DT
```
## The set() family
```
# Define DT
DT <- data.table(a = letters[c(1, 1, 1, 2, 2)], b = 1)

# Add a suffix "_2" to all column names
setnames(DT, names(DT), paste0(names(DT), "_2"))

# Change column name "a_2" to "A2"
setnames(DT, "a_2", "A2")

# Reverse the order of the columns
setcolorder(DT, rev(names(DT)))
```


# 3. Data.table expert 

## Selecting rows the data.table way
```
# Convert iris to a data.table
iris <- data.table(iris)

# Species is "virginica"
iris[Species == "virginica"]

# Species is either "virginica" or "versicolor"
iris[Species == "virginica" | Species == "versicolor"]
```
## Removing columns and adapting your column names
```
# Remove the "Sepal." prefix
setnames(iris, names(iris), gsub("Sepal\\.", "", names(iris)))

# Remove the two columns starting with "Petal"
iris[, grep("^Petal", names(iris)) := NULL]
```
## Understanding automatic indexing
```
# Cleaned up iris data.table
iris

# Area is greater than 20 square centimeters
iris[(Length * Width) > 20]

# Add new boolean column
iris[, is_large := Width * Length > 25]

# Now large observations with is_large
iris[is_large == TRUE]
```
## Selecting groups or parts of groups
```
# The 'keyed' data.table DT
DT <- data.table(A = letters[c(2, 1, 2, 3, 1, 2, 3)], 
                 B = c(5, 4, 1, 9, 8, 8, 6), 
                 C = 6:12)
setkey(DT, A, B)

# Select the "b" group
DT[A == "b"]

# "b" and "c" groups
DT[.(c("b", "c"))]

# The first row of the "b" and "c" groups
DT[.(c("b", "c")), mult = "first"]

# First and last row of the "b" and "c" groups
DT[.(c("b", "c")), .SD[c(1, .N)], by = .EACHI]

# Copy and extend code for instruction 4: add printout
DT[.(c("b", "c")), {print(.SD); .SD[c(1, .N)]}, by = .EACHI]
```
## Rolling joins - part one
```
# Keyed data.table DT
DT <- data.table(A = letters[c(2, 1, 2, 3, 1, 2, 3)], 
                 B = c(5, 4, 1, 9, 8, 8, 6), 
                 C = 6:12, 
                 key = "A,B")

# Get the key of DT
key(DT)

# Row where A == "b" and B == 6
DT[.("b", 6)]

# Return the prevailing row
DT[.("b", 6), roll = TRUE]

# Return the nearest row
DT[.("b", 6), roll = "nearest"]
```
## Rolling joins - part two
```
# Print the sequence (-2):10 for the "b" group
DT[.("b", (-2):10)]

# Add code: carry the prevailing values forwards
DT[.("b", (-2):10), roll = +Inf]

# Add code: carry the first observation backwards
DT[.("b", (-2):10), roll = +Inf, rollends = c(TRUE, TRUE)]
```
