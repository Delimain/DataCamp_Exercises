**Note**: At the time of writing, all the exercises herein are offered on datacamp.com and can be accessed via the link below. If you have an interest in learning data science, it is a highly valuable resource. The information below is for personal and professional reference and is no substitute for the wealth of knowledge attained from completing the course itself.
# [Joining Data in R with dplyr](https://www.datacamp.com/courses/joining-data-in-r-with-dplyr)

# 1. Mutating joins

## A basic join
```
# Complete the code to join artists to bands
bands2 <- left_join(bands, artists, by = c("first", "last"))

# Examine the results
bands2
```
## A second join
```
# Fix the code to recreate bands2
left_join(bands, artists, by = c("first", "last"))
```
## A right join
```
# Finish the code below to recreate bands3 with a right join
bands2 <- left_join(bands, artists, by = c("first", "last"))
bands3 <- right_join(artists, bands, by = c("first", "last"))

# Check that bands3 is equal to bands2
setequal(bands2, bands3)
```
## Inner joins and full joins
```
# Join albums to songs using inner_join()
inner_join(songs, albums, by = "album")

# Join bands to artists using full_join()
full_join(artists, bands, by = c("first", "last"))
```
## Pipes
```
# Find guitarists in bands dataset (don't change)
temp <- left_join(bands, artists, by = c("first", "last"))
temp <- filter(temp, instrument == "Guitar")
select(temp, first, last, band)

# Reproduce code above using pipes
bands %>% 
  left_join(artists, by = c("first", "last")) %>%
  filter(instrument == "Guitar") %>%
  select(first, last, band)
```
## Practice with pipes and joins
```
# Examine the contents of the goal dataset
goal

# Create goal2 using full_join() and inner_join() 
goal2 <- artists %>%
  full_join(bands, by = c("first", "last")) %>%
  inner_join(songs, by = c("first", "last")) 
  
# Check that goal and goal2 are the same
setequal(goal, goal2)
```
## Choose your joins
```
# Create one table that combines all information
artists %>%
  full_join(bands, by = c("first", "last")) %>%
  full_join(songs, by = c("first", "last")) %>%
  full_join(albums, by = c("album", "band"))
```


# 2. Filtering joins and set operations 

## Apply a semi-join
```
# View the output of semi_join()
artists %>% 
  semi_join(songs, by = c("first", "last"))

# Create the same result
artists %>% 
  right_join(songs, by = c("first", "last")) %>% 
  filter(instrument != "NA") %>% 
  select(first, last, instrument)
```
## Exploring with semi-joins
```
albums %>% 
  # Collect the albums made by a band
  semi_join(bands, by = "band") %>% 
  # Count the albums made by a band
  nrow()
```
## Apply an anti-join
```
# Return rows of artists that don't have bands info
artists %>% 
  anti_join(bands, by = c("first", "last"))
```
## Apply another anti-join
```
# Check whether album names in labels are mis-entered
labels %>% 
  anti_join(albums, by = "album")
```
## Which filtering join?
```
# Determine which key joins labels and songs
labels
songs

# Check your understanding
songs %>% 
  # Find the rows of songs that match a row in labels
  semi_join(labels, by = "album") %>% 
  # Number of matches between labels and songs
  nrow()
```
## How many songs are there?
```
aerosmith %>% 
  # Create the new dataset using a set operation
  union(greatest_hits) %>% 
  # Count the total number of songs
  nrow()
```
## Greatest hits
```
# Create the new dataset using a set operation
aerosmith %>% 
  intersect(greatest_hits)
```
## Live! Bootleg songs
```
# Select the song names from live
live_songs <- live %>% select(song)

# Select the song names from greatest_hits
greatest_songs <- greatest_hits %>% select(song)

# Create the new dataset using a set operation
live_songs %>% 
  setdiff(greatest_songs)
```
## Multiple operations
```
# Select songs from live and greatest_hits
live_songs <- select(live, song)
greatest_songs <- select(greatest_hits, song)


# Find songs in at least one of live_songs and greatest_songs
all_songs <- union(live_songs, greatest_songs)

# Find songs in both 
common_songs <- intersect(live_songs, greatest_songs)

# Find songs that only exist in one dataset
setdiff(all_songs, common_songs)
```
## Apply setequal
```
# Check if same order: definitive and complete
identical(definitive, complete)

# Check if any order: definitive and complete
setequal(definitive, complete)

# Songs in definitive but not complete
setdiff(definitive, complete)

# Songs in complete but not definitive
setdiff(complete, definitive)
```
## Apply setequal again
```
# Return songs in definitive that are not in complete
definitive %>% 
  anti_join(complete)

# Return songs in complete that are not in definitive
complete %>% 
  anti_join(definitive)
```
## Comparing albums
```
# Get union of complete and soundtrack
complete_and_soundtrack <- union(complete, soundtrack)

# Check if same order: definitive and union of complete and soundtrack
complete_and_soundtrack %>%
  identical(definitive)

# Check if any order: definitive and union of complete and soundtrack
complete_and_soundtrack %>%
  setequal(definitive)
```


# 3. Assembling data 

## Which bind?
```
# Examine side_one and side_two
side_one
side_two

# Bind side_one and side_two into a single dataset
side_one %>% 
  bind_rows(side_two)
```
## Bind rows
```
# Examine discography and jimi
discography
jimi

jimi %>% 
  # Bind jimi into a single data frame
  bind_rows(, .id = "album") %>% 
  # Make a complete data frame
  left_join(discography, by = "album")
```
## Bind columns
```
# Examine hank_years and hank_charts
hank_years
hank_charts

hank_years %>% 
  # Reorder hank_years alphabetically by song title
  arrange(song) %>% 
  # Select just the year column
  select(year) %>% 
  # Bind the year column
  bind_cols(hank_charts) %>% 
  # Arrange the finished dataset
  arrange(year, song)
```
## Make a data frame
```
# Make combined data frame using data_frame()
data_frame(year = hank_year, song = hank_song, peak = hank_peak) %>% 
  # Extract songs where peak equals 1
  filter(peak == 1)
```
## Lists of columns
```
# Examine the contents of hank
hank

# Convert the hank list into a data frame
as_data_frame(hank) %>% 
  # Extract songs where peak equals 1
  filter(peak == 1)
```
## Lists of rows (data frames)
```
# Examine the contents of michael
michael

bind_rows(michael, .id = "album") %>% 
  group_by(album) %>% 
  mutate(rank = min_rank(peak)) %>% 
  filter(rank == 1) %>% 
  select(-rank, -peak)
```
## Results
```
seventies %>% 
  # Coerce seventies$year into a useful numeric
  mutate(year = as.numeric(as.character(year))) %>% 
  # Bind the updated version of seventies to sixties
  bind_rows(sixties) %>% 
  arrange(year)
```


# 4. Advanced joining 

## Spot the key
```
# Load the tibble package
library(tibble)

stage_songs %>% 
  # Add row names as a column named song
  rownames_to_column(var = "song") %>% 
  # Left join stage_writers to stage_songs
  left_join(stage_writers, stage_songs, by = "song")
```
## Missing keys
```
# Examine the result of joining singers to two_songs
two_songs %>% inner_join(singers, by = "movie")

# Remove NA's from key before joining
two_songs %>% 
  filter(!is.na(movie)) %>% 
  inner_join(singers, by = "movie")
```
## A subset of keys
```
movie_years %>% 
  # Left join movie_studios to movie_years
  left_join(movie_studios, by = "movie") %>% 
  # Rename the columns: artist and studio
  rename(artist = name.x, studio = name.y)
```
## Mis-matched key names
```
# Identify the key column
elvis_songs
elvis_movies

elvis_movies %>% 
  # Left join elvis_songs to elvis_movies by this column
  left_join(elvis_songs, by = c("name" = "movie")) %>% 
  # Rename columns
  rename(song = name.y, movie = name)
```
## More mismatched names
```
# Identify the key columns
movie_directors
movie_years

movie_years %>% 
  # Left join movie_directors to movie_years
  left_join(movie_directors, by = c("movie" = "name")) %>% 
  # Arrange the columns using select()
  select(year, movie, artist = name, director, studio) 
```
## Join multiple tables
```
# Load the purrr library
library(purrr)

# Place supergroups, more_bands, and more_artists into a list
list(supergroups, more_bands, more_artists) %>% 
  # Use reduce to join together the contents of the list
  reduce(left_join, by = c("first", "last"))
```
## Filter multiple tables
```
list(more_artists, more_bands, supergroups) %>% 
  # Return rows of more_artists in all three datasets
  reduce(semi_join)
```
## Base R
```
# Alter the code to perform the join with a dplyr function
left_join(bands, artists, by = c("first", "last")) %>%
  arrange(band)
```


# 5. Case study 

## Universal keys?
```
# Examine lahmanNames
lahmanNames

# Find variables in common
reduce(lahmanNames, intersect)
```
## Common keys
```
lahmanNames %>%  
  # Bind the data frames in lahmanNames
  bind_rows(.id = "dataframe") %>%
  # Group the result by var
  group_by(var) %>%
  # Tally the number of appearances
  tally() %>%
  # Filter the data
  filter(n > 1) %>% 
  # Arrange the results
  arrange(desc(n))
```
## playerID
```
lahmanNames %>% 
  # Bind the data frames
  bind_rows(.id = "dataframe") %>%
  # Filter the results
  filter(var == "playerID") %>% 
  # Extract the dataframe variable
  `$`(dataframe)
```
## Who are the players?
```
players <- Master %>% 
  # Return one row for each distinct player
  distinct(playerID, nameFirst, nameLast)
```
## Missing salaries
```
players %>% 
  # Find all players who do not appear in Salaries
  anti_join(Salaries) %>%
  # Count them
  count()
```
## Unpaid games?
```
players %>% 
  anti_join(Salaries, by = "playerID") %>% 
  # How many unsalaried players appear in Appearances?
  semi_join(Appearances) %>% 
  count()
```
## How many games?
```
players %>% 
  # Find all players who do not appear in Salaries
  anti_join(Salaries, by = "playerID") %>% 
  # Join them to Appearances
  left_join(Appearances, by = "playerID") %>% 
  # Calculate total_games for each player
  group_by(playerID) %>%
  summarize(total_games = sum(G_all)) %>%
  # Arrange in descending order by total_games
  arrange(desc(total_games))
```
## How many at-bats?
```
players %>%
  # Find unsalaried players
  anti_join(Salaries, by = "playerID") %>% 
  # Join Batting to the unsalaried players
  left_join(Batting, by = "playerID") %>% 
  # Group by player
  group_by(playerID) %>% 
  # Sum at-bats for each player
  summarize(total_at_bat = sum(AB, na.rm = TRUE)) %>% 
  # Arrange in descending order
  arrange(desc(total_at_bat))
```
## Hall of fame nominations
```
# Find the distinct players that appear in HallOfFame
nominated <- HallOfFame %>% 
  distinct(playerID)
nominated %>% 
  # Count the number of players in nominated
  count()
nominated_full <- nominated %>% 
  # Join to Master
  left_join(Master, by = "playerID") %>% 
  # Return playerID, nameFirst, nameLast
  select(playerID, nameFirst, nameLast)
```
## Hall of fame inductions
```
# Find distinct players in HallOfFame with inducted == "Y"
inducted <- HallOfFame %>% 
  filter(inducted == "Y") %>% 
  distinct(playerID)

inducted %>% 
  # Count the number of players in inducted
  count()

inducted_full <- inducted %>% 
  # Join to Master
  left_join(Master, by = "playerID") %>% 
  # Return playerID, nameFirst, nameLast
  select(playerID, nameFirst, nameLast)
```
## Awards
```
# Tally the number of awards in AwardsPlayers by playerID
nAwards <- AwardsPlayers %>% 
  group_by(playerID) %>%
  tally()

nAwards %>% 
  # Filter to just the players in inducted 
  semi_join(inducted, by = "playerID") %>% 
  # Calculate the mean number of awards per player
  summarise(avg_n = mean(n, na.rm = TRUE))

nAwards %>% 
  # Filter to just the players in nominated 
  semi_join(nominated, by = "playerID") %>% 
  # Filter to players NOT in inducted 
  anti_join(inducted, by = "playerID") %>% 
  # Calculate the mean number of awards per player
  summarise(avg_n = mean(n, na.rm = TRUE))
```
## Salary
```
# Find the players who are in nominated, but not inducted
notInducted <- nominated %>% 
  setdiff(inducted, by = "playerID")

Salaries %>% 
  # Find the players who are in notInducted
  semi_join(notInducted, by = "playerID") %>% 
  # Calculate the max salary by player
  group_by(playerID) %>% 
  summarize(max_salary = max(salary)) %>% 
  # Calculate the average of the max salaries
  summarize(avg_salary = mean(max_salary))

# Repeat for players who were inducted
Salaries %>% 
  semi_join(inducted, by = "playerID") %>% 
  group_by(playerID) %>% 
  summarize(max_salary = max(salary)) %>% 
  summarize(avg_salary = mean(max_salary))
```
## Retirement
```
Appearances %>% 
  # Filter Appearances against nominated
  semi_join(nominated, by = "playerID") %>% 
  # Find last year played by player
  group_by(playerID) %>% 
  summarize(last_year = max(yearID)) %>% 
  # Join to full HallOfFame
  left_join(HallOfFame, by = "playerID") %>% 
  # Filter for unusual observations
  filter(last_year >= yearID)
```
