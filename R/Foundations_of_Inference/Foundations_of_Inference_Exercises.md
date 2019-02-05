**Note**: At the time of writing, all the exercises herein are offered on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource. The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Foundations of Inference](https://www.datacamp.com/courses/foundations-of-inference)

# 1. Introduction to ideas of inference

## Working with the NHANES data
```
# Load packages
library(ggplot2)
library(NHANES)

# What are the variables in the NHANES dataset?
colnames(NHANES)

# Create bar plot for Home Ownership by Gender
ggplot(NHANES, aes(x = Gender, fill = HomeOwn)) + 
  # Set the position to fill
  geom_bar(position = "fill") +
  ylab("Relative frequencies")
  
# Density plot of SleepHrsNight colored by SleepTrouble
ggplot(NHANES, aes(x = SleepHrsNight, color = SleepTrouble)) + 
  # Adjust by 2
  geom_density(adjust = 2) + 
  # Facet by HealthGen
  facet_wrap(~ HealthGen)
```
## Calculating statistic of interest
```
homes <- NHANES %>%
  # Select Gender and HomeOwn
  select(Gender, HomeOwn) %>%
  # Filter for HomeOwn equal to "Own" or "Rent"
  filter(HomeOwn %in% c("Own", "Rent"))
  
diff_orig <- homes %>%   
  # Group by gender
  group_by(Gender) %>%
  # Summarize proportion of homeowners
  summarize(prop_own = mean(HomeOwn == "Own")) %>%
  # Summarize difference in proportion of homeowners
  mutate(obs_diff_prop = diff(prop_own)) # male - female
```
## Randomized data under null model of independence
```
# Specify variables
homeown_perm <- homes %>%
  specify(HomeOwn ~ Gender, success = "Own")

# Print results to console
homeown_perm

# Hypothesize independence
homeown_perm <- homes %>%
  specify(HomeOwn ~ Gender, success = "Own") %>%
  hypothesize(null = "independence")  

# Print results to console
homeown_perm

# Perform 10 permutations
homeown_perm <- homes %>%
  specify(HomeOwn ~ Gender, success = "Own") %>%
  hypothesize(null = "independence") %>% 
  generate(reps = 10, type = "permute") 


# Print results to console
homeown_perm
```
## Randomized statistics and dotplot
```
# Perform 100 permutations
homeown_perm <- homes %>%
  specify(HomeOwn ~ Gender, success = "Own") %>%
  hypothesize(null = "independence") %>% 
  generate(reps = 100, type = "permute") %>% 
  calculate(stat = "diff in props", order = c("male", "female"))
  
# Print results to console
homeown_perm

# Dotplot of 100 permuted differences in proportions
ggplot(homeown_perm, aes(x = stat)) + 
  geom_dotplot(binwidth = 0.001)
```
## Randomization density
```
# Perform 1000 permutations
homeown_perm <- homes %>%
  # Specify HomeOwn vs. Gender, with `"Own" as success
  specify(HomeOwn ~ Gender, success = "Own") %>%
  # Use a null hypothesis of independence
  hypothesize(null = "independence") %>% 
  # Generate 1000 repetitions (by permutation)
  generate(reps = 1000, type = "permute") %>% 
  # Calculate the difference in proportions (male then female)
  calculate(stat = "diff in props", order = c("male", "female"))

# Density plot of 1000 permuted differences in proportions
ggplot(homeown_perm, aes(x = stat)) + 
  geom_density()
```
## Do the data come from the population?
```
# Plot permuted differences, diff_perm
ggplot(homeown_perm, aes(x = diff_perm)) + 
  # Add a density layer
  geom_density() +
  # Add a vline layer with intercept diff_orig
  geom_vline(aes(xintercept = diff_orig), color = "red")

# Compare permuted differences to observed difference
homeown_perm %>%
  summarize(n_perm_le_obs = sum(diff_perm <= diff_orig))
```


# 2. Completing a randomization test: gender discrimination 

## Summarizing gender discrimination
```
disc %>%
  # Count the rows by promote and sex
  count(promote, sex)

# Find proportion of each sex who were promoted
disc %>%
  # Group by sex
  group_by(sex) %>%
  # Calculate proportion promoted summary stat
  summarize(promoted_prop = mean(promote == "promoted"))
```
## Step-by-step through the permutation
```
# Replicate the entire data frame, permuting the promote variable
disc_perm <- disc %>%
  specify(promote ~ sex, success = "promoted") %>%
  hypothesize(null = "independence") %>%
  generate(reps = 5, type = "permute")

disc_perm %>%
  # Group by replicate
  group_by(replicate) %>%
  # Count per group
  count(promote, sex)

disc_perm %>%
  # Calculate difference in proportion, male then female
  calculate(stat = "diff in props", order = c("male", "female"))
```
## Randomizing gender discrimination
```
# From previous steps
diff_orig <- disc %>%
  group_by(sex) %>%
  summarize(prop_prom = mean(promote == "promoted")) %>%
  summarize(stat = diff(prop_prom)) %>% 
  pull()
disc_perm <- disc %>%
  specify(promote ~ sex, success = "promoted") %>%
  hypothesize(null = "independence") %>%
  generate(reps = 1000, type = "permute") %>%
  calculate(stat = "diff in props", order = c("male", "female"))
  
# Using permutation data, plot stat
ggplot(disc_perm, aes(x = stat)) + 
  # Add a histogram layer
  geom_histogram(binwidth = 0.01) +
  # Add a vertical line at diff_orig
  geom_vline(aes(xintercept = diff_orig), color = "red")
```
## Critical region
```
disc_perm %>% 
  summarize(
    # Find the 0.9 quantile of diff_perm's stat
    q.90 = quantile(stat, p = 0.9),
    # ... and the 0.95 quantile
    q.95 = quantile(stat, p = 0.95),
    # ... and the 0.99 quantile
    q.99 = quantile(stat, p = 0.99)
  )
```
## Two-sided critical region
```
# Use disc_perm
disc_perm %>% 
  # ... to calculate summary stats
  summarize(
    # Find the 0.01 quantile of stat
    q.01 = quantile(stat, p = 0.01),
    # ... and 0.05
    q.05 = quantile(stat, p = 0.05),
    # ... and 0.1 
    q.10 = quantile(stat, p = 0.1)
  )
```
## Sample size in randomization distribution
```
# Tabulate the small dataset
disc_small %>% 
  # Select sex and promote
  count(sex, promote)
  
# Do the same for disc_big
disc_big %>% 
  count(sex, promote)
  
# Using disc_perm_small, plot stat
ggplot(disc_perm_small, aes(x = stat)) + 
  # Add a histogram layer with binwidth 0.01
  geom_histogram(binwidth = 0.01) +
  # Add a vline layer, crossing x-axis at diff_orig_small
  geom_vline(aes(xintercept = diff_orig_small), color = "red")
  
# Swap the dataset to disc_perm_big
ggplot(disc_perm_big, aes(x = stat)) + 
  geom_histogram(binwidth = 0.01) +
  # Change the x-axis intercept to diff_orig_big
  geom_vline(aes(xintercept = diff_orig_big), color = "red")
```
## Sample size for critical region
```
calc_upper_quantiles <- function(dataset) {
  dataset %>% 
    summarize(
      q.90 = quantile(stat, p = 0.90),
      q.95 = quantile(stat, p = 0.95),
      q.99 = quantile(stat, p = 0.99)
    )
}

# Recall the quantiles associated with the original dataset
calc_upper_quantiles(disc_perm)

# Calculate the quantiles associated with the small dataset
calc_upper_quantiles(disc_perm_small)

# Calculate the quantiles associated with the big dataset
calc_upper_quantiles(disc_perm_big)
```
## Calculating the p-values
```
# Visualize and calculate the p-value for the original dataset
disc_perm %>%
  visualize(obs_stat = diff_orig, direction = "greater")

disc_perm %>%
  get_p_value(obs_stat = diff_orig, direction = "greater")

# Visualize and calculate the p-value for the small dataset
disc_perm_small %>%
  visualize(obs_stat = diff_orig_small, direction = "greater")

disc_perm_small %>%
  get_p_value(obs_stat = diff_orig_small, direction = "greater")

# Visualize and calculate the p-value for the original dataset
disc_perm_big %>%
  visualize(obs_stat = diff_orig_big, direction = "greater")

disc_perm_big %>%
  get_p_value(obs_stat = diff_orig_big, direction = "greater")
```
## Practice calculating p-values
```
# Recall the original data
disc %>% 
  count(sex, promote)

# Tabulate the new data
disc_new %>%
  count(sex, promote)
  
# Recall the distribution of the original permuted differences
ggplot(disc_perm, aes(x = stat)) + 
  geom_histogram() +
  geom_vline(aes(xintercept = diff_orig), color = "red")

# Plot the distribution of the new permuted differences
ggplot(disc_perm_new, aes(x = stat)) + 
  geom_histogram() +
  geom_vline(aes(xintercept = diff_orig_new), color = "red")
  
# Recall the p-value from the original data
disc_perm %>%
  summarize(p_value = mean(diff_orig <= stat))

# Find the p-value from the new data
disc_perm_new %>%
  summarize(p_value = mean(diff_orig_new <= stat))
```
## Calculating two-sided p-values
```
# Calculate the two-sided p-value
disc_perm %>%
  summarize(p_value = 2 * mean(diff_orig <= stat))
```


# 3. Hypothesis testing errors: opportunity cost 

## Summarizing opportunity cost (1)
```
# Tabulate the data
opportunity %>%
  count(decision, group)

# Find the proportion who bought the DVD in each group
opportunity %>%
  group_by(group) %>%
  summarize(buy_prop = mean(decision == "buyDVD"))
```
## Plotting opportunity cost
```
# Plot group, filled by decision
ggplot(opportunity, aes(x = group, fill = decision)) + 
  # Add a bar layer, with position "fill"
  geom_bar(position = "fill")
```
## Randomizing opportunity cost
```
# From previous steps
diff_obs <- opportunity %>%
  group_by(group) %>%
  summarize(prop_buy = mean(decision == "buyDVD")) %>%
  summarize(stat = diff(prop_buy)) %>% 
  pull()
opp_perm <- opportunity %>%
  specify(decision ~ group, success = "buyDVD") %>%
  hypothesize(null = "independence") %>%
  generate(reps = 1000, type = "permute") %>%
  calculate(stat = "diff in props", order = c("treatment", "control"))
  
# Using the permuation data, plot stat
ggplot(opp_perm, aes(x = stat)) + 
  # Add a histogram layer with binwidth 0.005
  geom_histogram(binwidth = 0.005) +
  # Add a vline layer with intercept diff_obs
  geom_vline(aes(xintercept = diff_obs), color = "red")
```
## Summarizing opportunity cost (2)
```
# Visualize the statistic 
opp_perm %>%
  visualize(obs_stat = diff_orig, direction = "less")

# Calculate the p-value using `get_p_value`
opp_perm %>%
  get_p_value(obs_stat = diff_orig, direction = "less")

# Calculate the p-value using `summarize`
opp_perm %>%
  summarize(p_value = mean(stat <= diff_orig))
```
## p-value for two-sided hypotheses: opportunity costs
```
# Calculate the two-sided p-value
opp_perm %>%
  summarize(p_value = 2 * mean(stat <= diff_orig))
```


# 4. Confidence intervals 

## Resampling from a sample
```
# From previous steps
ex1_props <- all_polls %>% 
  group_by(poll) %>% 
  summarize(stat = mean(vote == "yes"))
ex2_props <- all_polls %>%
  filter(poll == 1) %>%
  select(vote) %>%
  specify(response = vote, success = "yes") %>%
  generate(reps = 1000, type = "bootstrap") %>% 
  calculate(stat = "prop")
  
# Calculate variability of p-hat
ex1_props %>% 
  summarize(variability = sd(stat))
  
# Calculate variability of p-hat*
ex2_props %>% 
  summarize(variability = sd(stat))
```
## Visualizing the variability of p-hat
```
# Combine data from both experiments
both_ex_props <- bind_rows(ex1_props, ex2_props, .id = "experiment")

# Using both_ex_props, plot stat colored by experiment
ggplot(both_ex_props, aes(x = stat, color = experiment)) + 
  # Add a density layer with bandwidth 0.1
  geom_density(bw = 0.1)
```
## Empirical Rule
```
# Proportion of yes votes by poll
props <- all_polls %>% 
  group_by(poll) %>% 
  summarize(prop_yes = mean(vote == "yes"))

# The true population proportion of yes votes
true_prop_yes <- 0.6

# Proportion of polls within 2SE
props %>%
  # Add column: is prop_yes in 2SE of 0.6
  mutate(is_in_conf_int = abs(prop_yes - true_prop_yes) < 2 * sd(prop_yes)) %>%
  # Calculate  proportion in conf int
  summarize(prop_in_conf_int = mean(is_in_conf_int))
```
## Bootstrap t-confidence interval
```
# From previous exercises
one_poll <- all_polls %>%
  filter(poll == 1) %>%
  select(vote)
one_poll_boot <- one_poll %>%
  specify(response = vote, success = "yes") %>%
  generate(reps = 1000, type = "bootstrap") %>% 
  calculate(stat = "prop")
  
p_hat <- one_poll %>%
  # Calculate proportion of yes votes
  summarize(stat = mean(vote == "yes")) %>%
  pull()

# Create an interval of plausible values
one_poll_boot %>%
  summarize(
    # Lower bound is p_hat minus 2 std errs
    lower = p_hat - 2 * sd(stat),
    # Upper bound is p_hat plus 2 std errs
    upper = p_hat + 2 * sd(stat)
  )
```
## Bootstrap percentile interval
```
# Manually calculate a 95% percentile interval
one_poll_boot %>%
  summarize(
    lower = quantile(stat, p = 0.025),
    upper = quantile(stat, p = 0.975)
  )
  
# Calculate the same interval, more conveniently
percentile_ci <- one_poll_boot %>% 
  get_confidence_interval(level = 0.95)
  
one_poll_boot %>% 
  # Visualize in-between the endpoints given by percentile_ci
  visualize(endpoints = percentile_ci, direction = "between")
```
## Sample size effects on bootstrap CIs
```
calc_t_conf_int <- function(resampled_dataset) {
  resampled_dataset %>%
    summarize(
      lower = p_hat - 2 * sd(stat),
      upper = p_hat + 2 * sd(stat)
    )
}

# Find the bootstrap t-confidence interval for 30 resamples
calc_t_conf_int(one_poll_boot)

# ... and for 300 resamples
calc_t_conf_int(one_poll_boot_300)

# ... and for 3 resamples
calc_t_conf_int(one_poll_boot_3)
```
## Sample proportion value effects on bootstrap CIs
```
calc_p_hat <- function(dataset) {
  dataset %>%
    summarize(stat = mean(vote == "yes")) %>%
    pull()
}
calc_t_conf_int <- function(resampled_dataset, p_hat) {
  resampled_dataset %>%
    summarize(
      lower = p_hat - 2 * sd(stat),
      upper = p_hat + 2 * sd(stat)
    )
}

# Find proportion of yes votes from original population
p_hat <- calc_p_hat(one_poll)

# Review the value
p_hat  

# Calculate bootstrap t-confidence interval (original 0.6 param)
calc_t_conf_int(one_poll_boot, p_hat)

# Find proportion of yes votes from new population
p_hat_0.8 <- calc_p_hat(one_poll_0.8)
  
# Review the value
p_hat_0.8  
  
# Calculate the bootstrap t-confidence interval (new 0.8 param)
calc_t_conf_int(one_poll_boot_0.8, p_hat_0.8)
```
## Percentile effects on bootstrap CIs
```
# Calculate a 95% bootstrap percentile interval
one_poll_boot %>% 
  get_confidence_interval(level = 0.95) 

# Calculate a 99% bootstrap percentile interval
one_poll_boot %>% 
  get_confidence_interval(level = 0.99) 

# Calculate a 90% bootstrap percentile interval
one_poll_boot %>% 
  get_confidence_interval(level = 0.9) 

# Plot ci_endpoints vs. ci_percent to compare the intervals
ggplot(conf_int_data, aes(x = ci_percent, y = ci_endpoints)) +
  # Add a line layer
  geom_line()
```
