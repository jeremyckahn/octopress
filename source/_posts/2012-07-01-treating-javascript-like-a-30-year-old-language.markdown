---
layout: post
title: "Treating JavaScript like a 30 year old language"
date: 2012-07-01 15:51
comments: true
categories: 
---

I don't like JavaScript.  I write an enormous amount of JavaScript — in fact I write it almost exclusively — but I don't really like it as a language.  I don't want to write a giant screed as to why I don't like the language, but suffice it to say that it lacks some really basic features (like default parameters), and its lack of clearly defined rules (semicolons, whitespace) create lots of headaches.

Something that has helped me keep JavaScript manageable and even fun is the coding styles I have developed.  I create a lot of rules for myself that result in extremely readable and descriptive code.  This equates to lots of boring style constructs and boilerplate comments that add absolutely no features to what I'm writing, but go a long way to keep the code obvious and explicit.  I write JavaScript as though it were C, at least to some extent.  Why do I create this extra work for myself?  Because reading code sucks.  It will always suck, whether you are reading your own code or somebody else's.  Especially when it comes to my [open source projects](https://github.com/jeremyckahn), I really, really want people to read and contribute to the code I write.  It is absolutely worth it to take extra time to trivially polish code so that fellow humans can easily dive right in.  Additionally, I read my code far more often than I write it, so I want to have mercy on my future self by writing painfully obvious and straightforward code.

Much of my style is rooted in the [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml).  This is largely due to the fact that I need to follow this style guide in my day job.  However, I fallen in love with the strictness of the Google Way, and have adapted it for my own open source projects.  For said open source projects, I don't follow Google 100% because, well, I have my own opinions on clean code.  It's pointless to go over every minutiae of my style preferences, but I think there a few basic rules that go a long way in keeping large amounts of code sane and manageable.

