---
layout: post
title: keep-your-data-tidy
heading: "Keep your data tidy"
date: 2014-07-20
categories: science
tags:
    - R
    - data analysis
    - tidy data
    - statistics
---
I came across this nice preprint by Hadley Wickham:

> Hadley Wickham (2014). [Tidy data.](http://vita.had.co.nz/papers/tidy-data.pdf) Submitted.

In this preprint, Wickham describes a way of organizing data he calls “tidy.” He then argues that tidy data and tidy tools (that both input and output tidy data) make data analysis much more efficient than any alternative approach can.

<!--more-->

When are data tidy? When they satisfy these three conditions:

1. Each variable forms a column.
2. Each observation forms a row.
3. Each type of observational unit forms a table.

Every other arrangement of data is called "messy."

Let’s look at an example. Assume you’re making temperature measurements once a week in three cities (city A, city B, and city C). Instinctively, most people would probably record the data like this:

    week    city_A    city_B    city_C
       1        14        18        23
       2        15        21        24
       3        12        25        23
       4        13        17        25
       ...

Or maybe even like this:

    week         1        2        3        4      ...
    city_A      14       15       12       13
    city_B      18       21       25       17
    city_C      23       24       23       25
    
While both options may look quite organized, neither corresponds to tidy data. In both cases, Wickham’s rules 1 and 2 are violated. For example, in the first case, the variable `temperature` appears in three columns.  Consequently, multiple observations appear in each row. In the second case, multiple variables appear in each column and multiple observations appear in each row.

The tidy version of this data set would look like this:

    week    city    temperature
       1       A             14
       1       B             18
       1       C             23
       2       A             15
       2       B             21
       2       C             24
       ...
       
I believe that most people have an instinctive dislike towards tidy data, because tidy data sets tend to have many rows and are difficult to read with the human eye. You can clearly see this in my made-up data set. The messy [[1]](#note1) versions allow us to quickly compare cities’ temperatures in different weeks as well as identify trends over time. The tidy version does not. It also requires many more rows.

Nevertheless, for computational analysis, having tidy data makes things way more efficient, *if you have the right set of tools.* These tools need to consistently input and output tidy data. Fortunately, these tools exist in R. (And Wickham has greatly enhanced R’s capability to keep analyses tidy by writing the packages `reshape2`, `plyr`, and `ggplot2`.) With the appropriate tools, even quite complicated analyses can be expressed in just a few lines of code. And most importantly, there is no need for explicit loops or other bookkeeping code. You just express the semantics of your analysis and the programming language does the rest.

How does this work? In general, when we want to analyze data, we want to manipulate (specifically filter, transform, aggregate, and sort), model, and visualize. These steps require only a handful of generic tools, such as a generic data aggregation function. Let me show you a few examples, using the `summarize` and `ddply` functions from the `plyr` package. I assume we store the temperature data in tidy form in a data frame called `temp.data`:

    > temp.data
       week city temperature
    1     1    A          14
    2     1    B          18
    3     1    C          23
    4     2    A          15
    5     2    B          21
    6     2    C          24
    7     3    A          12
    8     3    B          25
    9     3    C          23
    10    4    A          13
    11    4    B          17
    12    4    C          25


Let’s calculate the mean temperature in each city:

    > ddply(temp.data, "city", summarize, mean=mean(temperature))
      city  mean
    1    A 13.50
    2    B 20.25
    3    C 23.75

Or in each week:

    > ddply(temp.data, "week", summarize, mean=mean(temperature))
      week     mean
    1    1 18.33333
    2    2 20.00000
    3    3 20.00000
    4    4 18.33333

Or let’s find the city with the highest temperature each week:

    > ddply(temp.data, "week", summarize, hottest.city=city[which.max(temperature)])
      week hottest.city
    1    1            C
    2    2            C
    3    3            B
    4    4            C

These are just a few simple examples. For more examples, read Wickham's paper, and also read his paper on `plyr` [[2]](#note2).

Does any of this matter? I’m sure somebody will tell me: Yeah, but R is an ugly and archaic programming language, and my python code will analyze the data tables that Wickham calls “messy” just fine. My answer is that it only matters if you care about how much time you spend analyzing your data. Read through the example analysis Wickham provides in his Section 5 ("Case study"). This analysis uses less than 30 lines of code, including the code for visualization, to identify and plot causes of death with unusual temporal patterns throughout the day (see his Fig. 4). How many lines of code would you have written to do a comparable analysis? And how long would it have taken you to write this code and debug it?

At some point, a quantitative advantage becomes a qualitative one. While one can do the exact same analyses with tidy and messy datasets/tools, the tidy approach will generally require much less code, and hence be faster to write, easier to debug, and easier to modify/maintain. In practice, this means that the person using the tidy approach will be able to analyze more data sets, try a larger number of different analysis approaches, and/or make fewer mistakes. Aggregated over the course of several months, this advantage can easily translate into some major new findings made only by the person using the tidy approach.

## Notes
[1]<a id="note1"></a> Throughout this post, I’m following Wickham in using “messy” as a technical term, meaning “not tidy,” as in “not conforming to the definition of tidy data.” 

[2]<a id="note2"></a> Hadley Wickham (2011) [The split-apply-combine strategy for data analysis.](http://vita.had.co.nz/papers/plyr.html) Journal of Statistical Software 40:1–29.
