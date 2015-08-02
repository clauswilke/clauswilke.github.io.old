---
layout: post
title: to-grid-or-not-to-grid
heading: "To grid or not to grid"
date: 2014-10-07
categories: science
tags:
    - R
    - ggplot2
    - plotting
    - chartjunk 
    - visual noise
---
I had a twitter discussion with ggplot2 author [Hadley Wickham](http://had.co.nz/) on whether or not to include a grid background in plots. He thinks the default should have a grid, I think the opposite. I believe we both agree that grids make sense for some plots and not for others, so this is just a question about defaults. On that issue, we remain in disagreement.

<!--more-->

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/ClausWilke">@ClausWilke</a> I think removing the grid lines is a bad idea. It hampers your ability to make accurate comparisons</p>&mdash; Hadley Wickham (@hadleywickham) <a href="https://twitter.com/hadleywickham/status/519439694413565953">October 7, 2014</a></blockquote>

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/ClausWilke">@ClausWilke</a> but see (e.g.) fig 3 of <a href="http://t.co/m3A1XgPpCK">http://t.co/m3A1XgPpCK</a> - the grid is the right default, but may make sense to remove in some cases</p>&mdash; Hadley Wickham (@hadleywickham) <a href="https://twitter.com/hadleywickham/status/519483409911922688">October 7, 2014</a></blockquote>

<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>


One of my preferred methods of data visualization is to take two variables that measure the same quantity in different ways or different systems and then plot one versus the other. As an example, see [this figure](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3678335/figure/RSTB20120334F3/) from a paper my lab published last year. In this kind of a plot, a grid would be highly distracting. In general, I like to add guiding lines that highlight specific features of the data. For example, if the most important feature in the data is whether *y* values fall above or below one, then placing a horizontal line at *y* = 1 would be a good idea, and it would likely be more helpful than a generic grid covering the entire plot. However, I do agree that if one does a lot of [faceting,](http://www.cookbook-r.com/Graphs/Facets_(ggplot2)) a grid may be necessary. In fact, yesterday I played around with faceted plots without background grid, and I noticed that they had a tendency to fall apart and not look very convincing. Without grid, the eye has little to go by in these plots.

So, if I can see the value of a background grid in some cases, why am I not convinced that it is the right default? When it comes to constructing plots, I fundamentally believe in an additive rather than a subtractive model. That is, start with a plot that is as empty as possible, and then add everything you need until you have a clear and informative graph. In a subtractive model, you would start with all sorts of additional visual elements of which you remove those you don’t need. While both approaches can lead to the same end result, it is my experience from ~15 years of supervising students, and from reviewing oodles of papers with poor-quality figures, that most people don’t remove visual noise from a graph unless explicitly prompted to do so. If ggplot2 places a gray background grid, then a gray background grid it is. Therefore, in my [own personal plotting package,](https://github.com/wilkelab/cowplot) whose intended purpose is internal use in my lab, the default is no background grid. I’d rather say  on occasion "please add a background grid to this figure" than having to repeat over and over "please remove the background grid."
