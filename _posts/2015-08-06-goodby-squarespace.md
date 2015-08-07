---
layout: post
title:  goodby-squarespace
heading: "Goodby Squarespace, Hello Github"
date:   2015-08-06
categories: misc
---

After having hosted my blog on Squarespace for about two years, I have decided to move it over to Github pages. Squarespace was a reasonable and easy solution for me two years ago when I knew nothing about web hosting and web design, but I’ve increasingly grown frustrated and feel that I’m constantly having to fight with Squarespace to get it to do what I want it to do. I originally chose Squarespace because I didn’t want to maintain my own article database and I didn’t like the design and feature set of most popular blogging platforms such as WordPress or Blogger. In the mean time, I have learned about static page generators, and I now think that they are superior to most other options for basic blogs and other simple web pages. So I’ve redesigned my site using [Jekyll](http://jekyllrb.com/) for page generation, [Bootstrap](http://getbootstrap.com/) as CSS and JS framework, [Google fonts](https://www.google.com/fonts) and [Font Awesome](http://fontawesome.io/) for typograpy and icons, and [Disqus](https://disqus.com/) for comments.

<!--more-->

As of this writing, the Squarespace site is still visible at [http://clauswilke.com](http://clauswilke.com), but I’ll probably take it offline soon. In porting my site over, I have made sure that the direct links to posts remain the same, so that any bookmarks or direct links to posts should continue to work as before. The only difference may be the RSS feed, so if you’re subscribing through an RSS reader you may have to resubscribe to the new page. I have also ported all the comments, so the comments that were made on the Squarespace site are still visible on the new site.

So what were the things that bugged me about Squarespace? Most importantly, it felt like a huge black box, and I was worried that at some point all the work I was putting into my blog might just go up in flames if I wasn’t moving my data out in time. More specifically, here are six concrete issues I had:

1. All the site data are in a big, proprietary database. While Squarespace has an export function, that function exports only text. Any images or other files uploaded to Squarespace cannot  easily be exported.

2. Related to the previous point, there is no way to manage all the media files that one uploads to Squarespace. They live in some mysterious data store that Squarespace customers are not given access to. As a corollary of this set up, if one wants to use the same image in multiple posts one has to upload the image multiple times.

3. While Squarespace posts can in principle be written in Markdown, Squarespace’s Markdown capabilities are limited and buggy. In particular:
  - Code blocks are buggy. Specifically, Squarespace doesn’t properly escape special characters in code blocks. This can make embedding code into Markdown posts a big headache.
  - Images cannot be inserted directly from the Markdown.
  - To insert images, one has to break the Markdown into two parts and insert an image block in between. As one does so, Squarespace rewrites the Markdown and turns all inline links into reference-style links. While this doesn’t alter the page output in any way, I prefer to use software that doesn’t randomly rewrite my source code.
 - The online Markdown editor Squarespace provides is slow and buggy. For longer pieces of text, the cursor is often displayed at the wrong location, so that it becomes difficult to edit the text at all.

4. It is not possible to extract excerpts of articles automatically. They need to be manually retyped. And excerpts cannot be entered in Markdown. And the formatting options for excerpts are limited. Excerpts simply don’t work very well in Squarespace at all.

5. The Squarespace user interface seems slow and cumbersome to me. Anything I want to do requires a lot of clicks.

6. Modifying the page design with Squarespace can be difficult. Certain superficial changes, such as colors or spacings, are generally easy. But other changes are difficult or even impossible. I frequently wanted to modify aspects of the design that I couldn’t. In theory, one can always inject custom CSS and modify the page that way. However, in practice it is often not clear how exactly the CSS would have to look, and which classes would need to be modified.

It took me about a day to set up the new web page on Github, and another two days to port all the posts over and fine-tune the page design. Since I had already written all my Squarespace posts in Markdown, copying them over to the new site was relatively straightforward. However, I took the opportunity to clean up some issues in most posts, so every post required 5-10 minutes of manual editing until it was properly ported.

Porting comments was a little more difficult, but by following [this guide](http://www.kenyagjohnson.com/techbytes/2013/5/19/import-squarespace-comments-into-disqus) I more or less made it work. It’s not perfect, and in particular the formatting is sometimes mangled, but at least the text is there. In general, I’m not too excited about having to use Disqus, since their business model relies on tracking users and selling ads, but the reality is that currently there is no viable competitor offering a comparable service, even for a fee. I have switched on guest posting in Disqus, so you can post comments here without having to sign up for a Disqus account.

I am still fiddling with the page design on the new blog. I feel the current design is Ok but not great. However, now that everything is collected in simple Markdown files, I feel I’m operating from a much more robust base and can work on the page design as I go forward. Also, the entire blog source is now openly available at [https://github.com/clauswilke/clauswilke.github.io.](https://github.com/clauswilke/clauswilke.github.io) Feel free to check it out or use as the base for your own page. Also feel free to share or re-host any of my posts. All code (CSS, HTML, JS) is licensed under the MIT license, and all posts are licensed (individually) under the [CC BY-ND license.](https://creativecommons.org/licenses/by-nd/4.0/)
