**Note**: At the time of writing, all the information herein--which has been copied verbatim to showcase markdown proficiency--is offered freely on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource.
# [Introduction to R](https://www.datacamp.com/courses/free-introduction-to-r)

## Course Description

In this introduction to R, you will master the basics of this beautiful open source language, including factors, lists and data frames. With the knowledge gained in this course, you will be ready to undertake your first very own data analysis. With over 2 million users worldwide R is rapidly becoming the leading programming language in statistics and data science. Every year, the number of R users grows by 40% and an increasing number of organizations are using it in their day-to-day activities. Leverage the power of R by completing this R online course today!

### Chapters
1. [Intro to Basics](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Instructions.md#1-intro-to-basics)
2. [Vectors](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Instructions.md#2-vectors)
3. [Matrices](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Instructions.md#3-matrices
)
4. [Factors](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Instructions.md#4-factors)
5. [Data frames](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Instructions.md#5-data-frames)
6. [Lists](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Instructions.md#6-lists)

### 1. [Intro to Basics](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#1-intro-to-basics)

In this chapter, you will take your first steps with R. You will learn how to use the console as a calculator and how to assign variables. You will also get to know the basic data types in R. Let's get started!

1. [How it works](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#how-it-works)

> In the editor on the right you should type R code to solve the exercises. When you hit the 'Submit Answer' button, every line of code is interpreted and executed by R and you get a message whether or not your code was correct. The output of your R code is shown in the console in the lower right corner.
> 
> R makes use of the `#` sign to add comments, so that you and others can understand what the R code is about. Just like Twitter! Comments are not run as R code, so they will not influence your result. For example, Calculate 3 + 4 in the editor on the right is a comment.
> 
> You can also execute R commands straight in the console. This is a good way to experiment with R code, as your submission is not checked for correctness.

2. [Arithmetic with R](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#arithmetic-with-r)

> In its most basic form, R can be used as a simple calculator. Consider the following arithmetic operators:
> 
>   - Addition: `+`
>   - Subtraction: `-`
>   - Multiplication: `*`
>   - Division: `/`
>   - Exponentiation: `^`
>   - Modulo: `%%`
> 
> The last two might need some explaining:
> 
>   - The `^` operator raises the number to its left to the power of the number to its right: for example `3^2` is 9.
>   - The modulo returns the remainder of the division of the number to the left by the number on its right, for example 5 modulo 3 or `5 %% 3` is 2.
> 
> With this knowledge, follow the instructions below to complete the exercise.

3. [Variable assignment](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#variable-assignment)

> A basic concept in (statistical) programming is called a variable.
> 
> A variable allows you to store a value (e.g. 4) or an object (e.g. a function description) in R. You can then later use this variable's name to easily access the value or the object that is stored within this variable.
> 
> You can assign a value 4 to a variable `my_var` with the command
> 
> `my_var <- 4`

4. [Variable assignment (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#variable-assignment-2)

> Suppose you have a fruit basket with five apples. As a data analyst in training, you want to store the number of apples in a variable with the name `my_apples`.

5. [Variable assignment (3)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#variable-assignment-3)

> Every tasty fruit basket needs oranges, so you decide to add six oranges. As a data analyst, your reflex is to immediately create the variable `my_oranges` and assign the value 6 to it. Next, you want to calculate how many pieces of fruit you have in total. Since you have given meaningful names to these values, you can now code this in a clear way:
> 
> `my_apples + my_oranges`

6. [Apples and oranges](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#apples-and-oranges)

> Common knowledge tells you not to add apples and oranges. But hey, that is what you just did, no :-)? The `my_apples` and `my_oranges` variables both contained a number in the previous exercise. The `+` operator works with numeric variables in R. If you really tried to add "apples" and "oranges", and assigned a text value to the variable `my_oranges` (see the editor), you would be trying to assign the addition of a numeric and a character variable to the variable `my_fruit`. This is not possible.

7. [Basic data types in R](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#basic-data-types-in-r)

> R works with numerous data types. Some of the most basic types to get started are:
> 
>   - Decimal values like `4.5` are called numerics.
>   - Natural numbers like `4` are called integers. Integers are also numerics.
>   - Boolean values (`TRUE` or `FALSE`) are called logical.
>   - Text (or string) values are called characters.
> 
> Note how the quotation marks on the right indicate that "some text" is a character.

8. [What's that data type?](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#whats-that-data-type)

> Do you remember that when you added `5 + "six"`, you got an error due to a mismatch in data types? You can avoid such embarrassing situations by checking the data type of a variable beforehand. You can do this with the `class()` function, as the code on the right shows.


### 2. [Vectors](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#2-vectors)

In this R course, we'll take you on a trip to Vegas, where you will learn how to analyze your gambling results using vectors in R! After completing this chapter, you will be able to create vectors in R, name them, select elements from them and compare different vectors. 

1. [Create a vector](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#create-a-vector)

> Feeling lucky? You better, because this chapter takes you on a trip to the City of Sins, also known as Statisticians Paradise!
> 
> Thanks to R and your new data-analytical skills, you will learn how to uplift your performance at the tables and fire off your career as a professional gambler. This chapter will show how you can easily keep track of your betting progress and how you can do some simple analyses on past actions. Next stop, Vegas Baby... VEGAS!!

2. [Create a vector (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#create-a-vector-2)

> Let us focus first!
> 
> On your way from rags to riches, you will make extensive use of vectors. Vectors are one-dimension arrays that can hold numeric data, character data, or logical data. In other words, a vector is a simple tool to store data. For example, you can store your daily gains and losses in the casinos.
> 
> In R, you create a vector with the combine function `c()`. You place the vector elements separated by a comma between the parentheses. For example:
> ```
> numeric_vector <- c(1, 2, 3)
> character_vector <- c("a", "b", "c")
> ```
> Once you have created these vectors in R, you can use them to do calculations.

3. [Create a vector (3)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#create-a-vector-3)

> After one week in Las Vegas and still zero Ferraris in your garage, you decide that it is time to start using your data analytical superpowers.
> 
> Before doing a first analysis, you decide to first collect all the winnings and losses for the last week:
> 
> For `poker_vector`:
> 
>   - On Monday you won $140
>   - Tuesday you lost $50
>   - Wednesday you won $20
>   - Thursday you lost $120
>   - Friday you won $240
> 
> For `roulette_vector`:
> 
>   - On Monday you lost $24
>   - Tuesday you lost $50
>   - Wednesday you won $100
>   - Thursday you lost $350
>   - Friday you won $10
> 
> You only played poker and roulette, since there was a delegation of mediums that occupied the craps tables. To be able to use this data in R, you decide to create the variables `poker_vector` and `roulette_vector`.

4. [Naming a vector](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#naming-a-vector)

> As a data analyst, it is important to have a clear view on the data that you are using. Understanding what each element refers to is therefore essential.
> 
> In the previous exercise, we created a vector with your winnings over the week. Each vector element refers to a day of the week but it is hard to tell which element belongs to which day. It would be nice if you could show that in the vector itself.
> 
> You can give a name to the elements of a vector with the `names()` function. Have a look at this example:
> ```
> some_vector <- c("John Doe", "poker player")
> names(some_vector) <- c("Name", "Profession")
> ```
> This code first creates a vector `some_vector` and then gives the two elements a name. The first element is assigned the name `Name`, while the second element is labeled `Profession`. Printing the contents to the console yields following output:
> ```
>           Name     Profession 
>     "John Doe" "poker player" 
> ```

5. [Naming a vector (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#naming-a-vector-2)

> If you want to become a good statistician, you have to become lazy. (If you are already lazy, chances are high you are one of those exceptional, natural-born statistical talents.)
> 
> In the previous exercises you probably experienced that it is boring and frustrating to type and retype information such as the days of the week. However, when you look at it from a higher perspective, there is a more efficient way to do this, namely, to assign the days of the week vector to a **variable**!
> 
> Just like you did with your poker and roulette returns, you can also create a variable that contains the days of the week. This way you can use and re-use it.

6. [Calculating total winnings](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#calculating-total-winnings)

> Now that you have the poker and roulette winnings nicely as named vectors, you can start doing some data analytical magic.
> 
> You want to find out the following type of information:
> 
>   - How much has been your overall profit or loss per day of the week?
>   - Have you lost money over the week in total?
>   - Are you winning/losing money on poker or on roulette?
> 
> To get the answers, you have to do arithmetic calculations on vectors.
> 
> It is important to know that if you sum two vectors in R, it takes the element-wise sum. For example, the following three statements are completely equivalent:
> ```
> c(1, 2, 3) + c(4, 5, 6)
> c(1 + 4, 2 + 5, 3 + 6)
> c(5, 7, 9)
> ```
> You can also do the calculations with variables that represent vectors:
> ```
> a <- c(1, 2, 3) 
> b <- c(4, 5, 6)
> c <- a + b
> ```

7. [Calculating total winnings (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#calculating-total-winnings-2)

> Now you understand how R does arithmetic with vectors, it is time to get those Ferraris in your garage! First, you need to understand what the overall profit or loss per day of the week was. The total daily profit is the sum of the profit/loss you realized on poker per day, and the profit/loss you realized on roulette per day.
> 
> In R, this is just the sum of `roulette_vector` and `poker_vector`.

8. [Calculating total winnings (3)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#calculating-total-winnings-3)

> Based on the previous analysis, it looks like you had a mix of good and bad days. This is not what your ego expected, and you wonder if there may be a very tiny chance you have lost money over the week in total?
> 
> A function that helps you to answer this question is `sum()`. It calculates the sum of all elements of a vector. For example, to calculate the total amount of money you have lost/won with poker you do:
> ```
> total_poker <- sum(poker_vector)
> ```

9. [Comparing total winnings](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#comparing-total-winnings)

> Oops, it seems like you are losing money. Time to rethink and adapt your strategy! This will require some deeper analysis...
> 
> After a short brainstorm in your hotel's jacuzzi, you realize that a possible explanation might be that your skills in roulette are not as well developed as your skills in poker. So maybe your total gains in poker are higher (or `>` ) than in roulette.

10. [Vector selection: the good times](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#vector-selection-the-good-times)

> Your hunch seemed to be right. It appears that the poker game is more your cup of tea than roulette.
> 
> Another possible route for investigation is your performance at the beginning of the working week compared to the end of it. You did have a couple of Margarita cocktails at the end of the week...
> 
> To answer that question, you only want to focus on a selection of the `total_vector`. In other words, our goal is to select specific elements of the vector. To select elements of a vector (and later matrices, data frames, ...), you can use square brackets. Between the square brackets, you indicate what elements to select. For example, to select the first element of the vector, you type `poker_vector[1]`. To select the second element of the vector, you type `poker_vector[2]`, etc. Notice that the first element in a vector has index 1, not 0 as in many other programming languages.

11. [Vector selection: the good times (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#vector-selection-the-good-times-2)

> How about analyzing your midweek results?
> 
> To select multiple elements from a vector, you can add square brackets at the end of it. You can indicate between the brackets what elements should be selected. For example: suppose you want to select the first and the fifth day of the week: use the vector `c(1, 5)` between the square brackets. For example, the code below selects the first and fifth element of poker_vector:
> ```
> poker_vector[c(1, 5)]
> ```

12. [Vector selection: the good times (3)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#vector-selection-the-good-times-3)

> Selecting multiple elements of `poker_vector` with `c(2, 3, 4)` is not very convenient. Many statisticians are lazy people by nature, so they created an easier way to do this: `c(2, 3, 4)` can be abbreviated to `2:4`, which generates a vector with all natural numbers from 2 up to 4.
> 
> So, another way to find the mid-week results is `poker_vector[2:4]`. Notice how the vector `2:4` is placed between the square brackets to select element 2 up to 4.

13. [Vector selection: the good times (4)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#vector-selection-the-good-times-4)

> Another way to tackle the previous exercise is by using the names of the vector elements (Monday, Tuesday, ...) instead of their numeric positions. For example,
> ```
> poker_vector["Monday"]
> ```
> will select the first element of `poker_vector` since `"Monday"` is the name of that first element.
> 
> Just like you did in the previous exercise with numerics, you can also use the element names to select multiple elements, for example:
> ```
> poker_vector[c("Monday","Tuesday")]
> ```

14. [Selection by comparison - Step 1](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#selection-by-comparison---step-1)

> By making use of comparison operators, we can approach the previous question in a more proactive way.
> 
> The (logical) comparison operators known to R are:
> 
>   - `<` for less than
>   - `>` for greater than
>   - `<=` for less than or equal to
>   - `>=` for greater than or equal to
>   - `==` for equal to each other
>   - `!=` not equal to each other
> 
> As seen in the previous chapter, stating `6 > 5` returns `TRUE`. The nice thing about R is that you can use these comparison operators also on vectors. For example:
> ```
> > c(4, 5, 6) > 5
> [1] FALSE FALSE TRUE
> ```
> This command tests for every element of the vector if the condition stated by the comparison operator is `TRUE` or `FALSE`.

15. [Selection by comparison - Step 2](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#selection-by-comparison---step-2)

> Working with comparisons will make your data analytical life easier. Instead of selecting a subset of days to investigate yourself (like before), you can simply ask R to return only those days where you realized a positive return for poker.
> 
> In the previous exercises you used `selection_vector <- poker_vector > 0` to find the days on which you had a positive poker return. Now, you would like to know not only the days on which you won, but also how much you won on those days.
> 
> You can select the desired elements, by putting `selection_vector` between the square brackets that follow `poker_vector`:
> ```
> poker_vector[selection_vector]
> ```
> R knows what to do when you pass a logical vector in square brackets: it will only select the elements that correspond to `TRUE` in `selection_vector`.

16. [Advanced selection](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#advanced-selection)

> Just like you did for poker, you also want to know those days where you realized a positive return for roulette.


### 3. [Matrices](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#3-matrices)

In this chapter you will learn how to work with matrices in R. By the end of the chapter, you will be able to create matrices and to understand how you can do basic computations with them. You will analyze the box office numbers of Star Wars to illustrate the use of matrices in R. May the force be with you! 

1. [What's a matrix?](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#whats-a-matrix)

> In R, a matrix is a collection of elements of the same data type (numeric, character, or logical) arranged into a fixed number of rows and columns. Since you are only working with rows and columns, a matrix is called two-dimensional.
> 
> You can construct a matrix in R with the [`matrix()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/matrix) function. Consider the following example:
> ```
> matrix(1:9, byrow = TRUE, nrow = 3)
> ```
> In the [`matrix()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/matrix) function:
> 
>   - The first argument is the collection of elements that R will arrange into the rows and columns of the matrix. Here, we use `1:9` which is a shortcut for `c(1, 2, 3, 4, 5, 6, 7, 8, 9)`.
>   - The argument `byrow` indicates that the matrix is filled by the rows. If we want the matrix to be filled by the columns, we just place `byrow = FALSE`.
>   - The third argument `nrow` indicates that the matrix should have three rows.

2. [Analyze matrices, you shall](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#analyze-matrices-you-shall)

> It is now time to get your hands dirty. In the following exercises you will analyze the box office numbers of the Star Wars franchise. May the force be with you!
> 
> In the editor, three vectors are defined. Each one represents the box office numbers from the first three Star Wars movies. The first element of each vector indicates the US box office revenue, the second element refers to the Non-US box office (source: Wikipedia).
> 
> In this exercise, you'll combine all these figures into a single vector. Next, you'll build a matrix from this vector.

3. [Naming a matrix](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#naming-a-matrix)

> To help you remember what is stored in `star_wars_matrix`, you would like to add the names of the movies for the rows. Not only does this help you to read the data, but it is also useful to select certain elements from the matrix.
> 
> Similar to vectors, you can add names for the rows and the columns of a matrix
> ```
> rownames(my_matrix) <- row_names_vector
> colnames(my_matrix) <- col_names_vector
> ```
> We went ahead and prepared two vectors for you: `region`, and `titles`. You will need these vectors to name the columns and rows of `star_wars_matrix`, respectively.

4. [Calculating the worldwide box office](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#calculating-the-worldwide-box-office)

> The single most important thing for a movie in order to become an instant legend in Tinseltown is its worldwide box office figures.
> 
> To calculate the total box office revenue for the three Star Wars movies, you have to take the sum of the US revenue column and the non-US revenue column.
> 
> In R, the function [`rowSums()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/colSums) conveniently calculates the totals for each row of a matrix. This function creates a new vector:
> ```
> rowSums(my_matrix)
> ```

5. [Adding a column for the Worldwide box office](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#adding-a-column-for-the-worldwide-box-office)

> In the previous exercise you calculated the vector that contained the worldwide box office receipt for each of the three Star Wars movies. However, this vector is not yet part of `star_wars_matrix`.
> 
> You can add a column or multiple columns to a matrix with the [`cbind()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/cbind) function, which merges matrices and/or vectors together by column. For example:
> ```
> big_matrix <- cbind(matrix1, matrix2, vector1 ...)
> ```

6. [Adding a row](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#adding-a-row)

> Just like every action has a reaction, every [`cbind()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/cbind) has an [`rbind()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/cbind). (We admit, we are pretty bad with metaphors.)
> 
> Your R workspace, where all variables you defined 'live' ([check out what a workspace is](https://www.statmethods.net/interface/workspace.html)), has already been initialized and contains two matrices:
> 
>   - `star_wars_matrix` that we have used all along, with data on the original trilogy,
>   - `star_wars_matrix2`, with similar data for the prequels trilogy.
> 
> Type the name of these matrices in the console and hit Enter if you want to have a closer look. If you want to check out the contents of the workspace, you can type `ls()` in the console.

7. [The total box office revenue for the entire saga](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#the-total-box-office-revenue-for-the-entire-saga)

> Just like [`cbind()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/cbind) has [`rbind()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/cbind), [`colSums()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/colSums) has [`rowSums()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/colSums). Your R workspace already contains the `all_wars_matrix` that you constructed in the previous exercise; type `all_wars_matrix` to have another look. Let's now calculate the total box office revenue for the entire saga.

8. [Selection of matrix elements](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#selection-of-matrix-elements)

> Similar to vectors, you can use the square brackets `[ ]` to select one or multiple elements from a matrix. Whereas vectors have one dimension, matrices have two dimensions. You should therefore use a comma to separate the rows you want to select from the columns. For example:
> 
>   - `my_matrix[1,2]` selects the element at the first row and second column.
>   - `my_matrix[1:3,2:4]` results in a matrix with the data on the rows 1, 2, 3 and columns 2, 3, 4.
> 
> If you want to select all elements of a row or a column, no number is needed before or after the comma, respectively:
> 
>   - `my_matrix[,1]` selects all elements of the first column.
>   - `my_matrix[1,]` selects all elements of the first row.
> 
> Back to Star Wars with this newly acquired knowledge! As in the previous exercise, `all_wars_matrix` is already available in your workspace.

9. [A little arithmetic with matrices](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#a-little-arithmetic-with-matrices)

> Similar to what you have learned with vectors, the standard operators like `+`, `-`, `/`, `*`, etc. work in an element-wise way on matrices in R.
> 
> For example, `2 * my_matrix` multiplies each element of `my_matrix` by two.
> 
> As a newly-hired data analyst for Lucasfilm, it is your job to find out how many visitors went to each movie for each geographical area. You already have the total revenue figures in `all_wars_matrix`. Assume that the price of a ticket was 5 dollars. Simply dividing the box office numbers by this ticket price gives you the number of visitors.

10. [A little arithmetic with matrices (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#a-little-arithmetic-with-matrices-2)

> Just like `2 * my_matrix` multiplied every element of `my_matrix` by two, `my_matrix1 * my_matrix2` creates a matrix where each element is the product of the corresponding elements in `my_matrix1` and `my_matrix2`.
> 
> After looking at the result of the previous exercise, big boss Lucas points out that the ticket prices went up over time. He asks to redo the analysis based on the prices you can find in `ticket_prices_matrix` (source: imagination).
> 
> *Those who are familiar with matrices should note that this is not the standard matrix multiplication for which you should use `%*%` in R.*


### 4. [Factors](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#4-factors)

Very often, data falls into a limited number of categories. For example, human hair color can be categorized as black/brown/blonde/red/grey/white (and perhaps a few more options for people who dye it). In R, categorical data is stored in factors. Given the importance of these factors in data analysis, you should start learning how to create, subset and compare them now! 

1. [What's a factor and why would you use it?](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#whats-a-factor-and-why-would-you-use-it)

> In this chapter you dive into the wonderful world of **factors**.
> 
> The term factor refers to a statistical data type used to store categorical variables. The difference between a categorical variable and a continuous variable is that a categorical variable can belong to a **limited number of categories**. A continuous variable, on the other hand, can correspond to an infinite number of values.
> 
> It is important that R knows whether it is dealing with a continuous or a categorical variable, as the statistical models you will develop in the future treat both types differently. (You will see later why this is the case.)
> 
> A good example of a categorical variable is sex. In many circumstances you can limit the sex categories to "Male" or "Female". (Sometimes you may need different categories. For example, you may need to consider chromosomal variation, hermaphroditic animals, or different cultural norms, but you will always have a finite number of categories.)

2. [What's a factor and why would you use it? (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#whats-a-factor-and-why-would-you-use-it-2)

> To create factors in R, you make use of the function [`factor()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/factor). First thing that you have to do is create a vector that contains all the observations that belong to a limited number of categories. For example, `sex_vector` contains the sex of 5 different individuals:
> ```
> sex_vector <- c("Male","Female","Female","Male","Male")
> ```
> It is clear that there are two categories, or in R-terms **'factor levels'**, at work here: "Male" and "Female".
> 
> The function [`factor()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/factor) will encode the vector as a factor:
> ```
> factor_sex_vector <- factor(sex_vector)
> ```

3. [What's a factor and why would you use it? (3)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#whats-a-factor-and-why-would-you-use-it-3)

> There are two types of categorical variables: a **nominal categorical variable** and an **ordinal categorical variable**.
> 
> A nominal variable is a categorical variable without an implied order. This means that it is impossible to say that 'one is worth more than the other'. For example, think of the categorical variable `animals_vector` with the categories `"Elephant"`, `"Giraffe"`, `"Donkey"` and `"Horse"`. Here, it is impossible to say that one stands above or below the other. (Note that some of you might disagree ;-) ).
> 
> In contrast, ordinal variables do have a natural ordering. Consider for example the categorical variable `temperature_vector` with the categories: `"Low"`, `"Medium"` and `"High"`. Here it is obvious that `"Medium"` stands above `"Low"`, and `"High"` stands above `"Medium"`

4. [Factor levels](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#factor-levels)

> When you first get a data set, you will often notice that it contains factors with specific factor levels. However, sometimes you will want to change the names of these levels for clarity or other reasons. R allows you to do this with the function [`levels()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/levels):
> ```
> levels(factor_vector) <- c("name1", "name2",...)
> ```
> A good illustration is the raw data that is provided to you by a survey. A common question for every questionnaire is the sex of the respondent. Here, for simplicity, just two categories were recorded, `"M"` and `"F"`. (You usually need more categories for survey data; either way, you use a factor to store the categorical data.)
> ```
> survey_vector <- c("M", "F", "F", "M", "M")
> ```
> Recording the sex with the abbreviations `"M"` and `"F"` can be convenient if you are collecting data with pen and paper, but it can introduce confusion when analyzing the data. At that point, you will often want to change the factor levels to `"Male"` and `"Female"` instead of `"M"` and `"F"` for clarity.
> 
> Watch out: the order with which you assign the levels is important. If you type `levels(factor_survey_vector)`, you'll see that it outputs `[1] "F" "M"`. If you don't specify the levels of the factor when creating the vector, R will automatically assign them alphabetically. To correctly map `"F"` to `"Female"` and `"M"` to `"Male"`, the levels should be set to `c("Female", "Male")`, in this order.

5. [Summarizing a factor](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#summarizing-a-factor)

> After finishing this course, one of your favorite functions in R will be [`summary()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/summary). This will give you a quick overview of the contents of a variable:
> ```
> summary(my_var)
> ```
> Going back to our survey, you would like to know how many `"Male"` responses you have in your study, and how many `"Female"` responses. The [`summary()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/summary) function gives you the answer to this question.

6. [Battle of the sexes](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#battle-of-the-sexes)

> You might wonder what happens when you try to compare elements of a factor. In `factor_survey_vector` you have a factor with two levels: `"Male"` and `"Female"`. But how does R value these relative to each other?

7. [Ordered factors](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#ordered-factors)

> Since `"Male"` and `"Female"` are unordered (or nominal) factor levels, R returns a warning message, telling you that the greater than operator is not meaningful. As seen before, R attaches an equal value to the levels for such factors.
> 
> But this is not always the case! Sometimes you will also deal with factors that do have a natural ordering between its categories. If this is the case, we have to make sure that we pass this information to R...
> 
> Let us say that you are leading a research team of five data analysts and that you want to evaluate their performance. To do this, you track their speed, evaluate each analyst as `"slow"`, `"medium"` or `"fast"`, and save the results in `speed_vector`.

8. [Ordered factors (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#ordered-factors-2)

> `speed_vector` should be converted to an ordinal factor since its categories have a natural ordering. By default, the function [`factor()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/factor) transforms `speed_vector` into an unordered factor. To create an ordered factor, you have to add two additional arguments: `ordered` and `levels`.
> ```
> factor(some_vector,
>        ordered = TRUE,
>        levels = c("lev1", "lev2" ...))
> ```
> By setting the argument `ordered` to `TRUE` in the function [`factor()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/factor), you indicate that the factor is ordered. With the argument `levels` you give the values of the factor in the correct order.

9. [Comparing ordered factors](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#comparing-ordered-factors)

> Having a bad day at work, 'data analyst number two' enters your office and starts complaining that 'data analyst number five' is slowing down the entire project. Since you know that 'data analyst number two' has the reputation of being a smarty-pants, you first decide to check if his statement is true.
> 
> The fact that `factor_speed_vector` is now ordered enables us to compare different elements (the data analysts in this case). You can simply do this by using the well-known operators.


### 5. [Data frames](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#5-data-frames)

Most data sets you will be working with will be stored as data frames. By the end of this chapter focused on R basics, you will be able to create a data frame, select interesting parts of a data frame and order a data frame according to certain variables. 

1. [What's a data frame?](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#whats-a-data-frame)

> You may remember from the chapter about matrices that all the elements that you put in a matrix should be of the same type. Back then, your data set on Star Wars only contained numeric elements.
> 
> When doing a market research survey, however, you often have questions such as:
> 
>   - 'Are you married?' or 'yes/no' questions (`logical`)
>   - 'How old are you?' (`numeric`)
>   - 'What is your opinion on this product?' or other 'open-ended' questions (`character`)
>   - ...
> 
> The output, namely the respondents' answers to the questions formulated above, is a data set of different data types. You will often find yourself working with data sets that contain different data types instead of only one.
> 
> A data frame has the variables of a data set as columns and the observations as rows. This will be a familiar concept for those coming from different statistical software packages such as SAS or SPSS.

2. [Quick, have a look at your data set](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#quick-have-a-look-at-your-data-set)

> Wow, that is a lot of cars!
> 
> Working with large data sets is not uncommon in data analysis. When you work with (extremely) large data sets and data frames, your first task as a data analyst is to develop a clear understanding of its structure and main elements. Therefore, it is often useful to show only a small part of the entire data set.
> 
> So how to do this in R? Well, the function [`head()`](https://www.rdocumentation.org/packages/utils/versions/3.5.2/topics/head) enables you to show the first observations of a data frame. Similarly, the function [`tail()`](https://www.rdocumentation.org/packages/utils/versions/3.5.2/topics/head) prints out the last observations in your data set.
> 
> Both [`head()`](https://www.rdocumentation.org/packages/utils/versions/3.5.2/topics/head) and [`tail()`](https://www.rdocumentation.org/packages/utils/versions/3.5.2/topics/head) print a top line called the 'header', which contains the names of the different variables in your data set.

3. [Have a look at the structure](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#have-a-look-at-the-structure)

> Another method that is often used to get a rapid overview of your data is the function [`str()`](https://www.rdocumentation.org/packages/utils/versions/3.5.2/topics/str). The function [`str()`](https://www.rdocumentation.org/packages/utils/versions/3.5.2/topics/str) shows you the structure of your data set. For a data frame it tells you:
> 
>   - The total number of observations (e.g. 32 car types)
>   - The total number of variables (e.g. 11 car features)
>   - A full list of the variables names (e.g. `mpg`, `cyl` ... )
>   - The data type of each variable (e.g. `num`)
>   - The first observations
> 
> Applying the [`str()`](https://www.rdocumentation.org/packages/utils/versions/3.5.2/topics/str) function will often be the first thing that you do when receiving a new data set or data frame. It is a great way to get more insight in your data set before diving into the real analysis.

4. [Creating a data frame](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#creating-a-data-frame)

> Since using built-in data sets is not even half the fun of creating your own data sets, the rest of this chapter is based on your personally developed data set. Put your jet pack on because it is time for some space exploration!
> 
> As a first goal, you want to construct a data frame that describes the main characteristics of eight planets in our solar system. According to your good friend Buzz, the main features of a planet are:
> 
>   - The type of planet (Terrestrial or Gas Giant).
>   - The planet's diameter relative to the diameter of the Earth.
>   - The planet's rotation across the sun relative to that of the Earth.
>   - If the planet has rings or not (TRUE or FALSE).
> 
> After doing some high-quality research on [Wikipedia](https://en.wikipedia.org/wiki/Planet), you feel confident enough to create the necessary vectors: `name`, `type`, `diameter`, `rotation` and `rings`; these vectors have already been coded up on the right. The first element in each of these vectors correspond to the first observation.
> 
> You construct a data frame with the [`data.frame()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/data.frame) function. As arguments, you pass the vectors from before: they will become the different columns of your data frame. Because every column has the same length, the vectors you pass should also have the same length. But don't forget that it is possible (and likely) that they contain different types of data.

5. [Creating a data frame (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#creating-a-data-frame-2)

> The `planets_df` data frame should have 8 observations and 5 variables. It has been made available in the workspace, so you can directly use it.

6. [Selection of data frame elements](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#selection-of-data-frame-elements)

> Similar to vectors and matrices, you select elements from a data frame with the help of square brackets `[ ]`. By using a comma, you can indicate what to select from the rows and the columns respectively. For example:
> 
>   - `my_df[1,2]` selects the value at the first row and second column in `my_df`.
>   - `my_df[1:3,2:4]` selects rows 1, 2, 3 and columns 2, 3, 4 in `my_df`.
> 
> Sometimes you want to select all elements of a row or column. For example, `my_df[1, ]` selects all elements of the first row. Let us now apply this technique on `planets_df`!

7. [Selection of data frame elements (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#selection-of-data-frame-elements-2)

> Instead of using numerics to select elements of a data frame, you can also use the variable names to select columns of a data frame.
> 
> Suppose you want to select the first three elements of the `type` column. One way to do this is
> ```
> planets_df[1:3,2]
> ```
> A possible disadvantage of this approach is that you have to know (or look up) the column number of `type`, which gets hard if you have a lot of variables. It is often easier to just make use of the variable name:
> ```
> planets_df[1:3,"type"]
> ```

8. [Only planets with rings](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#only-planets-with-rings)

> You will often want to select an entire column, namely one specific variable from a data frame. If you want to select all elements of the variable `diameter`, for example, both of these will do the trick:
> ```
> planets_df[,3]
> planets_df[,"diameter"]
> ```
> However, there is a short-cut. If your columns have names, you can use the `$` sign:
> ```
> planets_df$diameter
> ```

9. [Only planets with rings (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#only-planets-with-rings-2)

> You probably remember from high school that some planets in our solar system have rings and others do not. Unfortunately you can not recall their names. Could R help you out?
> 
> If you type `rings_vector` in the console, you get:
> ```
> [1] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
> ```
> This means that the first four observations (or planets) do not have a ring (`FALSE`), but the other four do (`TRUE`). However, you do not get a nice overview of the names of these planets, their diameter, etc. Let's try to use `rings_vector` to select the data for the four planets with rings.

10. [Only planets with rings but shorter](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#only-planets-with-rings-but-shorter)

> So what exactly did you learn in the previous exercises? You selected a subset from a data frame (`planets_df`) based on whether or not a certain condition was true (rings or no rings), and you managed to pull out all relevant data. Pretty awesome! By now, NASA is probably already flirting with your CV ;-).
> 
> Now, let us move up one level and use the function [`subset()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/subset). You should see the [`subset()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/subset) function as a short-cut to do exactly the same as what you did in the previous exercises.
> ```
> subset(my_df, subset = some_condition)
> ```
> The first argument of [`subset()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/subset) specifies the data set for which you want a subset. By adding the second argument, you give R the necessary information and conditions to select the correct subset.
> 
> The code below will give the exact same result as you got in the previous exercise, but this time, you didn't need the `rings_vector`!
> ```
> subset(planets_df, subset = rings)
> ```

11. [Sorting](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#sorting)

> Making and creating rankings is one of mankind's favorite affairs. These rankings can be useful (best universities in the world), entertaining (most influential movie stars) or pointless (best 007 look-a-like).
> 
> In data analysis you can sort your data according to a certain variable in the data set. In R, this is done with the help of the function [`order()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/order).
> 
> [`order()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/order) is a function that gives you the ranked position of each element when it is applied on a variable, such as a vector for example:
> ```
> > a <- c(100, 10, 1000)
> > order(a)
> [1] 2 1 3
> ```
> 10, which is the second element in `a`, is the smallest element, so 2 comes first in the output of `order(a)`. 100, which is the first element in `a` is the second smallest element, so 1 comes second in the output of `order(a)`.
> 
> This means we can use the output of `order(a)` to reshuffle `a`:
> ```
> > a[order(a)]
> [1]   10  100 1000
> ```

12. [Sorting your data frame](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#sorting-your-data-frame)

> Alright, now that you understand the [`order()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/order) function, let us do something useful with it. You would like to rearrange your data frame such that it starts with the smallest planet and ends with the largest one. A sort on the `diameter` column.


### 6. [Lists](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#6-lists)

Lists, as opposed to vectors, can hold components of different types, just like your to-do list at home or at work. This intro to R chapter will teach you how to create, name and subset these lists. 

1. [Lists, why would you need them?](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#lists-why-would-you-need-them)

> Congratulations! At this point in the course you are already familiar with:
> 
>   - **Vectors** (one dimensional array): can hold numeric, character or logical values. The elements in a vector all have the same data type.
>   - **Matrices** (two dimensional array): can hold numeric, character or logical values. The elements in a matrix all have the same data type.
>   - **Data frames** (two-dimensional objects): can hold numeric, character or logical values. Within a column all elements have the same data type, but different columns can be of different data type.
> 
> Pretty sweet for an R newbie, right? ;-)

2. [Lists, why would you need them? (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#lists-why-would-you-need-them-2)

> A **list** in R is similar to your to-do list at work or school: the different items on that list most likely differ in length, characteristic, and type of activity that has to be done.
> 
> A list in R allows you to gather a variety of objects under one name (that is, the name of the list) in an ordered way. These objects can be matrices, vectors, data frames, even other lists, etc. It is not even required that these objects are related to each other in any way.
> 
> You could say that a list is some kind super data type: you can store practically any piece of information in it!

3. [Creating a list](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#creating-a-list)

> Let us create our first list! To construct a list you use the function [`list()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/list):
> ```
> my_list <- list(comp1, comp2 ...)
> ```
> The arguments to the list function are the list components. Remember, these components can be matrices, vectors, other lists, ...

4. [Creating a named list](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#creating-a-named-list)

> Well done, you're on a roll!
> 
> Just like on your to-do list, you want to avoid not knowing or remembering what the components of your list stand for. That is why you should give names to them:
> ```
> my_list <- list(name1 = your_comp1, 
>                 name2 = your_comp2)
> ```
> This creates a list with components that are named `name1`, `name2`, and so on. If you want to name your lists after you've created them, you can use the `names()` function as you did with vectors. The following commands are fully equivalent to the assignment above:
> ```
> my_list <- list(your_comp1, your_comp2)
> names(my_list) <- c("name1", "name2")
> ```

5. [Creating a named list (2)](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#creating-a-named-list-2)

> Being a huge movie fan (remember your job at LucasFilms), you decide to start storing information on good movies with the help of lists.
> 
> Start by creating a list for the movie "The Shining". We have already created the variables `mov`, `act` and `rev` in your R workspace. Feel free to check them out in the console.

6. [Selecting elements from a list](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#selecting-elements-from-a-list)

> Your list will often be built out of numerous elements and components. Therefore, getting a single element, multiple elements, or a component out of it is not always straightforward.
> 
> One way to select a component is using the numbered position of that component. For example, to "grab" the first component of `shining_list` you type
> ```
> shining_list[[1]]
> ```
> A quick way to check this out is typing it in the console. Important to remember: to select elements from vectors, you use single square brackets: `[ ]`. Don't mix them up!
> 
> You can also refer to the names of the components, with `[[ ]]` or with the `$` sign. Both will select the data frame representing the reviews:
> ```
> shining_list[["reviews"]]
> shining_list$reviews
> ```
> Besides selecting components, you often need to select specific elements out of these components. For example, with `shining_list[[2]][1]` you select from the second component, `actors` (`shining_list[[2]]`), the first element (`[1]`). When you type this in the console, you will see the answer is Jack Nicholson.

7. [Adding more movie information to the list](https://github.com/Delimain/DataCamp_Exercises/blob/master/Introduction_to_R/Introduction_to_R_Exercises.md#adding-more-movie-information-to-the-list)

> Being proud of your first list, you shared it with the members of your movie hobby club. However, one of the senior members, a guy named M. McDowell, noted that you forgot to add the release year. Given your ambitions to become next year's president of the club, you decide to add this information to the list.
> 
> To conveniently add elements to lists you can use the [`c()`](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/c) function, that you also used to build vectors:
> ```
> ext_list <- c(my_list , my_val)
> ```
> This will simply extend the original list, `my_list`, with the component `my_val`. This component gets appended to the end of the list. If you want to give the new list item a name, you just add the name as you did before:
> ```
> ext_list <- c(my_list, my_name = my_val)
> ```
