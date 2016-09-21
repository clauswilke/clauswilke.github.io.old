---
layout: post
title: I-failed-to-parasitize-an-established-clinical-researcher
heading: "The one time I failed to parasitize an established clinical researcher"
date: 2016-01-24
categories: 
    - science
---
As regular readers of this blog probably know, I'm the paragon of a [research parasite.](https://twitter.com/hashtag/researchparasite) I'm a computational biologist, and all I ever do is publish my own analyses of other people's data. Except that one time, a few years back, when a senior clinical researcher stopped me in my tracks. Thanks to his careful and guarded stewardship of his data, I have been saved from drawing incorrect conclusions from his data and from publicly embarrassing myself by claiming his analysis is complete nonsense.

<!--more-->

The story happened a few years back, when a senior clinical researcher (let's call him X) published a paper claiming that egg-yolk consumption is nearly as bad for cardiovascular disease (CVD) as is smoking. As an avid egg lover, I wondered whether I should be concerned. Unfortunately, the manuscript was opaque and used statistical techniques I don’t trust ([quantiling](/blog/2013/8/18/common-errors-in-statistical-analyses)), so I contacted X and asked to see the raw data. He made me state that I did not have any ties, financial or otherwise, to the egg industry (I don’t), and then he shared his raw data with me under the condition that I would keep the data confidential and that he would be a co-author on any resulting publications. I accepted these conditions and took a look at the data.

I quickly realized that X and his colleagues had made several statistical mistakes, and that in fact the data exonerated eggs as a culprit for CVD. I analyzed the data using a variety of different approaches, just to be sure, but the simplest and most obvious one was a principal components analysis (PCA). It showed clearly that the egg-consumption axis was orthogonal to the age/smoking/CVD axis. (To this day, it's one of the cleanest examples I've ever seen of a PCA revealing distinct underlying trends in the data.)

I wrote a brief report and shared it with X, who forwarded it to a colleague of his in the biostatistics department. Let’s call him Y. The response I received was quite astonishing. (I’m paraphrasing from memory here.) First, Y said that “Claus Wilke is a strong student.” I was a tenured professor at the time. Second, Y said that “we don’t use PCA in clinical research.” Never mind that simple correlation tests, ordinary regressions, and regularized regressions all supported the results I had found with the PCA.

Now, since X and Y thought I was a good student who however didn’t understand how statistics work in the clinical practice, and since I thought X’s paper was a bunch of nonsense, writing a joint paper on this topic was out of the question. That’s alright by me. I don’t need to publish in nutrition, and I’m fine with not having to worry about being assassinated by the egg-substitutes industry. However, X’s paper is still out there, receiving almost 20 citations a year. And, more importantly, this paper and its associated data would serve as an ideal teaching tool for the dangers (and power) of multivariate statistics. Alas, I’ll have to let it go. I should probably just start collecting my own data set of carotid plaque thickness in patients that have or have not eaten eggs for many years.

**Note:** If you’re wondering what all of this is about, read [this editorial](http://www.nejm.org/doi/full/10.1056/NEJMe1516564) in the New England Journal of Medicine. You may also want to read [this translation into English.](http://jonathanpeelle.net/blog/2016/1/22/translation-to-plain-english-of-selected-portions-of-longo-and-drazens-editorial-on-data-sharing)
