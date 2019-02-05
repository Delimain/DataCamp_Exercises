**Note**: At the time of writing, all the exercises herein are offered on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource. The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Data Visualization with ggplot2 (Part 2)](https://www.datacamp.com/courses/data-visualization-with-ggplot2-2)

# 1. Statistics

## Smoothing
```
library(ggplot2)

# Explore the mtcars data frame with str()
str(mtcars)

# A scatter plot with LOESS smooth
ggplot(mtcars, aes(x = wt, y = mpg)) +
  geom_point() +
  geom_smooth()

# A scatter plot with an ordinary Least Squares linear model
ggplot(mtcars, aes(x = wt, y = mpg)) +
  geom_point() +
  geom_smooth(method = "lm")

# The previous plot, without CI ribbon
ggplot(mtcars, aes(x = wt, y = mpg)) +
  geom_point() +
  geom_smooth(method = "lm", se = FALSE)

# The previous plot, without points
ggplot(mtcars, aes(x = wt, y = mpg)) +
  geom_smooth(method = "lm", se = FALSE)
```
## Grouping variables
```
# 1 - Define cyl as a factor variable
ggplot(mtcars, aes(x = wt, y = mpg, col = factor(cyl))) +
  geom_point() +
  stat_smooth(method = "lm", se = FALSE)

# 2 - Plot 1, plus another stat_smooth() containing a nested aes()
ggplot(mtcars, aes(x = wt, y = mpg, col = factor(cyl))) +
  geom_point() +
  stat_smooth(method = "lm", se = FALSE) +
  stat_smooth(aes(group = 1),method = "lm", se = FALSE)
```
## Modifying stat_smooth
```
# Plot 1: change the LOESS span
ggplot(mtcars, aes(x = wt, y = mpg)) +
  geom_point() +
  geom_smooth(se = FALSE, span = 0.7)

# Plot 2: Set the second stat_smooth() to use LOESS with a span of 0.7
ggplot(mtcars, aes(x = wt, y = mpg, col = factor(cyl))) +
  geom_point() +
  stat_smooth(method = "lm", se = FALSE) +
  stat_smooth(method = "loess", aes(group = 1),
              se = FALSE, col = "black", span = 0.7)

# Plot 3: Set col to "All", inside the aes layer of stat_smooth()
ggplot(mtcars, aes(x = wt, y = mpg, col = factor(cyl))) +
  geom_point() +
  stat_smooth(method = "lm", se = FALSE) +
  stat_smooth(method = "loess",
              aes(group = 1, col = "All"),
              se = FALSE, span = 0.7)

# Plot 4: Add scale_color_manual to change the colors
myColors <- c(brewer.pal(3, "Dark2"), "black")
ggplot(mtcars, aes(x = wt, y = mpg, col = factor(cyl))) +
  geom_point() +
  stat_smooth(method = "lm", se = FALSE, span = 0.7) +
  stat_smooth(method = "loess", 
              aes(group = 1, col="All"), 
              se = FALSE, span = 0.7) +
  scale_color_manual("Cylinders", values = myColors)
```
## Modifying stat_smooth (2)
```
# Plot 1: Jittered scatter plot, add a linear model (lm) smooth
ggplot(Vocab, aes(x = education, y = vocabulary)) +
  geom_jitter(alpha = 0.2) +
  stat_smooth(method = "lm", se = FALSE)

# Plot 2: points, colored by year
ggplot(Vocab, aes(x = education, y = vocabulary, col = year)) +
  geom_jitter(alpha = 0.2) 

# Plot 3: lm, colored by year
ggplot(Vocab, aes(x = education, y = vocabulary, col = factor(year))) +
  stat_smooth(method = "lm", se = FALSE)
  
# Plot 4: Set a color brewer palette
ggplot(Vocab, aes(x = education, y = vocabulary, col = factor(year))) +
  stat_smooth(method = "lm", se = FALSE) +
  scale_color_brewer()

# Plot 5: Add the group aes, specify alpha and size
ggplot(Vocab, aes(x = education, y = vocabulary, col = year, group = factor(year))) +
  stat_smooth(method = "lm", se = FALSE, alpha = 0.6, size = 2) +
  scale_color_gradientn(colors = brewer.pal(9, "YlOrRd"))
```
## Quantiles
```
# Use stat_quantile instead of stat_smooth
ggplot(Vocab, aes(x = education, y = vocabulary, col = year, group = factor(year))) +
  stat_quantile(alpha = 0.6, size = 2) +
  scale_color_gradientn(colors = brewer.pal(9,"YlOrRd"))

# Set quantile to 0.5
ggplot(Vocab, aes(x = education, y = vocabulary, col = year, group = factor(year))) +
  stat_quantile(quantiles = 0.5, alpha = 0.6, size = 2) +
  scale_color_gradientn(colors = brewer.pal(9,"YlOrRd"))
```
## Sum
```
# Plot 1: Jittering only
p <- ggplot(Vocab, aes(x = education, y = vocabulary)) +
  geom_jitter(alpha = 0.2)

# Plot 2: Add stat_sum
p +
  stat_sum()

# Plot 3: Set size range
p +
  stat_sum() +
  scale_size(range = c(1, 10))

```
## Preparations
```
# Display structure of mtcars
str(mtcars)

# Convert cyl and am to factors
mtcars$cyl <- as.factor(mtcars$cyl)
mtcars$am <- as.factor(mtcars$am)

# Define positions
posn.d <- position_dodge(0.1)
posn.jd <- position_jitterdodge(jitter.width = 0.1, dodge.width = 0.2)
posn.j <- position_jitter(0.2)

# Base layers
wt.cyl.am <- ggplot(mtcars, aes(x = cyl, y = wt, col = am, fill = am, group = am))
```
## Plotting variations
```
# Plot 1: Jittered, dodged scatter plot with transparent points
wt.cyl.am +
  geom_point(position = posn.jd, alpha = 0.6)

# Plot 2: Mean and SD - the easy way
wt.cyl.am +
  geom_point(position = posn.d, alpha = 0.6) +
  stat_summary(fun.data = mean_sdl, 
               fun.args = list(mult = 1),
               position = posn.d)

# Plot 3: Mean and 95% CI - the easy way
wt.cyl.am +
  geom_point(position = posn.d, alpha = 0.6) +
  stat_summary(fun.data = mean_cl_normal, position = posn.d)

# Plot 4: Mean and SD - with T-tipped error bars - fill in ___
wt.cyl.am +
  stat_summary(geom = "point", fun.y = mean,
               position = posn.d) +
  stat_summary(geom = "errorbar", fun.data = mean_sdl,
               position = posn.d, fun.args = list(mult = 1), width = 0.1)
```
## Custom Functions
```
# Play vector xx is available

# Function to save range for use in ggplot
gg_range <- function(x) {
  data.frame(ymin = min(x),
             ymax = max(x))
}

gg_range(xx)
# Required output
#   ymin ymax
# 1    1  100

# Function to Custom function
med_IQR <- function(x) {
  data.frame(y = median(x),
             ymin = quantile(x)[2],
             ymax = quantile(x)[4])
}

med_IQR(xx)
# Required output
#        y  ymin  ymax
# 25% 50.5 25.75 75.25
```
## Custom Functions (2)
```
# The base ggplot command; you don't have to change this
wt.cyl.am <- ggplot(mtcars, aes(x = cyl,y = wt, col = am, fill = am, group = am))

# Add three stat_summary calls to wt.cyl.am
wt.cyl.am +
  stat_summary(geom = "linerange", fun.data = med_IQR,
               position = posn.d, size = 3) +
  stat_summary(geom = "linerange", fun.data = gg_range,
               position = posn.d, size = 3,
               alpha = 0.4) +
  stat_summary(geom = "point", fun.y = median,
               position = posn.d, size = 3,
               col = "black", shape = "X")
```


# 2. Coordinates and Facets 

## Zooming In
```
# Basic ggplot() command, coded for you
p <- ggplot(mtcars, aes(x = wt, y = hp, col = am)) + 
       geom_point() + 
       geom_smooth()

# Add scale_x_continuous()
p +
  scale_x_continuous(limits = c(3, 6), expand = c(0, 0
))

# Add coord_cartesian(): the proper way to zoom in
p +
  coord_cartesian(xlim = c(3, 6))
```
## Aspect Ratio
```
# Complete basic scatter plot function
base.plot <- ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, col = Species)) +
               geom_jitter() +
               geom_smooth(method = "lm", se = FALSE)

# Plot base.plot: default aspect ratio
base.plot

# Fix aspect ratio (1:1) of base.plot
base.plot +
  coord_equal()
```
## Pie Charts
```
# Create a stacked bar plot: wide.bar
wide.bar <- ggplot(mtcars, aes(x = 1, fill = cyl)) +
              geom_bar()

# Convert wide.bar to pie chart
wide.bar +
  coord_polar(theta = "y")

# Create stacked bar plot: thin.bar
thin.bar <- ggplot(mtcars, aes(x = 1, fill = cyl)) +
              geom_bar(width = 0.1) +
              scale_x_continuous(limits = c(0.5, 1.5))

# Convert thin.bar to "ring" type pie chart
thin.bar + 
  coord_polar(theta = "y")
```
## Facets: the basics
```
# Basic scatter plot
p <- ggplot(mtcars, aes(x = wt, y = mpg)) +
  geom_point()

# 1 - Separate rows according to transmission type, am
p +
  facet_grid(am ~ .)

# 2 - Separate columns according to cylinders, cyl
p +
  facet_grid(. ~ cyl)

# 3 - Separate by both columns and rows 
p +
  facet_grid(am ~ cyl)
```
## Many variables
```
# Code to create the cyl_am col and myCol vector
mtcars$cyl_am <- paste(mtcars$cyl, mtcars$am, sep = "_")
myCol <- rbind(brewer.pal(9, "Blues")[c(3,6,8)],
               brewer.pal(9, "Reds")[c(3,6,8)])

# Map cyl_am onto col
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl_am)) +
  geom_point() +
  scale_color_manual(values = myCol)
  
# Grid facet on gear vs. vs
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl_am)) +
  geom_point() +
  scale_color_manual(values = myCol) +
  facet_grid(gear ~ vs)

# Also map disp to size
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl_am, size = disp)) +
  geom_point() +
  scale_color_manual(values = myCol) +
  facet_grid(gear ~ vs)
```
## Dropping levels
```
# Basic scatter plot
p <- ggplot(mamsleep, aes(x = time, y = name, col = sleep)) +
  geom_point()
  
# Execute to display plot
p

# Facet rows accoding to vore
p +
  facet_grid(vore ~ .)

# Specify scale and space arguments to free up rows
p +
  facet_grid(vore ~ ., scale = "free_y", space = "free_y")
```


# 3. Themes

## Rectangles
```
# Starting point
z

# Plot 1: Change the plot background fill to myPink
z +
  theme(plot.background = element_rect(fill = myPink))

# Plot 2: Adjust the border to be a black line of size 3
z +
  theme(plot.background = element_rect(fill = myPink, color = "black", size = 3))

# Theme to remove all rectangles
no_panels <- theme(rect = element_blank())

# Plot 3: Combine custom themes
z +
  no_panels +
  theme(plot.background = element_rect(fill = myPink, color = "black", size = 3))
```
## Lines
```
# Extend z using theme() function and 3 args
z +
  theme(panel.grid = element_blank(), axis.line = element_line(color = "red"), axis.ticks = element_line(color = "red"))
```
## Text
```
# Original plot, color provided
z
myRed

# Extend z with theme() function and 3 args
z +
  theme(strip.text = element_text(size = 16, color = myRed),
        axis.title = element_text(color = myRed, hjust = 0, face = "italic"),
        axis.text = element_text(color = "black"))
```
## Legends
```
# Move legend by position
z +
  theme(legend.position = c(0.85, 0.85))

# Change direction
z +
  theme(legend.direction = "horizontal")
  
# Change location by name
z +
  theme(legend.position = "bottom")

# Remove legend entirely
z +
  theme(legend.position = "none")
```
## Positions
```
# Increase spacing between facets
library(grid)
z +
  theme(panel.spacing.x = unit(2, "cm"))

# Adjust the plot margin
z +
  theme(panel.spacing.x = unit(2, "cm"), plot.margin = unit(c(1, 2, 1, 1), "cm"))
```
## Updating Themes
```
# Original plot
z2

# Theme layer saved as an object, theme_pink
theme_pink <- theme(panel.background = element_blank(),
                    legend.key = element_blank(),
                    legend.background = element_blank(),
                    strip.background = element_blank(),
                    plot.background = element_rect(fill = myPink, color = "black", size = 3),
                    panel.grid = element_blank(),
                    axis.line = element_line(color = "red"),
                    axis.ticks = element_line(color = "red"),
                    strip.text = element_text(size = 16, color = myRed),
                    axis.title.y = element_text(color = myRed, hjust = 0, face = "italic"),
                    axis.title.x = element_text(color = myRed, hjust = 0, face = "italic"),
                    axis.text = element_text(color = "black"),
                    legend.position = "none")
  
# 1 - Apply theme_pink to z2
z2 +
  theme_pink

# 2 - Update the default theme, and at the same time
# assign the old theme to the object old.
old <- theme_update(panel.background = element_blank(),
             legend.key = element_blank(),
             legend.background = element_blank(),
             strip.background = element_blank(),
             plot.background = element_rect(fill = myPink, color = "black", size = 3),
             panel.grid = element_blank(),
             axis.line = element_line(color = "red"),
             axis.ticks = element_line(color = "red"),
             strip.text = element_text(size = 16, color = myRed),
             axis.title.y = element_text(color = myRed, hjust = 0, face = "italic"),
             axis.title.x = element_text(color = myRed, hjust = 0, face = "italic"),
             axis.text = element_text(color = "black"),
             legend.position = "none")

# 3 - Display the plot z2 - new default theme used
z2

# 4 - Restore the old default theme
theme_set(old)

# Display the plot z2 - old theme restored
z2
```
## Exploring 
```
# Original plot
z2

# Load ggthemes
library(ggthemes)

# Apply theme_tufte(), plot additional modifications
custom_theme <- theme_tufte() +
  theme(legend.position = c(0.9, 0.9),
        legend.title = element_text(face = "italic", size = 12),
        axis.title = element_text(face = "bold", size = 14))

# Draw the customized plot
z2 + 
  custom_theme
 
# Use theme set to set custom theme as default
theme_set(custom_theme)

# Plot z2 again
z2
```


# 4. Best Practices 

## Bar Plots (1)
```
# Base layers
m <- ggplot(mtcars, aes(x = cyl, y = wt))

# Draw dynamite plot
m +
  stat_summary(fun.y = mean, geom = "bar", fill = "skyblue") +
  stat_summary(fun.data = mean_sdl, fun.args = list(mult = 1), geom = "errorbar", width = 0.1)
```
## Bar Plots (2)
```
# Base layers
m <- ggplot(mtcars, aes(x = cyl,y = wt, col = am, fill = am))

# Plot 1: Draw dynamite plot
m +
  stat_summary(fun.y = mean, geom = "bar") +
  stat_summary(fun.data = mean_sdl, fun.args = list(mult = 1), geom = "errorbar", width = 0.1)

# Plot 2: Set position dodge in each stat function
m +
  stat_summary(fun.y = mean, geom = "bar", position = "dodge") +
  stat_summary(fun.data = mean_sdl, fun.args = list(mult = 1), 
               geom = "errorbar", width = 0.1, position = "dodge")

# Set your dodge posn manually
posn.d <- position_dodge(0.9)

# Plot 3: Redraw dynamite plot
m +
  stat_summary(fun.y = mean, geom = "bar", position = posn.d) +
  stat_summary(fun.data = mean_sdl, fun.args = list(mult = 1), geom = "errorbar", width = 0.1, position = posn.d)
```
## Bar Plots (3)
```
# Base layers
m <- ggplot(mtcars.cyl, aes(x = cyl, y = wt.avg))

# Plot 1: Draw bar plot with geom_bar
m + 
  geom_bar(stat = "identity", fill = "skyblue")

# Plot 2: Draw bar plot with geom_col
m + 
  geom_col(fill = "skyblue")

# Plot 3: geom_col with variable widths.
m + 
  geom_col(fill = "skyblue", width = mtcars.cyl$prop)
 
# Plot 4: Add error bars
m + 
  geom_col(fill = "skyblue", width = mtcars.cyl$prop) +
  geom_errorbar(aes(ymin = wt.avg, ymax = wt.avg), width = 0.1)
```
## Pie Charts (1)
```
# Bar chart
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar(position = "fill")

# Convert bar chart to pie chart
ggplot(mtcars, aes(x = factor(1), fill = am)) +
  geom_bar(position = "fill", width = 1) +
  facet_grid(. ~ cyl) +
  coord_polar(theta = "y") +
  theme_void()
```
## Pie Charts (2)
```
# Parallel coordinates plot using GGally
library(GGally)

# All columns except am
group_by_am <- 9
my_names_am <- (1:11)[-group_by_am]

# Basic parallel plot - each variable plotted as a z-score transformation
ggparcoord(mtcars, my_names_am, groupColumn = group_by_am, alpha = 0.8)
```
## Heat Maps
```
# Create color palette
myColors <- brewer.pal(9, "Reds")

# Build the heat map from scratch
ggplot(barley, aes(x = year, y = variety, fill = yield)) +
  geom_tile() +
  facet_wrap(~ site, ncol = 1) +
  scale_fill_gradientn(colors = myColors)
```
## Heat Maps Alternatives (1)
```
# The heat map we want to replace
# Don't remove, it's here to help you!
myColors <- brewer.pal(9, "Reds")
ggplot(barley, aes(x = year, y = variety, fill = yield)) +
  geom_tile() +
  facet_wrap( ~ site, ncol = 1) +
  scale_fill_gradientn(colors = myColors)

# Line plot; set the aes, geom and facet
ggplot(barley, aes(x = year, y = yield, color = variety, group = variety)) +
  geom_line() +
  facet_wrap(~ site, nrow = 1)
```
## Heat Maps Alternatives (2)
```
# Create overlapping ribbon plot from scratch
ggplot(barley, aes(x = year, 
    y = yield, 
    color = site, 
    group = site, 
    fill = site)) +
  stat_summary(fun.y = mean, geom = "line") +
  stat_summary(fun.data = mean_sdl, 
    fun.args = list(mult = 1), 
    geom = "ribbon", 
    col = NA, 
    alpha = 0.1)
```


# 5. Case Study 

## Exploring Data
```
# Explore the dataset with summary and str
summary(adult)
str(adult)

# Age histogram
ggplot(adult, aes(x = SRAGE_P)) +
  geom_histogram()

# BMI value histogram
ggplot(adult, aes(x = BMI_P)) +
  geom_histogram()

# Age colored by BMI, binwidth = 1
ggplot(adult, aes(x = SRAGE_P, fill = factor(RBMI))) +
  geom_histogram(binwidth = 1)
```
## Data Cleaning
```
# Keep adults younger than or equal to 84
adult <- adult[adult$SRAGE_P <= 84, ] 

# Keep adults with BMI at least 16 and less than 52
adult <- adult[adult$BMI_P >= 16 & adult$BMI_P < 52, ]

# Relabel the race variable
adult$RACEHPR2 <- factor(adult$RACEHPR2, labels = c("Latino", "Asian", "African American", "White"))

# Relabel the BMI categories variable
adult$RBMI <- factor(adult$RBMI, labels = c("Under-weight", "Normal-weight", "Over-weight", "Obese"))
```
## Multiple Histograms
```
# The dataset adult is available

# The color scale used in the plot
BMI_fill <- scale_fill_brewer("BMI Category", palette = "Reds")

# Theme to fix category display in faceted plot
fix_strips <- theme(strip.text.y = element_text(angle = 0, hjust = 0, vjust = 0.1, size = 14),
                    strip.background = element_blank(),
                    legend.position = "none")

# Histogram, add BMI_fill and customizations
ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) + 
  geom_histogram(binwidth = 1) +
  facet_grid(RBMI ~ .) +
  fix_strips +
  BMI_fill +
  theme_classic()
```
## Alternatives
```
# Plot 1 - Count histogram
ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) +
  geom_histogram(binwidth = 1) +
  BMI_fill

# Plot 2 - Density histogram
ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) + 
  geom_histogram(aes(y = ..density..), binwidth = 1) +
  BMI_fill

# Plot 3 - Faceted count histogram
ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) +
  geom_histogram(binwidth = 1) +
  facet_grid(RBMI ~ .) +
  BMI_fill

# Plot 4 - Faceted density histogram
ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) + 
  geom_histogram(aes(y = ..density..), binwidth = 1) +
  facet_grid(RBMI ~ .) +
  BMI_fill

# Plot 5 - Density histogram with position = "fill"
ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) + 
  geom_histogram(aes(y = ..density..), binwidth = 1, position = "fill") +
  BMI_fill

# Plot 6 - The accurate histogram
ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) + 
  geom_histogram(aes(y = ..count../sum(..count..)), binwidth = 1, position = "fill") +
  BMI_fill
```
## Do Things Manually
```
# An attempt to facet the accurate frequency histogram from before (failed)
ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) +
  geom_histogram(aes(y = ..count../sum(..count..)), binwidth = 1, position = "fill") +
  BMI_fill +
  facet_grid(RBMI ~ .)

# Create DF with table()
DF <- table(adult$RBMI, adult$SRAGE_P)

# Use apply on DF to get frequency of each group
DF_freq <- apply(DF, 2, function(x) x/sum(x))

# Load reshape2 and use melt on DF to create DF_melted
library(reshape2)
DF_melted = melt(DF_freq)

# Change names of DF_melted
names(DF_melted) <- c("FILL", "X", "value")

# Add code to make this a faceted plot
ggplot(DF_melted, aes(x = X, y = value, fill = FILL)) +
  geom_col(position = "stack") +
  BMI_fill + 
  facet_grid(FILL ~ .)
```
## Marimekko/Mosaic Plot
```
# The initial contingency table
DF <- as.data.frame.matrix(table(adult$SRAGE_P, adult$RBMI))

# Create groupSum, xmax and xmin columns
DF$groupSum <- rowSums(DF)
DF$xmax <- cumsum(DF$groupSum)
DF$xmin <- DF$xmax - DF$groupSum
# The groupSum column needs to be removed; don't remove this line
DF$groupSum <- NULL

# Copy row names to variable X
DF$X <- row.names(DF)

# Melt the dataset
library(reshape2)
DF_melted <- melt(DF, id.vars = c("X", "xmin", "xmax"), variable.name = "FILL")

# dplyr call to calculate ymin and ymax - don't change
library(dplyr)
DF_melted <- DF_melted %>%
  group_by(X) %>%
  mutate(ymax = cumsum(value/sum(value)),
         ymin = ymax - value/sum(value))

# Plot rectangles - don't change
library(ggthemes)
ggplot(DF_melted, aes(ymin = ymin,
                 ymax = ymax,
                 xmin = xmin,
                 xmax = xmax,
                 fill = FILL)) +
  geom_rect(colour = "white") +
  scale_x_continuous(expand = c(0,0)) +
  scale_y_continuous(expand = c(0,0)) +
  BMI_fill +
  theme_tufte()
```
## Adding statistics
```
# Perform chi.sq test (RBMI and SRAGE_P)
results <- chisq.test(table(adult$RBMI, adult$SRAGE_P))

# Melt results$residuals and store as resid
resid <- melt(results$residuals)

# Change names of resid
names(resid) <- c("FILL", "X", "residual")

# merge the two datasets:
DF_all <- merge(DF_melted, resid)

# Update plot command
library(ggthemes)
ggplot(DF_all, aes(ymin = ymin,
                   ymax = ymax,
                   xmin = xmin,
                   xmax = xmax,
                   fill = residual)) +
  geom_rect() +
  scale_fill_gradient2() +
  scale_x_continuous(expand = c(0,0)) +
  scale_y_continuous(expand = c(0,0)) +
  theme_tufte()
```
## Adding text
```
# Plot so far
p

# Position for labels on y axis (don't change)
index <- DF_all$xmax == max(DF_all$xmax)
DF_all$yposn <- DF_all$ymin[index] + (DF_all$ymax[index] - DF_all$ymin[index])/2

# Plot 1: geom_text for BMI (i.e. the fill axis)
p1 <- p %+% DF_all + 
  geom_text(aes(x = max(xmax), 
               y = yposn,
               label = FILL),
            size = 3, hjust = 1,
            show.legend  = FALSE)
p1

# Plot 2: Position for labels on x axis
DF_all$xposn <- DF_all$xmin + (DF_all$xmax - DF_all$xmin) / 2

# geom_text for ages (i.e. the x axis)
p1 %+% DF_all + 
  geom_text(aes(x = xposn, label = X),
            y = 1, angle = 90,
            size = 3, hjust = 1,
            show.legend = FALSE)
```
## Generalizations
```
# Load final package
library(reshape2)

# Script generalized into a function
mosaicGG

# BMI described by age (as previously seen)
mosaicGG(adult, X = "SRAGE_P", FILL = "RBMI")

# Poverty described by age
mosaicGG(adult, X = "SRAGE_P", FILL = "POVLL")

# mtcars: am described by cyl
mosaicGG(mtcars, "cyl", "am")

# Vocab: vocabulary described by education
library(carData)
mosaicGG(Vocab, "education", "vocabulary")
```
