---
layout: post
title: "Screenshot absolutely everything"
date: 2012-12-01 13:08
comments: true
categories:
---

One of the best things about being a programmer is using powerful tools to solve problems in simple ways.  One of the worst things about being a programmer is the ambiguity of feature requests and bug descriptions.  Luckily, we have simple tools to solve this problem!  The adage "show, don't tell" is one that is as true today as it ever was, and developers can avoid hours of frustration and wasted time by taking and requesting screenshots.

## Confirming the problem

Consider this bug request:

```
  1. Go to http://rekapi.com/ease.html
  2. Look at field for "Custom easing 1."
  3. Notice the right side of the input, it looks incorrect.
```

This is actually an exemplary bug description, but it still leaves a little bit open to interpretation.  Specifically, "looks incorrect" could mean anything.  This is a contrived example of a bug description, but you've no doubt seen bugs filed against you that read like this.  Rather than having to read those steps and reproduce the issue, how about just looking at this:

{% img /images/bug_image_example.png %}

This is much nicer!  Showing an image like this does a number of things for you:

  * It saves on time taken to reproduce an issue.
  * It helps you and your fellow humans make associations between images and issues, which our brains are particularly good at.
  * It captures what was actually shown, rather than an individual's perception.  Individual perception is less useful when dealing with UI issues, especially.
  * Since bugs are typically tracked indefinitely, an image gives you something concrete to refer to long after the issue was fixed and forgotten about.
  * It clearly demonstrates the bug regardless if it can be reliably reproduced, which is often not the case.

Screenshots are the _best_ tool for showing an issue and keeping the entire team on the same page.

## Confirming the solution

Just as bug descriptions are open to interpretation, so are their resolutions.  What is "fixed" to a developer is "off by a pixel" to a designer.  Before fixing a bug, committing the code and moving on, send a screenshot over to whomever needs to confirm the fix and save yourself the runaround of having to fix your fix.

This goes beyond simple UI bugs.  I recently filed [a Pull Request on Github](https://github.com/jquery/web-base-template/pull/137) which amounted to a very simple two-line change (I updated the version of jQuery).  However, being an open source project with huge visibility, I wanted to make very clear to others that my fix worked.  So, I attached [a screenshot](https://www.dropbox.com/s/85zo9e1mdkfnzuc/Screen%20Shot%202012-12-01%20at%2012.28.42%20PM.PNG?m), simply showing that the version was indeed updated on the site correctly.  Now the other developers don't have to sanity check my fix and can merge the Pull Request worry-free.  Proving your solutions with screenshots makes life better for everyone on your team.

## Taking screenshots is _easy_

Taking and sharing screenshots used to be difficult and slow.  Luckily, we now have a myriad of tools to optimize this.  I have [my own roundabout way](http://www.youtube.com/watch?v=xzNQZVMLnIw) of taking and sharing screenshots, but there are countless options out there.  Taking screenshots in Mac OS X is particularly easy, as there are screenshot-taking utilities built right into the OS (either use the "Grab" application or take a look at `Preferences > Keyboard > Keyboard Shortcuts > Screen Shots`).  Sharing is also easier than ever.  You can use Dropbox, Droplr, CloudApp, or any one of the many hosting services available to you.  Many of them are free.

## Absolutely everything

Screenshots help more than just software developers.  They are useful for debugging your family's IT woes.  They are useful for sharing text that can't be selected for copy/paste.  They are useful for showing progress on a design.  A picture is worth a thousand words, so save yourself some keystrokes and take screenshots instead!
