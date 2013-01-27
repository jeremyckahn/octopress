---
layout: post
title: "In Response to Oscar Godson"
date: 2013-01-26 15:29
comments: true
categories: 
---

[My WebKit monoculture post](/blog/2013/01/23/i-support-the-webkit-monoculture/) garnered quite a reaction in the community.  I figured my opinion would not be particularly popular on this subject, but I stand by what I said.  If nothing else it sparked a few really [interesting conversations](http://news.ycombinator.com/item?id=5108312).  Oscar Godson wrote a well-reasoned [response blog post](http://oscargodson.com/posts/in-response-to-jeremy-kahn-and-webkit-monoculture.html) with some strong counterpoints, which I'd like to address.

> Just because something is open source doesn't mean the downstream browser vendors implement it the same or don't add to it. If it were true that WebKit was used the exact same away across browsers why are there so many Safari and Chrome differences?

This is true.  There is inherent fragmentation in open source, and I don't know how to solve that problem.  However, I would argue that less fragmentation is better than more.  Even if a single project gets forked many times and each is heavily modified, there is still a common base from which each fork descends.  As I originally said, a world without browser rendering discrepancies is unrealistic.  I just think we can somewhat diminish the problem by unifying on a common codebase and branching from it.

> All that this does is creates browsers with different versions of WebKit where some have features A, B, C, and some X, Y, Z and some that mix and match and some that implement B differently because they felt that B was implemented in a bad way.

Yes, but this is the nature of open source.  This is what happened with Linux, but eventually leading distributions emerged (Ubuntu and Android are examples of market-chosen leaders).  Because it's all Linux it's not _impossible_ for different versions to cross-pollinate.  [Ubuntu for Android](http://www.ubuntu.com/devices/android) is a great example of this happening with a degree of success.  If either OS was built on top of a different kernel, such a frankenstein would be impossible (or a lot less elegant, anyways).

> Also, Gecko is open source, so why WebKit over Gecko?

This much is my own personal opinion.  To be clear, the original post reflects my opinion, so take it with a grain of salt.  I prefer WebKit to Gecko for a number of reasons.  Anecdotally I experience less frustration when developing with WebKit, but (also anecdotally) I am finding WebKit in more places than you can find Gecko.  It's already in two mainstream desktop browsers (Chrome and Safari), it is the (enforced) only option on iOS, and many less-popular browsers already use it or are [switching to it](http://www.engadget.com/2013/01/18/opera-ice-webkit-browser-android-ios/).  WebKit's overwhelming market acceptance is why there's even talk of a WebKit monoculture to begin with.  The market is speaking: People want WebKit.

> All three of the top browsers will be rapid release soon, so this makes WebKit no different.

True.  The update problem will eventually solve itself.  I mainly brought up the rapid release cycle to demonstrate how this _is not_ IE6 all over again.  My bigger concern is that Web Developers still need to support multiple rendering engines (`-webkit`, `-ms`, etc.), which makes us less productive.  I feel that the prefix situation is ridiculous and needs to be fixed.  The Web Developer community needs to decide which direction to move forward with - I think WebKit is the way to go because it is already winning.

> What's wrong with Gecko and/or Firebug?

Again, this much is my opinion.  I feel that Chrome offers more powerful tools than the competition, but developers are of course free to make their own decisions.

> And, the fact of the matter is, each WebKit browser has it's own implementation of the dev tools (see point #1 again). I can't stand Safari's. So, you must just mean Chrome's or do you mean Safari's? Which is the "right" dev tools for WebKit that are the most "developer-friendly"?

My argument is that WebKit _itself_ is a development tool because it can be scripted for automated tests.  I'd bet Gecko has such capabilities, but I haven't seen a PhantomJS equivalent for Gecko.  The community does not seem to support Gecko as strongly as it does WebKit, and I favor options with the best community endorsement when selecting my toolset.

> How is Gecko more buggy than WebKit? Are there stats on how many bugs and their severity? Are there more security bugs? Which is safer? I notice more bugs too in Gecko, _however_, I work in WebKit all day.

I actually agree with this entire part of the counterargument.  And no, I don't have metrics.  I was referring to the bugs that a developer experiences during testing, not internal bugs or security issues.  Bugginess favors the platform you didn't start with.  I build with WebKit first, and anecdotally I find that a lot of other developers do too.  Surely there is a reason for this trend.  I would postulate that it's because a lot of developers have found WebKit and its associated tools to be a better choice in day-to-day development.

> In the land of unicorns and rainbows WebKit would be the only browser, innovation would continue, every fork would be a vanilla fork and would somehow work the same on Windows, OS X, Linux, iOS, WP8, and Android. Unfortunately, in the real world that's not how competition or technology works.

The community need ideals to pursue - this is how we unify.  Perfect harmony is unrealistic, but why can't web development be easier and faster than it is today?  I think that it can, and agreeing on a core component such as a rendering engine will get us a little closer to a better ecosystem.

## Footnote

I'm not trying to start a revolution.  In all likelihood, I'm way off-base with some of my theories, but it _is_ interesting to think about.  The WebKit monoculture is something of an elephant in the room for the Web Development community, and I think it's worth exposing and considering its implications rather than adhering to cultural dogma.