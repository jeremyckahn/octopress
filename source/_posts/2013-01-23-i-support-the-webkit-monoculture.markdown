---
layout: post
title: "I Support the WebKit Monoculture"
date: 2013-01-23 20:11
comments: true
categories: 
---

_Full disclosure: I work for YouTube, which is owned by Google._

_Disclaimer: This post, as well as all posts on this blog, reflect my opinions and not those of my employer._

Counter to the opinion of the [Web Development literati](http://www.zeldman.com/2012/02/14/a-list-apart-no-344-the-new-webkit-monoculture/), I support a WebKit monoculture.  I'll put this in no uncertain terms:  I think the web would be better off if WebKit was the only rendering engine.  The common arguments against this are that it's bad for competition and that ["it's IE6 all over again"](http://news.cnet.com/8301-30685_3-57373764-264/w3c-co-chair-apple-google-power-causing-open-web-crisis/).  I feel that the former argument is invalid, and the latter is a false dichotomy.

## WebKit is open source

One of the core evils behind Internet Explorer is that it is a closed platform.  The Web is a fundamentally open platform, and anything "closed" flies in the face of what the Internet stands for.  IE attempted to follow in Microsoft's [Embrace, extend, and extinguish](http://en.wikipedia.org/wiki/Embrace,_extend_and_extinguish) strategy, and _that_ is bad for the web.

WebKit is open.  The source code is [freely available](https://trac.webkit.org/browser) to all, and anyone with a good idea is able to contribute.  WebKit has no single owner or controller.  In addition to being completely open, it also has strong corporate leadership and support (Apple and Google, among others).  WebKit is developed by individuals that want the Web to win, not a single corporation.  WebKit is no worse for the Web than Linux is for operating systems.

## Rapid release cycle

IE did [a lot of good](http://www.nczonline.net/blog/2012/08/22/the-innovations-of-internet-explorer/) for the Web in the short term, but it left deep scars.  It achieved almost complete vendor lock-in that lingers today; many users are stuck in the past because of how difficult it is to upgrade.  The WebKit developers recognize this problem and have solved it with easy and frequent updates.  In the case of Chrome, it is a fully automatic process.  Because WebKit has such strong corporate support, it has faster iterations than any competing project, which leads to more features and bug fixes. 

## It's not a platform

To say that a WebKit monoculture is "IE6 all over again" doesn't really make sense, because WebKit and IE aren't comparable projects.  IE6 tried to be a platform - the thing that apps are built upon - with ActiveX.  WebKit is a _rendering engine_, a single component of many that make up a web browser.  WebKit can be implemented into any project that wants to use it.

I don't love the idea of Web apps that run in only one browser, but I don't see an issue with apps that support one rendering engine.  Focusing on the capabilities of a single rendering engine frees developers up to build great features and not worry about appealing to the lowest common denominator.  This freedom is what pushes the Web forward.  In a perfect world, you would only only have to write and debug code once.  We would be much closer to that reality if all browsers used WebKit for rendering.

## It's more developer-friendly

WebKit has a lot to offer Web Developers.  Safari's built-in developer tools are great, and Chrome's Developer Tools are simply the best I've ever used.  These development tools are somewhat orthogonal to WebKit itself - you just usually find them paired with one another.  The real beauty of Webkit from a tooling perspective is that it is so flexible.  Again, WebKit is a component of a web browser, not a browser in and of itself.  [PhantomJS](http://phantomjs.org/) is a headless browser that is powered by WebKit.  It is fully scriptable and can be used for running automated tests - another thing that substantively pushes the Web forward.

Just as focusing on a single rendering engine allows us to spend more time writing cutting edge features for our apps, it also allows us to build more robust tools.  Software fragmentation is bad, and it's one of the biggest things holding the Web back right now.

## More wood behind fewer arrows

WebKit is not the only open source rendering engine.  The big competitor is [Gecko](https://developer.mozilla.org/en-US/docs/Mozilla/Gecko), Mozilla's rendering engine that is used in Firefox.  Gecko was instrumental in wresting the Web from Microsoft's grasp, but it is past its prime.  Now Gecko is old, buggy and slow - at least in comparison to WebKit.  Imagine if all of the Gecko developers left and joined forces with WebKit?  Both projects are (imperfectly) trying to adhere to W3C standards, so fragmentation due to inconsistencies would diminish significantly.  Imagine if Firefox switched to WebKit - it would free up a ton of time spent fixing Firefox bugs.  Don't get me wrong, a world without browser-specific bugs is a pipe dream.  But standardizing on a single _rendering engine_ would go a long way towards unifying the web.

Competition is good and necessary, but not for all things.  I would love to see browser vendors focus on competing on features to benefit the user, not their own interpretation of the W3C standards.