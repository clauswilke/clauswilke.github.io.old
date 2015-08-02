---
layout: post
title: r-markdown-the-easiest-and-most-elegant-approach-to-writing-about-data-analysis-with-r
heading: "R Markdown, the easiest and most elegant approach to writing about data analysis with R"
date: 2014-10-04
categories: writing
tags:
    - statistics
    - R
    - markdown
---
This weekend, I finally spent some time learning [R Markdown](http://rmarkdown.rstudio.com/). I had been aware of its existence for a while, but I had never bothered to check it out. What a mistake. R Markdown rocks! It's hands down the easiest and most elegant method to creating rich documents that contain data analysis, figures, mathematical formulas, and text. And it's super easy to learn. I wager that anybody who has RStudio installed can create a useful document in 30 minutes or less. So if you use R, and you've never used R Markdown, give it a try.

<!--more-->

R Markdown provides a literate programming platform for the R language. Literate programming, [invented by Donald Knuth,](http://en.wikipedia.org/wiki/Literate_programming) allows users to write both a program and a document describing the program, at the same time. In the case of R, this means that you can write a document that contains R code, the output that is generated when the R code is run (including graphs), and prose describing the R code and its output. To give you an example, I started writing a tutorial for R's ggplot2 library this weekend, and the original R Markdown file as well as the HTML output generated from that file are [available here.](https://github.com/wilkelab/ggplot2_cookbook/blob/master/README.md)

What does the word *Markdown* stand for? [Markdown](http://en.wikipedia.org/wiki/Markdown) is a minimalist approach to writing strutured documents. It consists of plain text with a few simple directives to mark sections, turn text bold or italics, or insert quotes. If you have ever edited a wikipedia article, you have used Markdown.

To give you an example, this is Markdown text:

    We can make text **bold**, *italics*, or `look like code.`
    We can also insert links, [e.g. to wikipedia,](http://www.wikipedia.org/) we can quote things:  
    
    > It is time to eat &#8212; Hungry John
    
    or make lists:
    
    1. Item 1
    2. Item 2
    3. Item 3

It will be rendered like this:

---
We can make text **bold**, *italics*, or `look like code.` We can also insert links, [e.g. to wikipedia,](http://www.wikipedia.org/) we can quote things: 

> It is time to eat &#8212; Hungry John

or make lists:
    
1. Item 1
2. Item 2
3. Item 3

---

R Markdown works the same, only that it adds the option to insert R code  blocks. An R code block could look something like this:

    ```{r}  
    # place R code here, e.g. to make a plot:  
    require(ggplot2)  
    x <- 1:10; y <- x^2  
    qplot(x, y)  
    ```

When you convert the R Markdown file to HTML, the R code gets executed, the R output captured and inserted into the document, and you've got everything nicely together, with very little work.

To create an R Markdown document in RStudio, all you have to do is go to ``File``, ``New File``, and then select ``R Markdown``. Accept the default settings, and R Studio will generate a new R Markdown file with a few lines of example content. To convert the file into HTML, simply click on the "Knit HTML" button. If you have previously stored your R Markdown file somewhere on your harddisk (with suffix .Rmd), RStudio will automatically save the generated HTML file in the same location, with the same name and suffix .html. The HTML file is self-contained, including all images, so it's easy to publish it on a web page or share it with people. RStudio also provides you with the option to publish the document online on the [RPubs](http://rpubs.com/) website. Just click on the "Publish" button in the HTML view.

To learn more about R Markdown, go to:  [http://rmarkdown.rstudio.com](http://rmarkdown.rstudio.com)
