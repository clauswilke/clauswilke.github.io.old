---
layout: post
title: post-publication-review-of-the-plos-one-paper-comparing-ms-word-and-latex-how-not-to-compare-document-preparation
heading: "Post-publication review of the PLOS ONE paper comparing MS Word and LaTeX: How not to compare document preparation"
date:   2014-12-27
categories: writing
Tags:
    - latex
    - MS Word
    - post-publication review 
    - markdown
---
PLOS ONE just published a paper comparing MS Word with LaTeX, which argues that LaTeX has little benefits over MS Word and should not be allowed by scientific journals:

> Knauff M, Nejasmic J (2014) [An Efficiency Comparison of Document Preparation Systems Used in Academic Research and Development.](http://www.plosone.org/article/info:doi/10.1371/journal.pone.0115069) PLoS ONE 9(12): e115069.

In my mind, this paper makes extremely strong claims based on a rather flawed and thin analysis. I am sure there are useful things to be said about MS Word vs. LaTeX. However, this paper does not make much of a contribution to this question. 

<!--more-->

To give you some background: I have been using LaTeX for over 20 years, I have written tens of thousands of pages with LaTeX, and I am extremely familiar with its pros and cons. I am also using MS Word on a regular basis, and I regularly make the choice between using LaTeX or MS Word, on a document-by-document case. There are documents I’d rather write in LaTeX, and there are other documents I’d rather write in MS Word. There are also documents (increasingly many, in fact) for which I prefer entirely different approaches, such as Markdown. With that said, let me list the main objections I have to the Knauff and Nejasmic paper.

## Apples and oranges
The entire premise of the paper is flawed: MS Word is a text editor, LaTeX is a file format. Those two things are inherently not comparable. There is no technical reason why MS Word cannot save documents to LaTeX, only the creators of MS Word chose not to implement this option. A simple work-around exists, however: Save the document as .docx and convert it to LaTeX with [pandoc](http://johnmacfarlane.net/pandoc/). Incidentally, you can also go the other way round, write the document in LaTeX and convert to .docx. Fundamentally, file formats describing the same kind of data can be converted into each other. Therefore, people should be allowed to use the software and file formats they prefer (within reason, and preferably non-proprietary ones). Computers can sort out the differences.


## A rigged comparison
The comparison the authors set up, the reproduction of three relatively simple, one-page documents, is entirely artificial and rigged to favor MS Word. This is particularly the case (and this is not really explained well in the paper) if the LaTeX users were tasked to reproduce the visual layout of the documents. LaTeX is meant to separate contents from layout, and the people who use it regularly tend to value that separation. However, this separation implies that it can sometimes be a bit difficult to achieve a particular physical layout. The correct, LaTeX way to solve this problem would be to prepare an appropriate style file. Yet I doubt the users in this test were given such a style file for the *continuous text* example (which poses some tricky formatting issues with the title, author list, and address line).

For anybody who has experience with both systems, it would be trivial to set up examples where MS Word utterly fails and LaTeX shines:

- Set up 50 numbered equations, refer to them throughout the text, then change the equation order.

- Have figures and their captions float to appropriate locations at the top or bottom of pages.

- Change the order of figures in a document and fix all references to those figures.

## It’s not surprising that LaTeX users are highly satisfied 

Throughout the paper, the authors state (somewhat surprised, it seems to me) that LaTeX users are highly satisfied with their document preparation software. The authors seem to have no explanation for this observation, other than cognitive dissonance. In effect, the authors are saying that LaTeX is so awful that the only way to use it regularly is to convince yourself it is great even though it is not.

There’s a simple alternative explanation, though: Even though LaTeX can be cumbersome and has its quirks, LaTeX is highly predictable. Once you have figured out how something works, it always works that way. LaTeX never crashes. Documents don’t suddenly change layout or font. Tables don’t jump around. By contrast, none of this can be said about MS Word. Everybody who uses MS Word knows that it sometimes does things that simply can’t be explained. Things that should work don’t. Formatting changes randomly.

In my own experience, to produce a final document, I fiddle around about as much with MS Word as I do with LaTeX, only that the issues with LaTeX are usually the same three predictable things (proper formatting of the cover page, some table issues, getting all the references into BibTeX). By contrast, with MS Word I always fight against some random, unexplainable stuff.

## State of the art in document preparation

What I find most amazing about the Knauff and Nejasmic paper, considering that it is a study on document preparation, is that the authors seem to be completely out of touch with the state-of-the-art developments in that field. The authors barely even mention the important distinction between document structure and document layout, and they don’t discuss at all why one might want to separate the two. They also don’t consider automatic document conversions for different media (e.g. web versus print). Finally, they don’t discuss the increasingly important issue, at least for scientific documents, of integrating the text of a paper with the code used for data analysis and figure generation.

In fact, there is plenty of room for improvement over LaTeX when it comes to document preparation. Most heavy LaTeX users would agree that the language can be cumbersome, and I haven’t met anybody who wouldn’t rather not type out all the LaTeX commands required to prepare a finished document. Extensive efforts are currently underway to address these and other issues, but these efforts are not happening in the world of MS Word.

The most exciting current developments, in my mind, are happening with [Markdown.](http://en.wikipedia.org/wiki/Markdown) Markdown is an extremely simplified markup language that can be learned in half an hour or less. Markdown documents can be read easily in their source form (unlike LaTeX documents), and they can also be converted into HTML or PDF documents. (The PDF conversion usually goes via LaTeX as intermediate.) Moreover, through extensions such as [R Markdown,](http://rmarkdown.rstudio.com/) one can easily combine the document text, the code for data analysis and figure preparation, and the final figures, all in a single file. The result is a publication-quality document that is easy to produce, self contained, and allows for complete reproducibility of the analysis and figure generation. I bet that if the comparison in the PLOS ONE paper had been MS Word vs. LaTeX vs. Markdown, Markdown would have won hands down.

## Does any of this matter?

Why quibble over file formats and editors at all? As I said in the beginning, I use various tools, depending on the task at hand. As long as we can all agree that there are different use cases and that people can make informed decisions on which tool to use when, I’m fine. However, this is where the authors of the PLOS ONE paper go off the deep end. After presenting their relatively thin, somewhat rigged, and definitely not comprehensive comparison of one text editor to one file format, they then make incredibly strong claims, including that LaTeX users may be suffering from cognitive dissonance and that vast amounts of money could be saved if people were forced to switch over from LaTeX to MS Word. These statements are simply not warranted, they do not follow logically from the analysis presented, and they entirely disregard that the future of scientific document preparation may lay elsewhere (e.g., Markdown). If there is one thing this paper doesn’t make is a strong argument *in favor* of MS Word, and we must be careful not to allow journal editors or other policy makers to use arguments such as the ones made in this paper to force us into a single mode of document preparation.
