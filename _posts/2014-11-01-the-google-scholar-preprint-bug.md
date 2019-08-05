---
layout: post
title: the-google-scholar-preprint-bug
heading: "The Google Scholar preprint bug"
date: 2014-11-01
categories: science
tags:
    - google
    - google scholar
    - preprints
    - scientific communication
    - bug
---
Google Scholar has a serious bug when it comes to preprints. If you have published a preprint of your paper, the later journal publication can be completely invisible to Google Scholar, seemingly absent from their entire database. Even a search for the exact article title will not find the article. And this condition remains for months. (It will eventually fix itself, though. After about a year.) I have now seen this bug in action for several of my papers, and I am confident it’s a reproducible flaw and not a one-off. I reported the issue to the Google Scholar team about a year ago (or at least, I filled in some web form that seemed to be designed to send them feedback) but I have received no response and the bug clearly still exists. I hope that with this blog-post I can draw some attention to this serious issue, so we can have it fixed. Thousands of scientists rely on Google Scholar every day. For many recent articles, this bug will steer these scientists towards outdated, early versions and make the authoritative article versions completely inaccessible.

<!--more-->

As far as I can tell, what triggers the bug for sure is the publication of an updated version of the same article with a changed title or author list. It is possible that the same bug occurs even when title or author list hasn’t changed, but I haven’t noticed it under those conditions. Here is an example of this bug in action. My lab published the following article on BioRxiv on April 24, 2014:

> Amir Shahmoradi, Dariya K. Sydykova, Stephanie J. Spielman, Eleisha L. Jackson, Eric T. Dawson, Austin G.Meyer, Claus O. Wilke. Predicting evolutionary site variability from structure in viral proteins: buriedness, flexibility, and design. [doi: https://doi.org/10.1101/004481](http://biorxiv.org/content/early/2014/04/24/004481)

If you click on the link, you’ll see that BioRxiv encourages you to check out the latest version of the article, with slightly different title, posted on July 21, 2014:

> Amir Shahmoradi, Dariya K. Sydykova, Stephanie J. Spielman, Eleisha L. Jackson, Eric T. Dawson, Austin G.Meyer, Claus O. Wilke. Predicting evolutionary site variability from structure in viral proteins: buriedness, packing, flexibility, and design. [doi: https://doi.org/10.1101/004481](http://biorxiv.org/content/early/2014/07/21/004481)

The doi is the same, so clearly those are two subsequent versions of the same article. BioRxiv also knows that the article was published in its final form by the Journal of Molecular Evolution under [doi: 10.1007/s00239-014-9644-x](http://link.springer.com/article/10.1007/s00239-014-9644-x) on September 13, 2014. Finally, the article has a PubMed entry ([PMID: 25217382](http://www.ncbi.nlm.nih.gov/pubmed/25217382)) and if you do a normal Google search using the complete, final article title the [top three hits](https://www.google.com/search?q=Predicting+evolutionary+site+variability+from+structure+in+viral+proteins%3A+buriedness%2C+packing%2C+flexibility%2C+and+design&oq=Predicting+evolutionary+site+variability+from+structure+in+viral+proteins%3A+buriedness%2C+packing%2C+flexibility%2C+and+design&aqs=chrome..69i57j69i59j69i60l3.549j0j1&sourceid=chrome&es_sm=91&ie=UTF-8) are two different preprint postings and the final journal article.

Now that we have established that the article clearly exists, has been published in its final form for over three months (since July 21, 2014), and is known to regular Google, let’s try to find it on Google Scholar. First, we search for the exact title. Here is the result:

{% include image.html url="/assets/images/posts/2014-11-01-Google_Scholar_screen_shot.png" %}

Yes, Google Scholar suggests to me that I misspelled the title and meant to type “busineses” instead of “buriedness.” Importantly, it doesn’t find the correct, latest article! It does find the preprint, though, as the second hit. If I click on “all 8 versions” for the preprint, I get all sorts of different versions of the preprint, but the [final, published article is not found](http://scholar.google.com/scholar?cluster=1799163645855055780) as of this writing (Nov. 1, 2014). The latest version also doesn’t show up among my 2014 publications in my [Google Scholar profile,]( http://scholar.google.com/citations?hl=en&user=Nc8U6E4AAAAJ&view_op=list_works&sortby=pubdate) only the first preprint version is shown. For all intents and purposes, the July 21 and September 13 versions of the article are completely missing from the Scholar database. I cannot retrieve them in any way through Scholar. Let me say this one more time: We’re not simply talking about Google Scholar  creating multiple redundant entries and not noticing that two articles are just different versions of the same article. **We’re talking about an earlier article completely hiding all later versions.** Note that, as I said at the beginning of the post, this issue will correct itself eventually. The paper for which I first noticed this is now, after a year, correctly indexed in Google Scholar.

To demonstrate that this is not a one-off, consider [this article,](http://biorxiv.org/content/early/2014/10/14/002287) posted in revised version on October 14. I’ll leave it as an exercise to the reader to verify that this article exists, is known to regular Google, and is completely invisible in Google Scholar.

In my mind, this is a serious bug that severely interferes with efficient scientific communication. It also is a huge embarrassment for a company that prides itself of being the world’s leading expert in information retrieval. I hope this post will give this bug more visibility, and will eventually lead the Scholar Team to fix the problem.

**Update:** In case you're wondering if this is just an issue of Google Scholar not having indexed the latest issues of J. Mol. Evol. and/or BiorRxiv yet, that is clearly not the case. Other articles from the [same J. Mol. Evol. issue](http://link.springer.com/journal/239/79/3/page/1) can be found by a search for their title, e.g. [this one](http://scholar.google.com/scholar?hl=en&q=Limits+of+Neutral+Drift%3A+Lessons+From+the+In+Vitro+Evolution+of+Two+Ribozymes) or [this one](http://scholar.google.com/scholar?hl=en&q=One+origin+for+metallo-%CE%B2-lactamase+activity%2C+or+two%3F+An+investigation+assessing+a+diverse+set+of+reconstructed+ancestral+sequences+based+on+a+sample+of+phylogenetic+trees) or [this one](http://scholar.google.com/scholar?q=Essential+is+Not+Irreplaceable%3A+Fitness+Dynamics+of+Experimental+E.+coli+RNase+P+RNA+Heterologous+Replacement).

