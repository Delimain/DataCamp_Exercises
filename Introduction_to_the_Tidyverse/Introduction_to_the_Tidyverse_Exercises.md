**Note**: At the time of writing, all the exercises herein are offered freely on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource.The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Introduction to the Tidyverse](https://www.datacamp.com/courses/introduction-to-the-tidyverse)

# 1. Data wrangling

## Loading the gapminder and dplyr packages
```
# Load the gapminder package
library(gapminder)

# Load the dplyr package
library(dplyr)

# Look at the gapminder dataset
gapminder
```
## Filtering for one year
```
# Filter the gapminder dataset for the year 1957
gapminder %>%
  filter(year == 1957)
```
## Filtering for one country and one year
```
# Filter for China in 2002
gapminder %>%
  filter(country == "China" & year == 2002)
```
## Arranging observations by life expectancy
```
# Sort in ascending order of lifeExp
gapminder %>%
  arrange(lifeExp)

# Sort in descending order of lifeExp
gapminder %>%
  arrange(desc(lifeExp))
```
## Filtering and arranging
```
# Filter for the year 1957, then arrange in descending order of population
gapminder %>%
  filter(year == 1957) %>%
  arrange(desc(pop))
```
## Using mutate to change or create a column
```
# Use mutate to change lifeExp to be in months
gapminder %>%
  mutate(lifeExp = lifeExp * 12)

# Use mutate to create a new column called lifeExpMonths
gapminder%>%
  mutate(lifeExpMonths = lifeExp * 12)
```
## Combining filter, mutate, and arrange
```
# Filter, mutate, and arrange the gapminder dataset
gapminder%>%
  filter(year == 2007) %>%
  mutate(lifeExpMonths = 12 * lifeExp) %>%
  arrange(desc(lifeExpMonths))
```


# 2. Data visualization 

## Variable assignment
```
# Load the ggplot2 package as well
library(ggplot2)

# Create gapminder_1952
gapminder_1952 <- gapminder %>% 
  filter(year == 1952)
```
## Comparing population and GDP per capita
```
# Change to put pop on the x-axis and gdpPercap on the y-axis
ggplot(gapminder_1952, aes(x = pop, y = gdpPercap)) +
  geom_point()
```
## Comparing population and life expectancy
```
# Create a scatter plot with pop on the x-axis and lifeExp on the y-axis
ggplot(gapminder_1952, aes(x = pop, y = lifeExp)) + 
  geom_point()
```
## Putting the x-axis on a log scale
```
# Change this plot to put the x-axis on a log scale
ggplot(gapminder_1952, aes(x = pop, y = lifeExp)) +
  geom_point() + 
  scale_x_log10()
```
## Putting the x- and y- axes on a log scale
```
# Scatter plot comparing pop and gdpPercap, with both axes on a log scale
ggplot(gapminder_1952, aes(x = pop, y = gdpPercap)) + 
  geom_point() + 
  scale_x_log10() + 
  scale_y_log10()
```
## Adding color to a scatter plot
```
# Scatter plot comparing pop and lifeExp, with color representing continent
ggplot(gapminder_1952, aes(x = pop, y = lifeExp, color = continent)) + 
  geom_point() + 
  scale_x_log10()
```
## Adding size and color to a plot
```
# Add the size aesthetic to represent a country's gdpPercap
ggplot(gapminder_1952, aes(x = pop, y = lifeExp, color = continent, size = gdpPercap)) +
  geom_point() +
  scale_x_log10()
```
## Creating a subgraph for each continent
```
# Scatter plot comparing pop and lifeExp, faceted by continent
ggplot(gapminder_1952, aes(x = pop, y = lifeExp)) + 
  geom_point() + 
  scale_x_log10() + 
  facet_wrap(~continent)
```
## Faceting by year
```
# Scatter plot comparing gdpPercap and lifeExp, with color representing continent
# and size representing population, faceted by year
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp, color = continent, size = pop)) + 
  geom_point() + 
  scale_x_log10() + 
  facet_wrap(~year)
```


# 3. Grouping and summarizing 

## Summarizing the median life expectancy
```
# Summarize to find the median life expectancy
gapminder %>%
  summarize(medianLifeExp = median(lifeExp))
```
## Summarizing the median life expectancy in 1957
```
# Filter for 1957 then summarize the median life expectancy
gapminder %>%
  filter(year == 1957) %>%
  summarize(medianLifeExp = median(lifeExp))
```
## Summarizing multiple variables in 1957
```
# Filter for 1957 then summarize the median life expectancy and the maximum GDP per capita
gapminder %>%
  filter(year == 1957) %>%
  summarize(medianLifeExp = median(lifeExp), maxGdpPercap = max(gdpPercap))
```
## Summarizing by year
```
# Find median life expectancy and maximum GDP per capita in each year
gapminder %>%
  group_by(year) %>%
  summarize(medianLifeExp = median(lifeExp), maxGdpPercap = max(gdpPercap))
```
## Summarizing by continent
```
# Find median life expectancy and maximum GDP per capita in each continent in 1957
gapminder %>%
  filter(year == 1957) %>%
  group_by(continent) %>%
  summarize(medianLifeExp = median(lifeExp), maxGdpPercap = max(gdpPercap))
```
## Summarizing by continent and year
```
# Find median life expectancy and maximum GDP per capita in each year/continent combination
gapminder %>%
  group_by(continent, year) %>%
  summarize(medianLifeExp = median(lifeExp), maxGdpPercap = max(gdpPercap))
```
## Visualizing median life expectancy over time
```
by_year <- gapminder %>%
  group_by(year) %>%
  summarize(medianLifeExp = median(lifeExp),
            maxGdpPercap = max(gdpPercap))

# Create a scatter plot showing the change in medianLifeExp over time
ggplot(by_year, aes(x = year, y = medianLifeExp)) + 
  geom_point() + 
  expand_limits(y = 0)
```
## Visualizing median GDP per capita per continent over time
```
# Summarize medianGdpPercap within each continent within each year: by_year_continent
by_year_continent <- gapminder %>%
  group_by(continent, year) %>%
  summarize(medianGdpPercap = median(gdpPercap))

# Plot the change in medianGdpPercap in each continent over time
ggplot(by_year_continent, aes(x = year, y = medianGdpPercap, color = continent)) + 
  geom_point() + 
  expand_limits(y = 0)
```
## Comparing median life expectancy and median GDP per continent in 2007
```
# Summarize the median GDP and median life expectancy per continent in 2007
by_continent_2007 <- gapminder %>%
  filter(year == 2007) %>%
  group_by(continent) %>%
  summarize(medianLifeExp = median(lifeExp), medianGdpPercap = median(gdpPercap))

# Use a scatter plot to compare the median GDP and median life expectancy
ggplot(by_continent_2007, aes(x = medianGdpPercap, y = medianLifeExp, color = continent)) + 
  geom_point()
```


# 4. Types of visualizations 

## Visualizing median GDP per capita over time
```
# Summarize the median gdpPercap by year, then save it as by_year
by_year <- gapminder %>%
  group_by(year) %>%
  summarize(medianGdpPercap = median(gdpPercap))

# Create a line plot showing the change in medianGdpPercap over time
ggplot(by_year, aes(x = year, y = medianGdpPercap)) + 
  geom_line() + 
  expand_limits(y = 0)
```
## Visualizing median GDP per capita by continent over time
```
# Summarize the median gdpPercap by year & continent, save as by_year_continent
by_year_continent <- gapminder %>%
  group_by(year, continent) %>%
  summarize(medianGdpPercap = median(gdpPercap))

# Create a line plot showing the change in medianGdpPercap by continent over time
ggplot(by_year_continent, aes(x = year, y = medianGdpPercap, color = continent)) + 
  geom_line() + 
  expand_limits(y = 0)
```
## Visualizing median GDP per capita by continent
```
# Summarize the median gdpPercap by year and continent in 1952
by_continent <- gapminder %>%
  filter(year == 1952) %>%
  group_by(continent) %>%
  summarize(medianGdpPercap = median(gdpPercap))

# Create a bar plot showing medianGdp by continent
ggplot(by_continent,aes(x = continent, y = medianGdpPercap)) + 
  geom_col()
```
## Visualizing GDP per capita by country in Oceania
```
# Filter for observations in the Oceania continent in 1952
oceania_1952 <- gapminder %>%
  filter(year == 1952, continent == "Oceania")

# Create a bar plot of gdpPercap by country
ggplot(oceania_1952, aes(x = country, y = gdpPercap)) + 
  geom_col()
```
## Visualizing population
```
# Create a histogram of population (pop)
ggplot(gapminder_1952, aes(x = pop)) + 
  geom_histogram()
```
## Visualizing population with x-axis on a log scale
```
# Create a histogram of population (pop), with x on a log scale
ggplot(gapminder_1952, aes(x = pop)) + 
  geom_histogram() + 
  scale_x_log10()
```
## Comparing GDP per capita across continents
```
# Create a boxplot comparing gdpPercap among continents
ggplot(gapminder_1952, aes(x = continent, y = gdpPercap)) + 
  geom_boxplot() + 
  scale_y_log10()
```
## Adding a title to your graph
```
# Add a title to this graph: "Comparing GDP per capita across continents"
ggplot(gapminder_1952, aes(x = continent, y = gdpPercap)) +
  geom_boxplot() +
  scale_y_log10() + 
  ggtitle("Comparing GDP per capita across continents")
```
