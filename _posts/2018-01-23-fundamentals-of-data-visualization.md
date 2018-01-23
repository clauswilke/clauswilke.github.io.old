---
layout: post
title: fundamentals-of-data-visualization
heading: "Fundamentals of Data Visualization"
date: 2018-01-23
categories: 
    - visualization
---

I'm very excited to announce my latest project, a book on data visualization. The working title is "Fundamentals of Data Visualization". The book will be published with O'Reilly, and a preview is [available here.](http://serialmentor.com/dataviz/)  The entire book is written in R Markdown, and the figures are made with ggplot2. The source for the book is [available on github.](https://github.com/clauswilke/dataviz)

<!--more-->

Even though the entire book is written in R Markdown, it is not a book on programming. The book is meant as a guide to making visualizations that accurately reflect the data, tell a story, and look professional. It has grown out of my experience of working with students and postdocs in my laboratory on thousands of data visualizations. Over the years, I have noticed that the same issues arise over and over. I have attempted to collect my accumulated knowledge from these interactions in the form of this book.

As of this writing, approximately half of the planned chapters are completed, and all completed chapters are available online. I will post future chapters as they become available. Since this is a work in progress, not everything may be completely finalized, and I may rewrite some of the posted chapters at a later date. I welcome feedback. If you see any errors or other problems, please [open an issue on github.](https://github.com/clauswilke/dataviz/issues) If you have suggestions for other topics to cover, or for datasets that would work well for certain chapters, please also feel free to record these suggestions as issues on github.

With very few exceptions, all figures in the book are generated straight from ggplot2, with no manual post-processing in photoshop or illustrator. (At present, the only exception is two figures in the chapter on [image file formats.](http://serialmentor.com/dataviz/image-file-formats.html)) Therefore, the book also serves as a showcase of what ggplot2 can do. I am using the bleeding edge of ggplot2 software development, though. To reproduce all the figures in the book, you may have to install current development versions of several R packages.
