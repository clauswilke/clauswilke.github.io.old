---
layout: post
title: perfectly-smooth-transition-between-fixed-and-variable-positioning-of-html-elements-using-css-and-javascript
heading: "Perfectly smooth transition between fixed and variable positioning of HTML elements using CSS and Javascript"
date:   2014-12-23
categories:
    - web design
Tags:
    - CSS
    - Javascript
    - HTML
    - web design
---
The last couple of days I have been working on a new [webpage.](http://wilkelab.org) In doing so, I wanted to create a design where the menu bar initially resides at the bottom of the page and moves upwards as the user scrolls down. However, once the menu bar hits the top edge of the viewport, it should remain fixed there. A bit of googling quickly revealed a solution for this problem, using a combination of CSS and Javascript. However, I wasn’t happy with the solution, because it created a visible jump in the layout every time the menu bar hit the top edge of the screen. In fact, this jump is quite common among most web pages that use this design trick. For example, check out a [profile page on Google Scholar:](http://scholar.google.com/citations?user=Nc8U6E4AAAAJ&hl=en) As you scroll down, the heading above the publication list stays fixed as soon as it hits the top edge of the screen. And if you scroll slowly, you’ll see that the layout jumps the moment the element hits the top edge. I didn’t like this effect at all, so I devised a way to work around it.

<!--more-->

Let’s first discuss how we implement this kind of effect in general. They key idea is to use a little bit of Javascript to monitor where on the screen the element of interest resides. The moment it hits the top edge of the viewport, we set it’s `position` property to `fixed` so it can’t move any further. If we scroll back down, we revert the setting so the element can move downwards again.

The following code will generate this effect:   
HTML:

{% highlight html %}
<div id="content-anchor"></div>
<div id="sticky">This turns sticky</div>
{% endhighlight %}

(The `content-anchor` id is needed so the Javascript code can monitor where the sticky element should be on the page relative to the rest of the document. See the code below.) 

CSS:

{% highlight css %}
#sticky {
}

#sticky.stick {
    position: fixed;
    top: 0;
    width: 100%;
}
{% endhighlight %}

Javascript (using the jQuery framework):

{% highlight js %}
function sticky_relocate() {  
    var window_top = $(window).scrollTop();  
    var div_top = $('#content-anchor').offset().top;  
    if (window_top > div_top) {  
        $('#sticky').addClass('stick');  
    } else {  
        $('#sticky').removeClass('stick');  
    }  
}  

$(function () {  
    $(window).scroll(sticky_relocate);  
    sticky_relocate();  
});
{% endhighlight %}

You can check out a working example of this idea [here.](http://jsfiddle.net/0zxxrjqj/) What you will notice, if you scroll slowly, is that just as the sticky element hits the top edge of the viewport, the bottom element (“Main document”) jumps upwards. In fact, at the moment at which the sticky property is turned on, the sticky element covers most of the heading of the main document. This is exactly the same effect that you can see on the Google Scholar page and on countless other pages around the web.

What is going on here? What is happening is that as the sticky property is turned on, the sticky box is removed from the layout and displayed on top of the rest of the document. Hence, the height of that box is now missing from the layout, causing the visible jump. The solution is simple, of course: As we take out an element from the layout, we need to insert an alternative one of exactly the same size. The simple solution is to add a copy of the sticky element that we can show or hide as needed. The corresponding code looks as follows:

HTML:

{% highlight html %}
<div id="content-anchor"></div>
<div id="sticky-phantom">This turns sticky</div>
<div id="sticky">This turns sticky</div>
{% endhighlight %}

CSS:

{% highlight css %}
#sticky {
}

#sticky-phantom {
    visibility: hidden;
}

#sticky.stick {
    position: fixed;
    top: 0;
    width: 100%;
}
{% endhighlight %}


Javascript:

{% highlight js %}
function sticky_relocate() {
    var window_top = $(window).scrollTop();
    var div_top = $('#content-anchor').offset().top;
    if (window_top > div_top) {
        $('#sticky').addClass('stick');
        $('#sticky-phantom').show();
    } else {
        $('#sticky').removeClass('stick');
        $('#sticky-phantom').hide();
    }
}

$(function () {
    $(window).scroll(sticky_relocate);
    sticky_relocate();
});
{% endhighlight %}

I have provided a working implementation of this idea [here.](http://jsfiddle.net/ju9ay0y7/) As you can see, in this example the layout doesn’t jump at all. The scrolling is smooth the whole time.

This is such a simple trick that I’m surprised it is not used more often. Maybe now that I have posted it here, more people will use it, and we’ll see fewer jarring layout jumps.
