**Note**: At the time of writing, all the exercises herein are offered on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource. The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Multiple and Logistic Regression](https://www.datacamp.com/courses/multiple-and-logistic-regression)

# 1. Parallel Slopes

## Fitting a parallel slopes model
```
# Explore the data
str(mario_kart)

# fit parallel slopes
lm(totalPr ~ wheels + cond, data = mario_kart)
```
## Using geom_line() and augment()
```
# Augment the model
augmented_mod <- augment(mod)
glimpse(augmented_mod)

# scatterplot, with color
data_space <- ggplot(augmented_mod, aes(x = wheels, y = totalPr, color = cond)) +
  geom_point()
  
# single call to geom_line()
data_space + 
  geom_line(aes(y = .fitted))
```
## Syntax from math
```
# build model
lm(bwt ~ age + parity, data = babies)
```
## Syntax from plot
```
# build model
lm(bwt ~ gestation + smoke, data = babies)
```


# 2. Evaluating and extending parallel slopes model 

## R-squared vs. adjusted R-squared
```
# R^2 and adjusted R^2
summary(mod)

# add random noise
mario_kart_noisy <- mario_kart %>%
  mutate(noise = rnorm(nrow(mario_kart)))
  
# compute new model
mod2 <- lm(totalPr ~ wheels + cond + noise, data = mario_kart_noisy)

# new R^2 and adjusted R^2
summary(mod2)
```
## Prediction
```
# return a vector
predict(mod)

# return a data frame
augment(mod)
```
## Fitting a model with interaction
```
# include interaction
lm(totalPr ~ cond + duration + cond:duration, data = mario_kart)
```
## Visualizing interaction models
```
# interaction plot
ggplot(mario_kart, aes(x = duration, y = totalPr, color = cond)) + 
  geom_point() + 
  geom_smooth(method = "lm", se = FALSE)
```
## Simpson's paradox in action
```
slr <- ggplot(mario_kart, aes(y = totalPr, x = duration)) + 
  geom_point() + 
  geom_smooth(method = "lm", se = 0)

# model with one slope
lm(totalPr ~ duration, data = mario_kart)

# plot with two slopes
slr + aes(color = cond)
```


# 3. Multiple Regression 

## Fitting a MLR model
```
# Fit the model using duration and startPr
lm(totalPr ~ duration + startPr, data = mario_kart)
```
## Tiling the plane
```
# add predictions to grid
price_hats <- augment(mod, newdata = grid)

# tile the plane
data_space + 
  geom_tile(data = price_hats, aes(fill = .fitted), alpha = 0.5)
```
## Models in 3D
```
# draw the 3D scatterplot
p <- plot_ly(data = mario_kart, z = ~totalPr, x = ~duration, y = ~startPr, opacity = 0.6) %>%
  add_markers() 
  
# draw the plane
p %>%
  add_surface(x = ~x, y = ~y, z = ~plane, showscale = FALSE)
```
## Visualizing parallel planes
```
# draw the 3D scatterplot
p <- plot_ly(data = mario_kart, z = ~totalPr, x = ~duration, y = ~startPr, opacity = 0.6) %>%
  add_markers(color = ~cond) 
  
# draw two planes
p %>%
  add_surface(x = ~x, y = ~y, z = ~plane0, showscale = FALSE) %>%
  add_surface(x = ~x, y = ~y, z = ~plane1, showscale = FALSE)
```


# 4. Logistic Regression 

## Fitting a line to a binary response
```
# scatterplot with jitter
data_space <- ggplot(MedGPA, aes(x = GPA, y = Acceptance)) + 
  geom_jitter(width = 0, height = 0.05, alpha = 0.5)

# linear regression line
data_space + 
  geom_smooth(method = "lm", se = FALSE)
```
## Fitting a line to a binary response (2)
```
# filter
MedGPA_middle <- filter(MedGPA, GPA <= 3.77, GPA >= 3.375)

# scatterplot with jitter
data_space <- ggplot(MedGPA_middle, aes(x = GPA, y = Acceptance)) + 
  geom_jitter(width = 0, height = 0.05, alpha = 0.5)

# linear regression line
data_space + 
  geom_smooth(method = "lm", se = FALSE)
```
## Fitting a model
```
# fit model
glm(Acceptance ~ GPA, data = MedGPA, family = binomial)
```
## Using geom_smooth()
```
# scatterplot with jitter
data_space <- ggplot(MedGPA, aes(x = GPA, y = Acceptance)) + 
  geom_jitter(width = 0, height = 0.05, alpha = .5)

# add logistic curve
data_space +
  geom_smooth(method = "glm", method.args = list(family = "binomial"), se = FALSE)
```
## Using bins
```
# binned points and line
data_space <- ggplot(MedGPA_binned, aes(x = mean_GPA, y = acceptance_rate)) +
  geom_point() +
  geom_line()

# augmented model
MedGPA_plus <- augment(mod, type.predict = "response")

# logistic model on probability scale
data_space +
  geom_line(data = MedGPA_plus, aes(x = GPA, y = .fitted), color = "red")
```
## Odds scale
```
# compute odds for bins
MedGPA_binned <- mutate(MedGPA_binned, odds = acceptance_rate / (1 - acceptance_rate))

# plot binned odds
data_space <- ggplot(MedGPA_binned, aes(x = mean_GPA, y = odds)) +
  geom_point() +
  geom_line()

# compute odds for observations
MedGPA_plus <- mutate(MedGPA_plus, odds_hat = .fitted / (1 - .fitted))

# logistic model on odds scale
data_space +
  geom_line(data = MedGPA_plus, aes(x = GPA, y = odds_hat), color = "red")
```
## Log-odds scale
```
# compute log odds for bins
MedGPA_binned <- mutate(MedGPA_binned, log_odds = log(acceptance_rate / (1 - acceptance_rate)))

# plot binned log odds
data_space <- ggplot(MedGPA_binned, aes(x = mean_GPA, y = log_odds)) +
  geom_point() +
  geom_line()

# compute log odds for observations
MedGPA_plus <- mutate(MedGPA_plus, log_odds_hat = log(.fitted / (1 - .fitted)))

# logistic model on log odds scale
data_space +
  geom_line(data = MedGPA_plus, aes(x = GPA, y = log_odds_hat), color = "red")
```
## Making probabilistic predictions
```
# create new data frame
new_data <- data.frame(GPA = 3.51)

# make predictions
augment(mod, newdata = new_data, type.predict = "response")
```
## Making binary predictions
```
# data frame with binary predictions
tidy_mod <- augment(mod, type.predict = "response") %>%
  mutate(Acceptance_hat = round(.fitted))
  
# confusion matrix
tidy_mod %>%
  select(Acceptance, Acceptance_hat) %>% 
  table()
```


# 5. Case Study: Italian restaurants in NYC 

## SLR models
```
# Price by Food plot
ggplot(nyc, aes(x = Food, y = Price)) +
  geom_point()

# Price by Food model
lm(Price ~ Food, data = nyc)
```
## A plane in 3D
```
# fit model
lm(Price ~ Food + Service, data = nyc)

# draw 3D scatterplot
p <- plot_ly(data = nyc, z = ~Price, x = ~Food, y = ~Service, opacity = 0.6) %>%
  add_markers() 

# draw a plane
p %>%
  add_surface(x = ~x, y = ~y, z = ~plane, showscale = FALSE) 
```
## Parallel planes with location
```
# Price by Food and Service and East
lm(Price ~ Food + Service + East, data = nyc)
```
## Impact of location
```
# draw 3D scatterplot
p <- plot_ly(data = nyc, z = ~Price, x = ~Food, y = ~Service, opacity = 0.6) %>%
  add_markers(color = ~factor(East)) 

# draw two planes
p %>%
  add_surface(x = ~x, y = ~y, z = ~plane0, showscale = FALSE) %>%
  add_surface(x = ~x, y = ~y, z = ~plane1, showscale = FALSE)
```
