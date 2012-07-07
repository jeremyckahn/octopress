---
layout: post
title: "A JavaScript Library Template"
date: 2012-07-05 17:17
comments: true
categories:
---

I really like to write JavaScript libraries.  This is because low-level programming interests me a lot.  Although JavaScript is an inherently high-level language, I find writing the abstractions that "just work" like magic for others to be really fascinating.  I've [written](https://github.com/jeremyckahn/c-qwncr) a [number](https://github.com/jeremyckahn/shifty) of [libraries](https://github.com/jeremyckahn/rekapi) of varying complexity, and I've developed a pretty good pattern that gives me a lot of flexibility when developing them.  Building a library to scale is a much different challenge than building an application to scale, and it's not discussed very much.

## Libraries versus apps

End users are the audience for applications.  Libraries are different, their audience is other developers.  This makes a big difference when architecting a library.  Applications are often very large and have a lot of dependencies, but good libraries are [small](http://microjs.com/).  I believe that libraries should follow the [UNIX philosophy](http://en.wikipedia.org/wiki/Unix_philosophy), they should "do one thing and do it well."

To achieve this, library code must be optimized for size and performance.  Dependencies, while not unreasonable to have, must be carefully considered and used sparingly.  Using [Backbone](http://backbonejs.org/) or [CanJS](http://canjs.us/) to structure the library codebase is probably not a good idea, because MVC frameworks add significant bloat and makes it less portable.  However, some degree of boilerplate is needed to develop and tie it all together.

## Introducing lib-tmpl

[lib-tmpl](https://github.com/jeremyckahn/lib-tmpl) is a small project that I wrote.  It is a skeleton project to build JavaScript libraries on top of.  It does several things for you.

### Built to scale, built for sanity

For a project of any size, structure is paramount.  It is very important to organize code in a logical way, for a number of reasons.  Most importantly, code must be approachable for others.  This is necessary for effective collaboration with fellow developers - successful projects are not a one-man show.  The best way to start organizing code is to have a directory structure that makes sense.  lib-tmpl follows the directory structure that I developed with [Rekapi](https://github.com/jeremyckahn/rekapi) and [Shifty](https://github.com/jeremyckahn/shifty), which is a hodgepodge of directory structures that I saw in various other libraries.  Each directory has a README that explains what it is for.

Another way to structure a library codebase is to divide it up into modules.  The pattern I follow is to have one "core" module that defines a constructor and basic utilities, and multiple non-core modules that each perform a specific task.  What a module should do entirely depends on your project, but it should serve to enhance the code that exists in the core.  lib-tmpl provides a very simple module pattern that clearly defines all of the sections that you should put your code (such as private/public functions and constants).

### "Best practices"

"Best practices" is kind of a weird, nebulous concept.  What seems obvious to one person is evil to another, so I tried not to get overbearing with this project.  There are certain practices that most developers seem to agree upon, such as testing, documentation, optimizing with a compiler.  lib-tmpl provides hooks for all of these.  While I simply made a directory to house documentation, I made choices regarding compiler and testing framework options.  For testing, I like to use [QUnit](http://qunitjs.com/).  I included that as a the default testing framework, along with some basic example tests.

lib-tmpl uses [UglifyJS](https://github.com/mishoo/UglifyJS/) as its build tool.  This means that lib-tmpl requires [NodeJS](http://nodejs.org/).  Building a lib-tmpl library is easy, thanks to the included `build.js` script.  The documentation explains how to use and extend the build script.

## Building better libraries

I have [my opinions](http://jeremyckahn.github.com/blog/2012/07/01/treating-javascript-like-a-30-year-old-language/) when it comes to JavaScript style.  lib-tmpl is built on those opinions, but you are encouraged to ditch them and form your own if they don't suit you.  Regardless of the style you choose, lib-tmpl's structure and included toolset should go a long way to help you build awesome JavaScript libraries and minimize friction.

lib-tmpl lives [here](https://github.com/jeremyckahn/lib-tmpl) and is open source.  Please fork and expand on the template to your liking.
