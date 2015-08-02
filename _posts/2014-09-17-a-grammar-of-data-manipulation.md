---
layout: post
title: a-grammar-of-data-manipulation
heading: "A grammar of data manipulation"
date: 2014-09-17
categories: science
tags:
    - R
    - data analysis
    - tidy data
    - dplyr
---
It seems that Hadley Wickham, the author of the spectacular [`ggplot2`](http://ggplot2.org/) library for R, is not content with revolutionizing the world of computational data analysis just once. He keeps doing it. This spring, he released the [`dplyr`](http://cran.r-project.org/web/packages/dplyr/index.html) package, a package that proposes a grammar of data manipulation. I predict that `dplyr` will become as important for large-scale data analysis and manipulation as `ggplot2` has become for visualization. If you like `ggplot2`, you will love `dplyr`. [[1]](#note1)

<!--more-->

`dplyr` is the next iteration of the popular `plyr` package, only that it is 100 times faster and way more intuitive. It provides a clean interface to work with data sets that are “tidy.” (See also my previous two blog posts on tidy data [here](/blog/2014/7/20/keep-your-data-tidy) and [here.](/blog/2014/7/21/keep-your-data-tidy-part-ii)) Let me whet your appetite by showing you a simple analysis I did the other day.

I wanted to find out how much evolutionary divergence there is between human genes and the corresponding yeast (*S. cerevisiae*) orthologs. Specifically, I was interested in the range of sequence identities among genes, i.e., what are the most conserved genes, the most diverged genes, what is the mean divergence, and so on. The analysis has an additional twist in that there are different types of ortholog pairs. There are one-to-one orthologs, where the human gene has exactly one counter-part in the yeast genome, there are one-to-many orthologs, where the gene in one organism has multiple counter-parts in the other organism, and there are many-to-many orthologs, where there are multiple genes in both organisms that are orthologous to each other. Thus, I wanted to carry out my analysis by orthology type.

I went to [ensembl](http://www.ensembl.org/index.html) and downloaded all human-to-yeast orthologs with their respective sequence identities. The resulting csv file is available [here.](https://dl.dropboxusercontent.com/u/97817736/human_yeast_divergence.csv) We can download this file directly into R, using the `RCurl` package. We'll also load the `dplyr` package, since we'll need it later:

{% highlight r %}
require(RCurl)  
require(dplyr)  
url <- "https://dl.dropboxusercontent.com/u/97817736/human_yeast_divergence.csv"    
data <- read.csv(textConnection(getURL(url)))
{% endhighlight %}

Let's take a look at the data. There are five columns, the gene id for the human gene, the gene id for the
corresponding yeast ortholog, the homology type (one-to-one, one-to-many, many-to-many), the percent identity with respect to both the human (`perc.ident.human`) and the yeast (`perc.ident.yeast`) gene, and a confidence score that tells us how confident we are that the two genes are actually orthologous.

{% highlight r %}
head(data)
{% endhighlight %}

        human.gene.ID yeast.gene.ID      homology.type perc.ident.human  
    1 ENSG00000100077       YKL126W ortholog_many2many               19  
    2 ENSG00000100077       YHR205W ortholog_many2many               18  
    3 ENSG00000100077       YMR104C ortholog_many2many               18  
    4 ENSG00000196139       YHR104W  ortholog_one2many               33  
    5 ENSG00000173213       YFL037W  ortholog_one2many               71  
    6 ENSG00000154930       YLR153C ortholog_many2many               43  
      perc.identity.yeast confidence  
    1                  19          1  
    2                  15          1  
    3                  18          1  
    4                  33          1  
    5                  69          1  
    6                  44          1  


Now we're ready for some `dplyr` magic. Let's assume we want to analyze the data by homology type, and we want to find the minimum, mean, median, and maximum sequence identity for each homology type, as well as the standard deviation of the identity distribution. All this can be achieved with the following code:

{% highlight r %}
data %>% group_by(homology.type) %>%  
    summarize(  
        min=min(perc.ident.human),  
        mean=mean(perc.ident.human),  
        std.dev=sd(perc.ident.human),
        max=max(perc.ident.human))
{% endhighlight %}

    Source: local data frame [3 x 5]
    
           homology.type min     mean  std.dev max
    1 ortholog_many2many   1 26.36965 16.37955  92
    2  ortholog_one2many   0 27.46243 15.18146  86
    3   ortholog_one2one   1 33.04183 12.89296  80


The function `group_by()` states that we want to carry out the analysis separately for each homology type, and the function `summarize()` calculates the summary statistics (min, mean, etc.) for each group. The operator `%>%` is a chaining operator, like a pipe in the UNIX command line. It takes the output from the previous operation and feeds it into the subsequence operation. 

As you can see, `dplyr` syntax focuses entirely on the logical flow of the data analysis. You don't ever have to worry about bookkeeping, looping over cases, or details of the data storage.

Let’s do another example. Let’s say we’re only interested in one-to-one orthologs, and we want to find the top 10 least diverged yeast genes and list them in descending order. The following lines achieve this:


{% highlight r %}
data %>% filter(homology.type=='ortholog_one2one') %>%  
    select(yeast.gene.ID, human.gene.ID, perc.ident.human) %>%  
    top_n(10) %>%   
    arrange(desc(perc.ident.human))
{% endhighlight %}

    Selecting by perc.ident.human  
       yeast.gene.ID   human.gene.ID perc.ident.human  
    1        YLR167W ENSG00000143947               80  
    2        YDR064W ENSG00000110700               77  
    3        YKL145W ENSG00000161057               75  
    4        YOR210W ENSG00000177700               75  
    5        YGL048C ENSG00000087191               74  
    6        YPL086C ENSG00000134014               74  
    7        YPR016C ENSG00000242372               72  
    8        YJR121W ENSG00000110955               72  
    9        YDL007W ENSG00000100764               71  
    10       YEL027W ENSG00000185883               70  

The function `filter()` selects all rows of the given homology type, the function `select()` picks the specific columns we are interested in, the function `top_n()` selects the top *n* values in the last data column (i.e., column `perc.ident.human` in this example), and the function `arrange()` sorts the data.

If these examples have piqued your interest and you want to learn more, I recommend you start by reading the `dplyr` vignette, which you can find here: [http://cran.r-project.org/web/packages/dplyr/vignettes/introduction.html](http://cran.r-project.org/web/packages/dplyr/vignettes/introduction.html)  
There is also an excellent introduction by Kevin Markham, with accompanying 40 minute video, available here: [http://rpubs.com/justmarkham/dplyr-tutorial](http://rpubs.com/justmarkham/dplyr-tutorial)

And have I mentioned already that `dplyr` has a [database backend,]( http://cran.rstudio.com/web/packages/dplyr/vignettes/databases.html) so you can now easily use all the statistical sophistication that R provides on arbitrarily large, remotely stored data sets.

## Notes
[1]<a id="note1"></a> And if you aren’t familiar with [`ggplot2`,](http://ggplot2.org/) spend some time with it. It is fantastic, though it may feel alien initially. If you’re used to traditional visualization approaches, you may think in terms of drawing points and lines onto a canvas. `ggplot2` requires you to approach visualization in a completely different way, in terms of mapping features of the data onto aesthetic features of the graph. Once you get this way of thinking, it becomes rather powerful.
