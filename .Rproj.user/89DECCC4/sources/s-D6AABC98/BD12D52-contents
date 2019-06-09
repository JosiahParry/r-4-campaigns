library(tidyverse)
library(lubridate)

# create fake name & age data for van users
# Read common last names census data
surnames <- read_csv("../data/Names_2010Census.csv") %>% 
  pull(name) %>% 
  stringr::str_to_title()

# get baby names from people from the 50s+
first_names <- babynames::babynames %>% 
  filter(year >= 1950) %>% 
  pull(name)

# create range of dates for birth dates 
bday_range <- seq(from = as.Date("1950-01-01"), to = as.Date("2001-01-01"), 1)

van_ids <- read_csv("../data/van_turf_lookup.csv")



# create names and birthdates
van_names <- van_ids %>% 
  mutate(first_name = sample(first_names, n()),
         last_name = sample(surnames, n()),
         date_of_birth = sample(bday_range, n()),
         age = year(Sys.Date()) - year(date_of_birth)) %>% 
  select(-turf_code) 

write_csv(van_names, "../data/van_names.csv")  






