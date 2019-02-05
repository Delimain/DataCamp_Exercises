**Note**: At the time of writing, all the exercises herein are offered on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource. The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Correlation and Regression](https://www.datacamp.com/courses/correlation-and-regression)

# 1. Visualizing two variables

## Scatterplots
```
# Scatterplot of weight vs. weeks
ggplot(ncbirths, aes(x = weeks, y = weight)) +
  geom_point()
```
## Boxplots as discretized/conditioned scatterplots
```
# Boxplot of weight vs. weeks
ggplot(data = ncbirths, 
       aes(x = cut(weeks, breaks = 5), y = weight)) + 
  geom_boxplot()
```
## Creating scatterplots
```
# Mammals scatterplot
ggplot(mammals, aes(x = BodyWt, y = BrainWt)) +
  geom_point()

# Baseball player scatterplot
ggplot(mlbBat10, aes(x = OBP, y = SLG)) +
  geom_point()

# Body dimensions scatterplot
ggplot(bdims, aes(x = hgt, y = wgt, color = factor(sex))) +
  geom_point()

# Smoking scatterplot
ggplot(smoking, aes(x = age, y = amtWeekdays)) +
  geom_point()
```
## Transformations
```
# Scatterplot with coord_trans()
ggplot(data = mammals, aes(x = BodyWt, y = BrainWt)) +
  geom_point() + 
  coord_trans(x = "log10", y = "log10")

# Scatterplot with scale_x_log10() and scale_y_log10()
ggplot(data = mammals, aes(x = BodyWt, y = BrainWt)) +
  geom_point() +
  scale_x_log10() + 
  scale_y_log10()
```
## Identifying outliers
```
# Scatterplot of SLG vs. OBP
mlbBat10 %>%
  filter(AB >= 200) %>%
  ggplot(aes(x = OBP, y = SLG)) +
  geom_point()

# Identify the outlying player
mlbBat10 %>%
  filter(AB >= 200, OBP < 0.200)
```


# 2. Correlation

## Computing correlation
```
# Compute correlation
ncbirths %>%
  summarize(N = n(), r = cor(weight, mage))

# Compute correlation for all non-missing pairs
ncbirths %>%
  summarize(N = n(), r = cor(weight, weeks, use = "pairwise.complete.obs"))
```
## Exploring Anscombe
```
# Compute properties of Anscombe
Anscombe %>%
  group_by(set) %>%
  summarize(N = n(), mean(x), sd(x), mean(y), sd(y), cor(x, y))
```
## Perception of correlation (2)
```
# Correlation for all baseball players
mlbBat10 %>%
  summarize(N = n(), r = cor(OBP, SLG))

# Correlation for all players with at least 200 ABs
mlbBat10 %>%
  filter(AB >= 200) %>%
  summarize(N = n(), r = cor(OBP, SLG))

# Correlation of body dimensions
bdims %>%
  group_by(sex) %>%
  summarize(N = n(), r = cor(hgt, wgt))

# Correlation among mammals, with and without log
mammals %>%
  summarize(N = n(), 
            r = cor(BodyWt, BrainWt), 
            r_log = cor(log(BodyWt), log(BrainWt)))
```
## Spurious correlation in random data
```
# Create faceted scatterplot
ggplot(noise, aes(x = x, y = y)) +
  geom_point() +
  facet_wrap(~ z)

# Compute correlations for each dataset
noise_summary <- noise %>%
  group_by(z) %>%
  summarize(N = n(), spurious_cor = cor(x, y))

# Isolate sets with correlations above 0.2 in absolute strength
noise_summary %>%
  filter(abs(spurious_cor) > 0.2)
```


# 3. Simple linear regression 

## The "best fit" line
```
# Scatterplot with regression line
ggplot(data = bdims, aes(x = hgt, y = wgt)) + 
  geom_point() + 
  geom_smooth(method = "lm", se = FALSE)
```
## Uniqueness of least squares regression line
```
# Estimate optimal value of my_slope
add_line(my_slope = 1)
```
## Fitting a linear model "by hand"
```
# Print bdims_summary
bdims_summary

# Add slope and intercept
bdims_summary %>%
  mutate(slope = r * (sd_wgt / sd_hgt), 
         intercept = mean_wgt - (slope * mean_hgt))
```
## Regression to the mean
```
# Height of children vs. height of father
ggplot(data = Galton_men, aes(x = father, y = height)) +
  geom_point() + 
  geom_abline(slope = 1, intercept = 0) + 
  geom_smooth(method = "lm", se = FALSE)

# Height of children vs. height of mother
ggplot(data = Galton_women, aes(x = mother, y = height)) +
  geom_point() +
  geom_abline(slope = 1, intercept = 0) +
  geom_smooth(method = "lm", se = FALSE)
```


# 4. Interpreting regression models 

## Fitting simple linear models
```
# Linear model for weight as a function of height
lm(wgt ~ hgt, data = bdims)

# Linear model for SLG as a function of OBP
lm(SLG ~ OBP, data = mlbBat10)

# Log-linear model for body weight as a function of brain weight
lm(log(BodyWt) ~ log(BrainWt), data = mammals)
```
## The lm summary output
```
# Show the coefficients
coef(mod)

# Show the full output
summary(mod)
```
## Fitted values and residuals
```
# Mean of weights equal to mean of fitted values?
mean(bdims$wgt) == mean(fitted.values(mod))

# Mean of the residuals
mean(residuals(mod))
```
## Tidying your linear model
```
# Load broom
library(broom)

# Create bdims_tidy
bdims_tidy <- augment(mod)

# Glimpse the resulting data frame
glimpse(bdims_tidy)
```
## Making predictions
```
# Print ben
ben

# Predict the weight of ben
predict(mod, newdata = ben)
```
## Adding a regression line to a plot manually
```
# Add the line to the scatterplot
ggplot(data = bdims, aes(x = hgt, y = wgt)) + 
  geom_point() + 
  geom_abline(data = coefs, 
              aes(intercept = `(Intercept)`, slope = `hgt`),  
              color = "dodgerblue")
```


# 5. Model Fit

## Standard error of residuals
```
# View summary of model
summary(mod)

# Compute the mean of the residuals
mean(residuals(mod))

# Compute RMSE
sqrt(sum(residuals(mod) ^ 2) / df.residual(mod))
```
## Assessing simple linear model fit
```
# View model summary
summary(mod)

# Compute R-squared
bdims_tidy %>%
  summarize(var_y = var(wgt), var_e = var(.resid)) %>%
  mutate(R_squared = 1 - (var_e / var_y))
```
## Linear vs. average
```
# Compute SSE for null model
mod_null %>%
  summarize(SSE = var(.resid))

# Compute SSE for regression model
mod_hgt %>%
  summarize(SSE = var(.resid))
```
## Leverage
```
# Rank points of high leverage
mod %>%
  augment() %>%
  arrange(desc(.hat)) %>%
  head()
```
## Influence
```
# Rank influential points
mod %>%
  augment() %>%
  arrange(desc(.cooksd)) %>%
  head()
```
## Removing outliers
```
# Create nontrivial_players
nontrivial_players <- mlbBat10 %>%
  filter(AB >= 10 & OBP < 0.500)

# Fit model to new data
mod_cleaner <- lm(SLG ~ OBP, data = nontrivial_players)

# View model summary
summary(mod_cleaner)

# Visualize new model
ggplot(nontrivial_players, aes(x = OBP, y = SLG)) +
  geom_point() +
  geom_smooth(method = "lm")
```
## High leverage points
```
# Rank high leverage points
mod %>%
  augment() %>%
  arrange(desc(.hat), .cooksd) %>%
  head()
```
