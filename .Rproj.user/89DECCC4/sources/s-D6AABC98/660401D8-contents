library(tidyverse)
library(lubridate)

# data from https://www.kaggle.com/regivm/retailtransactiondata#Retail_Data_Transactions.csv

raw <- read_csv("data/Retail_Data_Transactions.csv") %>% 
  mutate(trans_date = as.Date(trans_date, "%d-%b-%y"),
         vol_yes = rbinom(n(), 1, prob = .3)) %>% 
  select(-tran_amount) 

# get only data for 2015 seems like a reasonable range
demo_dat <- raw %>% 
  filter(year(trans_date) == 2015) %>% 
  rename(date = trans_date) %>% 
  # make 2019 to be more realistic
  mutate(date = date + years(4),
         # want to add some duplicates say, ~88% aren't dupes
         van_id = rep_len(1:(round(n() * 0.9)),
                          length.out = n())) %>% 
  select(van_id, date, vol_yes)

# write fake canvassing data
write_csv(demo_dat, "data/canvassing_results.csv")

# create van id to turf code look up
turf_van_id <- demo_dat %>% 
  select(van_id) %>% 
  mutate(turf_code = sample(toupper(head(letters)), 
                            size = n(), replace = TRUE)) %>% 
  group_by(van_id) %>% 
  # only take 1 for each person because there are undoubtedly dupes
  sample_n(size = 1)

write_csv(turf_van_id, "data/van_turf_lookup.csv")

# Create fake goals data

goals <- tibble(week = 1:52) %>% 
  mutate(region = list(toupper(letters[1:6]))) %>% 
  unnest() %>% 
  mutate(goal = sample(seq(from = 50, to = 130, by = 10), 
                       size = n(), 
                       replace = TRUE)
  )


write_csv(goals, "data/goals.csv")
