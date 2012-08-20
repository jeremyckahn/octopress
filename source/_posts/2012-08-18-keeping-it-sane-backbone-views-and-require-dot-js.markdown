---
layout: post
title: "Keeping it Sane: Backbone Views and Require.js"
date: 2012-08-18 12:09
comments: true
categories:
---

I love experimenting with application architecture and organization.  [I build applications for fun](https://github.com/jeremyckahn), and each one gives me a chance to try out a new method for keeping a growing codebase manageable and readable.  I try to mix it up a bit with each new project, but a number of consistent patterns have emerged and proven themselves useful time and again.

The same is true of my toolset.  I have come to really enjoy two libraries in particular - [Backbone](http://backbonejs.org/) and [Require.js](http://requirejs.org/).  Each does one thing and does it well: Backbone organizes an application, and Require.js gets code onto the page.  What makes these libraries great is that they are not heavy-handed solutions - as long as you know how to use them, they don't lock you into some weird pattern that makes your code inflexible.  Additionally, they work very well together.

That being said, knowing how to use Backbone and Require.js is a discipline.  Without a consistent pattern to follow, even a small Backbone app can grow unmanageable and hard to build upon.  The patterns I'll discuss here are designed to grow with your UI and make your life easier.

I have built a sample project that puts the patterns I'll discuss into use.  __You can find the code [here](https://github.com/jeremyckahn/require-and-backbone-views).__


## Keeping it real small

Whether you use the patterns or tools I'll be going over, one concept that applies to nearly all projects is this:  Many smaller files are better than fewer large files.  It is much easier to read and comprehend a file that is 200 lines long than one that is 2000 lines.  Some files cannot be broken up into smaller chunks for any number of reasons, but often that can be a red flag that the code in that file is too tightly coupled and assumes too much about how it is being used.  Think of it like building a house: You can create any number of floor plans with a large collection of bricks.  When you're working with an assortment of pre-assembled walls, it becomes harder to create a floor plan that was previously not considered.

While breaking up code across many files will result in a more complex directory structure, the tradeoff is worth it because you increase your chances of reusing certain bits of functionality in future projects.  However, you do wind up with a lot of files to work with and load.  It just so happens that Require.js is a very powerful tool for working with many files.


## Required bootstrapping

You don't need terribly much Require.js code to glue your app together.  Require.js's only footprints in your project should be the `require` or `define` function calls that wrap the contents of each file:

```javascript
// A View module.  Use the view.viewName.js file naming convention.  This file
// would be called view.button.js.
define(['exports'], function (button) {
  button.View = Backbone.View.extend({});
});
```

I like to use the [`exports` syntax for defining modules](https://github.com/jrburke/requirejs/wiki/Differences-between-the-simplified-CommonJS-wrapper-and-standard-AMD-define#wiki-magic).  It is syntactical sugar and is not required for this pattern, but it saves me from having to `return` the module from somewhere in the middle of the file.

It helps to put all of your View files in a directory called `view`.  The rest of this tutorial assumes this convention.  In addition to multiple View files, I like to have a single `init.js` file that serves as the entry point for an app.  Place this somewhere higher up your directory structure (it is in the top level for this example), because there should only be one of these and it should be differentiated from other files.

```javascript
// init.js
require(['view/button', 'view/slider'], function (button, slider) {
  // App initialization code goes here.  When this code runs, we can assume that 
  // the files `./view/view.button.js` and `./view/view.slider.js` are loaded
  // and ready to use as `button` and `slider`.
  var buttonView = new button.View();
});
```

One really great feature of Require.js is the [optimization tool](http://requirejs.org/docs/optimization.html).  Having a lot of files equates to many HTTP requests, which is slow.  Require.js makes it very easy to build one single binary out of all of your modules, making for a much quicker download.


## Backbone boilerplate

Some amount of boilerplate code is needed to build out a Backbone View, but luckily we don't need that much.  The pattern I use for Backbone Views more or less echoes that [pattern that I use for writing from-scratch JavaScript libraries](/blog/2012/07/05/a-javascript-library-template/), because it's flexible and lends itself to modularity and sane public/private APIs.  You can see a working example of this pattern in the [companion project](https://github.com/jeremyckahn/require-and-backbone-views) I built for this tutorial, but the basic pattern is this:

```javascript
define(['exports'], function (exportedObject) {
  
  // PRIVATE UTILITY FUNCTIONS
  //
  
  function noop () {}
  
  // This is where we define the View.  Every property on this Object is 
  // exposed publicly.
  exportedObject.View = Backbone.View.extend({
    
    'events': {
      'click': 'onClick'
    }
    
    /**
     * @param {Object} opts
     */
    ,'initialize': function (opts) { }
    
    /**
     * @param {jQuery.Event} evt
     */
    ,'onClick': function (evt) { }
  });
});
```

There are a few things to keep in mind with this approach.  First, try to keep your View's public API as small as possible.  Expose only the methods that are needed to let your View do its job, as well as event handlers.  It is easier to work with a View that has a small interface, because it helps to abstract away the implementation.  Client code should never have to know about your View's implementation (that's called a [leaky abstraction](http://en.wikipedia.org/wiki/Leaky_abstraction)).  If your View needs to do a complex computation, consider moving that logic into a helper function (inside of the area marked as `PRIVATE UTILITY FUNCTIONS`) that is called from a public method:

```javascript
define(['exports'], function (exportedObject) {
  
  // PRIVATE UTILITY FUNCTIONS
  //
  
  function longComplexCalculationImplementation () {
    // Implementation code goes here
  }
  
  exportedObject.View = Backbone.View.extend({
    
    // Remember, this is a public API.
    'performLongComplexCalculation': function () {
      longComplexCalculationImplementation();
    }
  });
});
```

The point of this is to move as much implementation code out of the View as possible.  A View should have a simple structure - use it for wiring up events to logic and building out APIs.  This helps to isolate complexity into discrete components.

Another thing to keep in mind with this pattern is the organization of your View's methods.  Try to group them by their purpose.  The order of the groups is up to you, but I prefer to go with something like this:

  1. `events` map
  2. `initialize`
  3. Event handlers
  4. Non-event handler public APIs

Here's an example:

```javascript
Backbone.View.extend({
    
  'events': {
    'click': 'onClick'
    ,'click button': 'onButtonClick'
  }
  
  ,'initialize': function () {}
  
  ,'onClick': function () {}
  
  ,'onButtonClick': function () {}
  
  ,'aPublicMethod': function () {}
  
  ,'anotherPublicMethod': function () {}
});
```

The goal is to build towards a consistent View organization.


## Narrow Views

My organizational approaches may or may not be your cup of tea, as patterns are always subjective.  What appeals to one person is weird and ugly to another.  In any case, there are some design patterns that are a little more universal.  One such pattern is keeping Views narrowly focused.  In other words, any given View should be concerned with as little as practical.  The trick is finding a balance between a View that is overly granular and one that is too heavy-handed.  In my [example project](https://github.com/jeremyckahn/require-and-backbone-views), I have a `UIMischief` View that just manages some buttons that grow and shrink.  I could have taken it a step further and made a View to represent each button, but that would have been unnecessarily abstract and would not have added much to the structure of the app.  One of the advantages of the pattern I use is that it's fairly easy to refactor Views into larger or smaller Views if needed.  As long as your code is modular and complexity is isolated into small functions, it should not be hard to move things around.

One way to gauge how "narrow" a View should be is to think about components that will be duplicated in your app.  Any UI component that may have multiple instances warrants having its own View.


## Keeping the peace

Regardless of how you choose to structure your application, pick a method that is consistent and scalable.  The pattern I use has helped me build [Stylie](http://jeremyckahn.github.com/stylie/) and my in-progress [Pine](https://github.com/jeremyckahn/pine) UI.  I strongly recommend that you use some kind of open source framework such as Backbone or [CanJS](http://canjs.us/), because a lot of people have already solved many of the problems you will run into when trying to build an app.  As a project grows, managing complexity becomes far more difficult than writing new code.  Research a solution that works for you.