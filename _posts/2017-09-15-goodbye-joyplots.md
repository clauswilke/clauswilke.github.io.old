---
layout: post
title: Goodbye-joyplots
heading: "Goodbye Joyplots"
date: 2017-09-15
categories: 
    - dataviz
---

Anybody who has been paying any attention to the data visualization scene knows that the summer of 2017 was the summer of joyplots. This type of visualization turned viral, probably not in small part fueled by the R package [ggjoy](https://CRAN.R-project.org/package=ggjoy) that I wrote in July. However, I think it's time to retire both the name "joyplot" and the ggjoy package, and as of today the ggjoy package is officially deprecated. A replacement package [ggridges](https://CRAN.R-project.org/package=ggridges) is in place and provides essentially the same functionality.

<!--more-->

The term "joyplot" was coined by Jenny Bryan in a tweet on April 24, 2017:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">I hereby propose that we call these &quot;joy plots&quot; <a href="https://twitter.com/hashtag/rstats?src=hash">#rstats</a> <a href="https://t.co/uuLGpQLAwY">https://t.co/uuLGpQLAwY</a></p>&mdash; Jenny Bryan (@JennyBryan) <a href="https://twitter.com/JennyBryan/status/856674638981550080">April 25, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

The idea was to honor the band Joy Division, whose 1979 album [*Unknown Pleasures*](https://en.wikipedia.org/wiki/Unknown_Pleasures) features on its cover a visualization of radio waves as staggered lines, creating a 3D-like effect. This seemed like a good idea and the name caught on like wildfire.

Unfortunately, when the name "joyplot" took off, nobody in the datascience community was aware of the origin of the name "Joy Division". As described in the book [*House of Dolls,*](https://en.wikipedia.org/wiki/House_of_Dolls) joy divisions were groups of Jewish women in Nazi concentration camps kept for the sexual pleasure of soldiers. The band Joy Division took their name directly from this book and even quoted from the book in one of their early songs.

Thus, as joyful as the name "joyplot" sounds to the uninformed, its history is rather dark, and we would do better using a different name. For this reason, I have decided to now call these plots "ridgeline plots". Indeed, from day one, the ggjoy package contained a `geom_ridgeline()`, so I'm just keeping in this tradition. The new ggridges package uses this naming convention throughout, and all functions have been renamed accordingly. For example, `geom_joy()` is now called `geom_density_ridges()`. A complete list of all name replacements is provided [here](https://github.com/clauswilke/ggjoy/blob/master/README.md). Porting your code from ggjoy to ggridges should be as simple as a search-and-replace for all those functions in your code. If you run into any trouble, please let me know or open an [issue on github](https://github.com/clauswilke/ggridges/issues).
