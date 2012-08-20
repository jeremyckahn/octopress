---
layout: post
title: "Keeping it Sane: Backbone Views and Require.js"
date: 2012-08-18 12:09
comments: true
categories:
---

I love experimenting with application architecture and organization.  I build applications for fun, and each one gives me a chance to try out a new method for keeping a growing codebase manageable and readable.  I try to mix it up a but with each new project, but a number of consistent patterns have emerged and proven themselves useful time and again.

The same is true of my toolset.  I have come to really enjoy two libraries in particular - Backbone and Require.js.  Each one does one thing and does it well: Backbone organizes an application, and Require.js gets code onto the page.  What makes these libraries great is that they are not heavy-handed solutions - as long as you know how to use them, they don't lock you into some weird pattern that makes your code inflexible.

That being said, knowing how to use Backbone and Require.js is a discipline.  Without a consistent pattern to follow, even a small Backbone app can grow unmanageable and hard to build upon.  The patterns I'll discuss here are designed to grow with your app and make your life easier.


## Keeping it real small

Whether you use the patterns or tools I'll be going over, one concept that applies to nearly all projects is this:  Many smaller files are better than fewer large files.  It is much easier to read and comprehend a file that is 200 lines long than one that is 2000 lines.  Some files cannot be broken up into smaller chunks for any number of reasons, but often that can be a red flag that the code in that file is too tightly coupled and assumes too much about how it is being used.  You can think of it like building a house: You can create any number of floor plans with a large collection of bricks.  When you're working with an assortment of pre-assembled walls, it becomes harder to create a floor plan that was previously not considered.

While breaking up code across many files will result in a more complex directory structure, the tradeoff is worth it because you increase your chances of reusing certain bits of functionality in future projects.  However, you do wind up with a lot of files to work with and load.  It just so happens that Require.js is a very powerful tool for working with many files.


## Required bootstrapping

You don't need terribly much Require.js code to glue your app together.  Require.js's only footprint in your project should be the `require` or `define` function call that wraps the contents of each file:

````javascript
// A View module.  Use the view.viewName.js file naming convention.
define(['exports'], function (exportedObject) {
  exportedObject.View = Backbone.View.extend({});
});
````

It helps to put all of your View files in a directory called `view`.  The rest of this tutorial assumes this convention.  In addition to multiple View files, I like to have a single `init.js` file that serves as the entry point for an app.  Place this somewhere higher up your directory structure, because there should only be one of these and it should be differentiated from other files.

````javascript
// init.js
require(['view/button', 'view/slider'], function (button, slider) {
  // App initialization code goes here.  When this code runs, we can assume that 
  // the files `./view/view.button.js` and `./view/view.slider.js` are loaded
  // and ready to use as `button` and `slider`.
  var buttonView = new button.View();
});
````


## Backbone boilerplating

Some amount of boilerplate code is needed to build out a Backbone View, but luckily we don't need that much.


## Narrow Views


