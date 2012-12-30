---
layout: post
title: "Keeping It Sane: The Joy of Constants Modules"
date: 2012-12-29 19:46
comments: true
categories:
---

The first programming language I learned was C++.  C++ has support for something called ["constants"](http://goo.gl/LQpg), which didn't seem terribly interesting or valuable to me at first.  The idea of a read-only variable seemed kind of pointless, and the syntactic implications felt annoying.  It wasn't until later that I saw the benefits of constant variables - they give meaning to values and don't let a programmer modify them inadvertently.  Given the complexity of pretty much every piece of software, having a guaranteed and predictable variable value is indispensable.

On [recent](https://github.com/jeremyckahn/pine/blob/75132c806c3b602efed67f0f8e4c5c423f59f4d6/ui/public/js/constants.js) [pet projects](https://github.com/jeremyckahn/jumpjump/blob/10c9c1f654b44a622d68cff4a1d5a68fa884439b/src/constants.js), I've been using [Require.js](http://requirejs.org/) to isolate my constants into a single AMD module that I can access at-will.  This has proven to be incredibly useful in keeping my code clean and decoupled, and I think that a similar pattern can benefit any project.

## Data vs. logic

First of all, what should be a constant, and what shouldn't?  Simply, any value that represents [immutable](http://en.wikipedia.org/wiki/Immutable_object) data should be a constant - everything else is logic.  A color string, a placeholder string, anything with a literal value - these are all data.  Mathematical formulas, property names (like CSS properties), and conventional components (like the leading `on` in DOM event names) are logic.  Logic should be defined where it is used, and data should be decoupled and defined in a dedicated location.

## DRY

The most obvious benefit to using constant variables for your data is that it helps to reduce repetition in your code.  This is necessary to achieve a [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself) codebase, which is almost always ideal.  DRY isn't just a buzzword, it has many real-world benefits.  A DRY codebase is easier to maintain, because you don't have to hunt around for all instances of a piece of data.  For example, you may have a color that indicates the health level for a character in a game.  Let's say that "green" means "healthy".  

```javascript
// Notice that the variable is named after what it represents, not the value 
// itself.  i.e., it is not "GREEN."
var HEALTHY_COLOR = '#0f0';
```

If you decide to change this color to something else, you don't want to dig through the entire codebase and hope that you got every instance of `#0f0.`  It is much easier in the long run to define this value once and only read from it after that.  This also makes automated find-and-replace tools more reliable.

To make life even easier, consolidate your constants into a single file.  This isn't strictly necessary, but it's that much less searching you have to do when you want to modify a constant.

## Constants as configuration

I'm of the opinion that good code reads more or less like a configuration file.  That is, each line operates as a distinct component of an application and is decoupled from the code around it.  This isn't feasible in most cases, but it's a ideal to strive for.  One way to decouple code is to separate it out into modules, which Require.js is built exactly for.

As I mentioned, it's best to put all of your constants into a single module file.  This seems trivial, but it provides a subtle benefit - this module turns into a sort of "config file" for your entire application.  This assumes that you are diligent about separating your logic and data.  If you were building a physics simulation, you may want to tweak the acceleration due to gravity, or the coefficient of friction for a given material.  All of your tweaking only needs to happen in one place, rather than jumping around the codebase to make changes.

## Meaningful code

In addition to decoupled code, I strive for readable, meaningful code.  In essence, I like code that reads like prose, or at least a sort of broken english.  [Some projects](http://cukes.info/) take this too far, but ultimately we don't want to be human compilers.  Code should be readable, and meaningful variable names let us do that.  A standard convention for constants is to `NAME_THEM_LIKE_THIS`.  This tells whoever is reading the code that the variable is a constant and can/should not be modified.  It also helps to communicate your intent.  The semantic intent of this jQuery code isn't very clear:

```javascript
$('.name').css('background', '#f00');
```

But this is: 

```javascript
$(NAME_FIELD_SELECTOR).css('background', REQUIRED_COLOR);
```

Most importantly, you want to reduce the amount of guesswork that another programmer has to do in order figure out what you were trying to accomplish with a given piece of code.

## Faith-based constants

Despite all of the virtues I have extolled of constants, JavaScript doesn't actually support them.  The only way to have "real" constants in JavaScript is to run your code through a compiler like the [Google Closure Compiler](https://developers.google.com/closure/compiler/) (with the `@const` annotation).  It appears that `const` support is [coming to the language in ES 6](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Statements/const), and that some browsers already support it.  Assuming you are targeting a wider audience, you are left to hope that the value of your constants are not modified by an unsuspecting future developer.  This is not ideal, and short of using the Closure Compiler, you simply have to be diligent with not writing to constants.  `VARIABLE_NAMES_LIKE_THIS` should go a long way toward preventing mistakes, however.

## Constant improvement

Constants make your life easier.  While you won't explicitly think about the benefits I outlined above when using them, they do have an immediate impact on the readability of your code.  Constants will help you to separate logic and data and keep your code decoupled.  With any luck, we'll see constants standardized and not need to depend on tools and conventions to enjoy the benefits.