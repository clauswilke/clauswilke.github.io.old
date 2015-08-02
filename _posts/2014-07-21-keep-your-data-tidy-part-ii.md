---
layout: post
title: keep-your-data-tidy-part-ii
heading: "Keep your data tidy, Part II"
date: 2014-07-21
categories: science
tags:
    - R
    - data analysis
    - tidy data
    - observational unit
---
My previous post on [tidy data](/blog/2014/7/20/keep-your-data-tidy) didn’t at all touch on rule 3, "Each type of observational unit forms a table." The example I gave had only one observational unit, the weekly temperature measurements. Frequently, however, we have data corresponding to multiple observational units. In this case, it is important that we store them in separate tables, and that we know how to combine these tables for useful analyses.

<!--more-->

First, we need to figure out when we’re dealing with multiple observational units and when we are not. An observational unit is the base unit on which measurements are done. Importantly, multiple measurements can be performed on the same unit. For example, if we’re studying a group of patients, and for each patient we measure height, weight, heart rate, and blood pressure, then the observational unit is the patient, and we are measuring four variables per observational unit. However, if we’re following the patients over time, and we make those four measurements once every month for a year, then the observational units are the patient-months, i.e., we have one observational unit per patient each month.

In what follows, I’m assuming you have read the [previous post](/blog/2014/7/20/keep-your-data-tidy) and you are familiar with the temperature example I made there. In this example, since we’re measuring temperature each week, we have one observational unit per city per week. If in addition to temperature we also measured humidity, then we’d have two measurements per observational unit but the number and type of observational units wouldn’t change. Now, however, assume that we’re also recording additional information about the cities that we’re studying, for example their altitude. The altitude will be the same every week. Therefore, altitude is a property of the city, not of the city-week that is the experimental unit for the temperature measurements. Thus, we now have two separate sets of experimental units, the city-weeks for which we measure temperature and the cities themselves for which we measure altitude.

By rule 3 for tidy data, the altitude measurements do not belong into the table that contains temperature data, they belong into a separate table. For example, this table could look like this:

    > alt.data
      city altitude
    1    A     2300
    2    B      400
    3    C      250

Let’s assume that we want to know whether there is a relationship between the mean temperature for a city and the city’s altitude. How would we do this? First, we calculate the mean temperature, as before, and store it in a new data frame called `mean.temp`:

    > mean.temp <- ddply(temp.data, "city", summarize, mean.temp=mean(temperature))
    > mean.temp
      city mean.temp
    1    A     13.50
    2    B     20.25
    3    C     23.75

Now, we need to merge the two data frames `alt.data` and `mean.temp`. This can be done with the function `join` from the `plyr` package, or alternatively with the function `merge` from base R:

    > city.data <- join(mean.temp, alt.data)
    Joining by: city
    > city.data
      city mean.temp altitude
    1    A     13.50     2300
    2    B     20.25      400
    3    C     23.75      250

Now we can investigate the relationship between the two variables, for example by fitting a linear model:

    > summary(lm(altitude ~ mean.temp, data = city.data))
    
    Call:
    lm(formula = altitude ~ mean.temp, data = city.data)
    
    Residuals:
         1      2      3 
     121.1 -354.8  233.6 
    
    Coefficients:
                Estimate Std. Error t value Pr(>|t|)
    (Intercept)  5027.01    1177.01   4.271    0.146
    mean.temp    -210.97      59.95  -3.519    0.176
    
    Residual standard error: 441.7 on 1 degrees of freedom
    Multiple R-squared:  0.9253,	Adjusted R-squared:  0.8506 
    F-statistic: 12.38 on 1 and 1 DF,  p-value: 0.1763

Both the `join` and the `merge` function can handle much more complicated situations. For example, by default, both functions merge on all shared variables. Further, you can specify how you want to handle the situation when cases are missing. A “left” join keeps all rows from the first data frame and matches the corresponding ones from the second, a “right” join keeps all rows from the second data frame and matches the corresponding ones from the first, an “inner” join only keeps rows that exist in both data frames, and a “full” join keeps all observations that exist in either data frame. For more details, read the documentation of either function.


