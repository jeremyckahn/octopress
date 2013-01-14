---
layout: post
title: "Making Life Easier With Grunt"
date: 2013-01-13 15:10
comments: true
categories: 
---

[Grunt](http://gruntjs.com/) is task management tool by [Ben Alman](https://twitter.com/cowboy) for JavaScript projects.  I've been playing around with it for a few weeks and have integrated it into [Shifty](http://jeremyckahn.github.com/shifty/) and [Rekapi](http://rekapi.com/).  Grunt has brought nothing but benefits to both projects.  While it doesn't do anything new or particularly flashy, it does do a great deal to __standardize and streamline development tasks__ you are already doing or seriously need to consider doing.  This includes:

  * Linting source files
  * Running automated unit tests at the command line
  * Concatenating and minifying source files into distributable binaries

These are just the tasks I have used so far.  Grunt does more than this out of the box, and you can extend it to perform any custom tasks you may need.  The point of this tool is to painlessly automate tasks you need to do repeatedly, probably many times a day.

## What I was doing wrong

The libraries I write need a build process so that users can easily grab a deployment-ready file and get to work.  Back in the day, I copy/pasted source files into the [Google Closure Compiler web UI](http://closure-compiler.appspot.com/home) and then copy/pasted the compiled code into a `.min.js` file.  This was annoying, so I eventually automated the process with a BASH script to do this.  This script was difficult to write and maintain, and it also required me to have an internet connection to contact the Closure API or have a copy of the compiler locally.  It was slow and cumbersome, but it worked.  Eventually, with the help of [Miller Medeiros](https://github.com/millermedeiros), I switched to custom Node scripts to build my projects.

For linting, I took a similar approach: I copy/pasted code into the [JSLint](http://www.jslint.com/) web UI, read the errors, fixed them individually, and then copy/pasted back and forth until the errors were fixed.

For testing, I just manually tested things in the browser.  I then discovered the joy of unit testing to automate this, and started writing QUnit tests which, again, I ran in the browser.  For larger projects, I have several testing suites, so I needed to check each one.

The consistent flaw with all of these approaches is that they are __manual processes__.  Programmers exist to automate solutions to problems, and I was not doing that.

## How I fixed it with Grunt

Grunt abstracts lint, test and build workflows into a system that is configured by a [Gruntfile](https://github.com/gruntjs/grunt/wiki/Sample-Gruntfile).  For me, the biggest benefit was being able to switch from a 150+ line custom build script to a much simpler configuration Object that achieved the same outcome.  Since linting and testing is controlled by that same configuration Object, it was trivial to add those tasks.  My codebases have already seen improvements from the ease of linting and testing, and I can make improvements more quickly and safely.

## Don't code tasks, configure them

The key lesson I learned is to __favor task configuration over implementation__.  My old build script needed to be re-read and understood every time I needed to change or fix something.  It was difficult to reuse for other projects because it was built specifically around the needs it was originally written for.  A tool like Grunt takes care of all of the implementation details.  

All build processes are fundamentally the same, and Grunt implements the concatenation and minification process for you.  You only need to specify input and output files, and Grunt is smart enough to take care of the rest.  This is much better than doing it yourself!  _Configurations are easier to maintain than implementations_ and are almost always faster to write at the outset.

## Standardizing the web developer workflow

A soft benefit of a tool like Grunt is that it helps to unify the common workflows of web developers.  It is easier to get familiar with a new codebase using Grunt because there is less infrastructure (building/testing/etc.) to worry about.  Another way to look it: Grunt does for workflows what jQuery does for cross-browser DOM manipulation and traversal.

## The way forward

As web apps become more sophisticated, so must our tools and workflows.  Other ecosystems have enjoyed powerful task and build systems (like [Make](http://www.gnu.org/software/make/) or [Rake](http://rake.rubyforge.org/)) for decades, and JavaScript is finally catching up.  I think that Grunt is the ideal tool to help power the next generation of web applications - it is easy to use, it is well-documented, and it has strong community support.  Most importantly, it does not get in your way and restrict you to a specific way of doing things.  Going forward, all of my projects will be using Grunt - definitely [give it a look](https://github.com/gruntjs/grunt/blob/0.3-stable/docs/toc.md) so you can start automating your workflow too.