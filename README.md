# mini-essay-2

This is a simple code review.  
Firstly, we need to check out the design of overall the  design of the code.  

```R
#### Acquire ####
toronto_shelters <- 
  # Each package is associated with a unique id found in the "For 
  # Developers" tab of the relevant page from Open Data Toronto
  # [Open Data Toronto - Shelter Occupancy](https://open.toronto.ca/dataset/daily-shelter-overnight-service-occupancy-capacity/)
  list_package_resources("21c83b32-d5a8-4106-a54f-010dbe49f6f2") |>
  # Within that package, we are interested in the 2021 dataset
  filter(name == 
    "daily-shelter-overnight-service-occupancy-capacity-2021.csv") |>
  # Having reduced the dataset to one row we can get the resource
  get_resource()

write_csv(
  x = toronto_shelters,
  file = "toronto_shelters.csv"
)

head(toronto_shelters)


```
This is very clear for readers to know where the code comes from. The code is well-structured and appears to accomplish the task of acquiring data from Open Data Toronto related to daily shelter overnight service occupancy capacity for 2021. Using understanding english, the comment is helpful for readers to handle the complex codes.  
It's good that you included a URL link to the Open Data Toronto dataset. However, you might want to place it within a comment to make it more explicit.

```R
toronto_shelters_clean <-
  clean_names(toronto_shelters) |>
  mutate(occupancy_date = ymd(occupancy_date)) |> 
  select(occupancy_date, occupied_beds)

head(toronto_shelters_clean)
```

This is the most important part of the code to gain the data and form a clear data set.  
The clean_names() function is used to clean the column names, which is a good practice for consistency. The use of ymd() from the lubridate package to convert the "occupancy_date" to a date format is appropriate. 
However, consider adding comments to explain the purpose of each step or any specific considerations. This can be helpful for someone not familiar with R reviewing the code.
