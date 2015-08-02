---
layout: post
title: is-consumer-software-creating-a-new-generation-of-computer-illiterates
heading: "Is consumer software creating a new generation of computer illiterates?"
date: 2013-08-30
categories: 
    - misc
tags:
    - computing
    - programming
    - software
    - office365
    - computer illiteracy
---
When I was growing up, computers were a still a pretty unusual thing. As a result, people could generally be subdivided into two types: those that knew their way around computers and those that didn’t. The ones that knew their way around computers really knew things, often down to the hardware level. (I had a book listing the entire operating system of my Commodore, in machine language.) The others pretty much knew nothing, *and they knew that they knew nothing.* So the world was in order. Everybody knew their place. These days, computers are ubiquitous. Everybody and their dog knows how to fill out a web form or install an app. Yet unless we venture beyond the shiny interfaces provided by the Microsofts, Apples, and Googles of this world we remain just as illiterate as the earlier generation. We just don’t know how much we don't know.

<!--more-->

What prompted me to write this post? At my university, I have the pleasure of using email service provided through Microsoft’s new Office365. And yesterday, I made the mistake of trying their email filtering solution. My goal was a simple one: Set up an email filter that takes all replies (but not original posts!) to a certain mailing list and moves those messages into a special folder. You should know that all messages to the list are tagged with a unique identifier, something like “[list-X]”, so it’s easy enough to find those messages. But how do we know a message is a reply, not an original post? Well, for original posts, “[list-X]” appears at the beginning of the subject line. For replies, the subject line usually begins with “Re: [list-X]” or “RE: [list-X]” or maybe even “Aw: [list-X]” (the latter happens if somebody is using an email program in the German language). So original posts and replies are easy enough to tell apart. All we have to do is create a filter rule that captures all posts whose subject contains, *but doesn’t begin with,* the tag “[list-X]”. How hard could that be?

Well, in Office365, this is a problem of infinite difficulty. It cannot be done. You can filter by sender, you can filter by receiver, you can filter by keywords in the subject line, but you cannot filter for specific sequences of words, and you cannot filter for words that do appear in the subject line but not at the beginning. Now, if you’re a modern-day computer illiterate, you may think: “Well, of course Microsoft programmers couldn’t include a separate option for any random combination of conditions somebody could come up with. They have to make reasonable selection among common cases, and there’s just no way around that.” If this is your thinking, then what you do not know is that computer scientists have long had a simple solution to this problem, a solution called “regular expression.” (If you’ve never heard of [regular expressions](http://en.wikipedia.org/wiki/Regular_expression), look them up. They are super powerful. They are the computing equivalent of a swiss army knife, a chain saw, and a pickup truck all in one.) All Microsoft would have to do is add one more option, “filter by regular expression,” and I could create the most spectacular filtering rules. And this option is trivial to implement. It would take a skilled programmer about an afternoon to add. Likely, the underlying filtering software in Office365 already employs regular expressions, so all that Microsoft programmers would have to do is allow me to access that software layer directly. But they don’t, and so I can’t.

Now, why don’t they add an option that would be tremendously useful and trivial to add? There are two possible interpretation. It’s either because they don’t want to scare us (benign interpretation) or because they don’t want us to be in control of our computers (malicious interpretation). Whatever the reason, the outcome is the same. If all you know is the polished user interface of consumer software, you’ll know computers as magical contraptions that can do incredible things, as long as somebody has thought of the things you might want to do. If you want to do something different, though, something unconventional, then that’s usually not possible, as far as you know. I suspect that if you have grown up in this environment, you don’t even know what it is you can’t do. You have no good mental model of the underlying technology, so you don’t know what should be easy and what might be difficult. Dumbed-down consumer software keeps you ignorant of the true power of computing technology.

A conspiracy theorist might pose that this is done on purpose. If you don’t really understand how computers work and what they are capable of, you don’t realize how easy it would be to, for example, take the metadata [[1]](#note1) of your phone and text messages and figure out with whom you’re likely having an affair. I don’t really believe in massive conspiracies, though, so I think the more likely explanation is that in the effort of making software simple and accessible to all, it’s often easier and less work to simply hide the true underlying capabilities. Either way, the end result is the same. Plenty of people who think they know how to use computers but really they don’t.

As to Office365, I’ll file a bug report. Fat chance they’ll act on it.

## Notes

[1]<a id="note1"></a> Metadata in this case means call and text records, but without their content. Basically a list of who did you call when, who called you, who did you text, and who texted you.
