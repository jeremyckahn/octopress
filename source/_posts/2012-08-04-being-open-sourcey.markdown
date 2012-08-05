---
layout: post
title: "Being Open Sourcey"
date: 2012-08-04 10:55
comments: true
categories: 
---

I absolutely love open source.  It's something that is fascinating on many levels, and it's also a ton of fun.  Depending on who you talk to, "open source" can mean a great many things.  At the core, open source is public access to computer source code.  Interestingly, this access has created religion-esque alliances and discords within communities for decades.  For my part, I am strongly on the side of open.  I initially became interested because it's fun to share code.  Over time, I further developed my beliefs and examined my motivations.  I have come to believe that open source is what's best for society on a global level.  I think it's important to be "open sourcey."

## What is "being open sourcey?"

Since I'm inventing a term, I should probably define it.  Being open sourcey means being a developer that writes open source code, while also working with the developer community to improve existing code and solve problems.

Writing code is just one, fairly small component of this.  Software development is heavily maintenance-oriented, and typing out code is actually a pretty trivial task.  The bigger challenge is iterating and improving code over time to meet new requirements while also fulfilling the original set of requirements.  Interestingly, this becomes exponentially more challenging over time, and it quickly becomes too much work for one person.

World changing code is _never_ written by one person.  World changing ideas may come from one person, but actual implementations are always the result of an organized and collaborative effort shared between many smart people.  Linus Torvalds did not write the entirety of the Linux kernel that is in use today, and John Resig did not write every line of the jQuery that we use today.  It takes one person to come up with an idea, but it takes a community to execute on it.

## Why be open sourcey?

There are many benefits in choosing to make code openly available.  I recently came across [an audio interview of Linus Torvalds](http://www.youtube.com/watch?v=bt_Y4pSdsHw0), and he succinctly explained why open source makes sense:

> I actually see open source as science.  If you don't spread your ideas in the open, if you don't allow other people to look at how your ideas work and verify that they work, you're not doing science.  You're doing witchcraft.  And traditional software development models where you keep things inside a company and hide what you're doing, they're basically witchcraft.

When your code is available to anyone that cares to read it, people can make suggestions about how to improve the code and potentially come up with something that was much better than the original.  Granted, such suggestions may be completely wrong, so some good judgment is needed to vet people's suggestions.  However, by closing code off from the world, you eliminate any possibility that your code will be passively improved.

It is highly unlikely that you will write code that is so astonishingly brilliant that no one else can write equivalently brilliant code.  Programming is simply not that magical.  If somebody wants to make the same time tracking app as you, but you don't share your code, they can simply write their own.  Hoarding and hiding your code is not going to effectively thwart your competition, it just wastes time.  We can accomplish more as a society by sharing and iterating on our code than we can by rewriting it.

## How to be open sourcey

Being open sourcey is pretty simple, really.  It boils down to writing and maintaining code and empowering the open source community.

Open source can't exist without code to share, so that's the first step.  The less obvious task is writing code that is sharable.  Write code for others to read.  Refine and groom it to be [as approachable as possible](/blog/2012/07/01/treating-javascript-like-a-30-year-old-language/).  If your code is sloppy and hard to follow, you greatly diminish the chance that someone will just come along and improve it.  Drive-by patches only occur when another developer is interested in working with your code, and shoddy code will deter a lot of people.

An important component of this is up-to-date automated tests and documentation.  The lack of either of these indicates a programmer that is unmotivated.  People generally don't want to work with other people that are unmotivated.  In addition to being a sign of respect for fellow coders, testing and documentation defines a clear description of the requirements of the code.  Testing is especially important to someone unfamiliar with the code.  When modifying unfamiliar code of any degree of complexity, there is a high probability that something will break.  Testing is an incredibly effective tool for communicating to a collaborator that they broke something early on.

The other part of being open sourcey is facilitating progress within the community.  There's a lot elements to this, but at a high level it's just a matter of encouraging contributions and rewarding participation.  Writing a patch is not a trivial task, and people need a reason to take time out of their day to do it.

When someone files a bug or submits a patch, _thank them_.  Praise them for being awesome and taking an interest in your work.  Do what you can to reward them for their efforts.  An anecdote:  In my [Shifty](https://github.com/jeremyckahn/shifty) and [Rekapi](http://rekapi.com/) projects, I had no need nor interest in building in AMD compatibility.  For both projects, someone came along submitted a Pull Request that added such functionality ([Miller Medeiros](https://github.com/millermedeiros) and [Franck Lecollinet](https://github.com/sork), respectively).  Adding this feature is not a small task.  While I personally didn't need AMD and was generally indifferent to the benefit that it added to either project, I thanked the contributors and accepted their Pull Requests.  I wanted to validate their hard work.  It was a minor risk on my part, because adding any functionality brings some amount technical baggage, but rewarding and encouraging my contributors was a worthy tradeoff.  Both Miller and Franck went on to contribute significant features to my projects.

The point is, strangers have no reason to help you, especially on the internet.  On the off chance that somebody does go out of their way to do something as considerate as write code for you - for free - reward them.  All it takes is a "thank you" and a merge.  Obviously you have to be judicious when accepting patches, but do whatever it takes to validate your contributors' efforts.

## It's not about you, it's about the project

In open source, you are not more important than your contribution.  It is absolutely necessary to put progress before egos.  If you submit a patch and it gets accepted, it's because your code was awesome - not you.  Likewise, if someone submits a patch that replaces large swaths of your code for better code of their own, you absolutely must accept it.  You'd be crazy not to.  The only thing that matters at the end of the day is that the code was improved.  Users will never know how much code was yours and how much was another contributor's.

[Take a look at this](https://github.com/documentcloud/backbone/graphs/impact).  It's a graph of contributor activity on Backbone.  Look at how small Jeremy Ashkenas's individual contribution gets over time.  The point of this isn't to downplay Jeremy's value in Backbone's development.  On the contrary, this shows that Jeremy knows a good patch when he sees it and is good enough of a leader to accept it.  Although he may argue with people on what should or should not be merged into the repository, at the end of the day he wants what is good for Backbone more than he wants what is good for his ego.

## Better code for a better future

Open source has a lot of practical advantages over the alternative.  It also happens to be incredibly fun to work with like-minded, talented people.  However, participating in open source - being open sourcey - takes a lot of discipline and humility.  It's an incredibly complex challenge, but it becomes much clearer when you focus on the end goal:  Producing better software to make the world a better place.