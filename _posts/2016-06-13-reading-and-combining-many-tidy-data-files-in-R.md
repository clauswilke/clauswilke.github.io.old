---
layout: post
title: Reading-and-combining-many-tidy-data-files-in-R
heading: "Reading and combining many tidy data files in R"
date: 2016-06-13
categories: 
    - science
---
Everybody who is familiar with the R libraries for processing of tidy data, such as `dplyr` and `ggplot`, knows how powerful they are and how much one can get done with just a few lines of R code. However, similarly, everybody who has used them has probably spent more time bringing data into the appropriate tidy format than writing analysis and/or plotting code. In particular, one scenario that arises all the time is that even if data files are in tidy format, the entire dataset may be spread out over many individual files, and loading them all in and combining them into one large table can be cumbersome. Here, I want to demonstrate some neat tricks, using the relatively new package `purrr` and some recent additions to the package `tidyr`, that make loading and combining many data files a piece of cake.

The code shown here depends on the following R packages:
<!--more-->

```R
require(readr)  # for read_csv()
require(dplyr)  # for mutate()
require(tidyr)  # for unnest()
require(purrr)  # for map(), reduce()
```

## Reading in all files matching a given name

As an example, we will consider a scenario where we have population census data for various cities, stored in individual csv files for each city. The data I'm using here comes from <http://factfinder.census.gov/>.

The first scenario we will consider is one where we want to read all csv files in the current working directory. To achieve this goal, we first list all `*.csv` files, using the function `dir()`. We find that there are three, for the cities Houston, Los Angeles, and New York:

```R
# find all file names ending in .csv 
files <- dir(pattern = "*.csv")
files
```

    ## [1] "Houston_TX.csv"     "Los Angeles_CA.csv" "New York_NY.csv"

We can then read in those files and combine them into one data frame using the `purrr` functions `map()` and `reduce()`:

```R
data <- files %>%
  map(read_csv) %>%    # read in all the files individually, using
                       # the function read_csv() from the readr package
  reduce(rbind)        # reduce with rbind into one dataframe
data
```

    ## Source: local data frame [15 x 3]
    ## 
    ##           location  year population
    ##              (chr) (int)      (int)
    ## 1      Houston, TX  2011    2142221
    ## 2      Houston, TX  2012    2177376
    ## 3      Houston, TX  2013    2216460
    ## 4      Houston, TX  2014    2256192
    ## 5      Houston, TX  2015    2296224
    ## 6  Los Angeles, CA  2011    3828604
    ## 7  Los Angeles, CA  2012    3864724
    ## 8  Los Angeles, CA  2013    3902005
    ## 9  Los Angeles, CA  2014    3936940
    ## 10 Los Angeles, CA  2015    3971883
    ## 11    New York, NY  2011    8287000
    ## 12    New York, NY  2012    8365069
    ## 13    New York, NY  2013    8436047
    ## 14    New York, NY  2014    8495194
    ## 15    New York, NY  2015    8550405

Often, we want to read the data from a given directory rather than from the current working directory. The ability to define functions on-the-fly in `purrr` makes this easy:

```R
data_path <- "city_data"   # path to the data
files <- dir(data_path, pattern = "*.csv") # get file names

data <- files %>%
  # read in all the files, appending the path before the filename
  map(~ read_csv(file.path(data_path, .))) %>% 
  reduce(rbind)
data
```

    ## Source: local data frame [15 x 3]
    ## 
    ##           location  year population
    ##              (chr) (int)      (int)
    ## 1      Houston, TX  2011    2142221
    ## 2      Houston, TX  2012    2177376
    ## 3      Houston, TX  2013    2216460
    ## 4      Houston, TX  2014    2256192
    ## 5      Houston, TX  2015    2296224
    ## 6  Los Angeles, CA  2011    3828604
    ## 7  Los Angeles, CA  2012    3864724
    ## 8  Los Angeles, CA  2013    3902005
    ## 9  Los Angeles, CA  2014    3936940
    ## 10 Los Angeles, CA  2015    3971883
    ## 11    New York, NY  2011    8287000
    ## 12    New York, NY  2012    8365069
    ## 13    New York, NY  2013    8436047
    ## 14    New York, NY  2014    8495194
    ## 15    New York, NY  2015    8550405

Here, the expression `~ read_csv(file.path(data_path, .))` is a shortcut for the anonymous function definition `function(x) read_csv(file.path(data_path, x))`:

```R
# this code does the exact same thing as the previous code
data <- files %>%
  map(function(x) read_csv(file.path(data_path, x))) %>%  
  reduce(rbind)
data
```

    ## Source: local data frame [15 x 3]
    ## 
    ##           location  year population
    ##              (chr) (int)      (int)
    ## 1      Houston, TX  2011    2142221
    ## 2      Houston, TX  2012    2177376
    ## 3      Houston, TX  2013    2216460
    ## 4      Houston, TX  2014    2256192
    ## 5      Houston, TX  2015    2296224
    ## 6  Los Angeles, CA  2011    3828604
    ## 7  Los Angeles, CA  2012    3864724
    ## 8  Los Angeles, CA  2013    3902005
    ## 9  Los Angeles, CA  2014    3936940
    ## 10 Los Angeles, CA  2015    3971883
    ## 11    New York, NY  2011    8287000
    ## 12    New York, NY  2012    8365069
    ## 13    New York, NY  2013    8436047
    ## 14    New York, NY  2014    8495194
    ## 15    New York, NY  2015    8550405

## Keeping auxilliary information about the files read

One limitation of the previous approach is that we don't keep any auxilliary information we may want to, such as the filenames of the files read. To keep the filename alongside the data, we can read the data into a nested dataframe rather than a list, using the `mutate()` function from `dplyr`. This gives us the following result:

```R
data <- data_frame(filename = files) %>% # create a data frame
                                         # holding the file names
  mutate(file_contents = map(filename,          # read files into
           ~ read_csv(file.path(data_path, .))) # a new data column
        )  
data
```

    ## Source: local data frame [3 x 2]
    ## 
    ##             filename  file_contents
    ##                (chr)          (chr)
    ## 1     Houston_TX.csv <tbl_df [5,3]>
    ## 2 Los Angeles_CA.csv <tbl_df [5,3]>
    ## 3    New York_NY.csv <tbl_df [5,3]>

To turn this data frame into one useful for downstream analysis, we use the function `unnest()` from `tidyr`:

```R
unnest(data)
```

    ## Source: local data frame [15 x 4]
    ## 
    ##              filename        location  year population
    ##                 (chr)           (chr) (int)      (int)
    ## 1      Houston_TX.csv     Houston, TX  2011    2142221
    ## 2      Houston_TX.csv     Houston, TX  2012    2177376
    ## 3      Houston_TX.csv     Houston, TX  2013    2216460
    ## 4      Houston_TX.csv     Houston, TX  2014    2256192
    ## 5      Houston_TX.csv     Houston, TX  2015    2296224
    ## 6  Los Angeles_CA.csv Los Angeles, CA  2011    3828604
    ## 7  Los Angeles_CA.csv Los Angeles, CA  2012    3864724
    ## 8  Los Angeles_CA.csv Los Angeles, CA  2013    3902005
    ## 9  Los Angeles_CA.csv Los Angeles, CA  2014    3936940
    ## 10 Los Angeles_CA.csv Los Angeles, CA  2015    3971883
    ## 11    New York_NY.csv    New York, NY  2011    8287000
    ## 12    New York_NY.csv    New York, NY  2012    8365069
    ## 13    New York_NY.csv    New York, NY  2013    8436047
    ## 14    New York_NY.csv    New York, NY  2014    8495194
    ## 15    New York_NY.csv    New York, NY  2015    8550405

## Creating filenames from data

In the previous examples, we have read in all the data files in a given directory. Often, however, we would rather read in specific files based on other data we have. For example, let's assume we have the following data table:

```R
cities <- data_frame(city = c("New York", "Houston"),
                     state = c("NY", "TX"),
                     area = c(305, 599.6))
cities
```

    ## Source: local data frame [2 x 3]
    ## 
    ##       city state  area
    ##      (chr) (chr) (dbl)
    ## 1 New York    NY 305.0
    ## 2  Houston    TX 599.6

We want to use the city and state columns to create appropriate filenames and then load in the corresponding files. The code in its entirety looks as follows:

```R
data <- cities %>% # start with the cities table
  # create filenames
  mutate(filename = paste(city, "_", state, ".csv", sep="")) %>%
  # read in data
  mutate(file_contents = map(filename,
           ~ read_csv(file.path(data_path, .)))
        ) %>% 
  select(-filename) %>% # remove filenames, not needed anynmore
  unnest() %>% # unnest
  select(-location) # remove location column, not needed
                    # since we have city and state columns
data
```

    ## Source: local data frame [10 x 5]
    ## 
    ##        city state  area  year population
    ##       (chr) (chr) (dbl) (int)      (int)
    ## 1  New York    NY 305.0  2011    8287000
    ## 2  New York    NY 305.0  2012    8365069
    ## 3  New York    NY 305.0  2013    8436047
    ## 4  New York    NY 305.0  2014    8495194
    ## 5  New York    NY 305.0  2015    8550405
    ## 6   Houston    TX 599.6  2011    2142221
    ## 7   Houston    TX 599.6  2012    2177376
    ## 8   Houston    TX 599.6  2013    2216460
    ## 9   Houston    TX 599.6  2014    2256192
    ## 10  Houston    TX 599.6  2015    2296224

I hope you have found these examples useful, and you will start loading files into nested data frames.
