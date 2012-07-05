---
layout: post
title: "Treating JavaScript like a 30 year old language"
date: 2012-07-01 15:51
comments: true
categories:
---

I don't like JavaScript.  I write an enormous amount of JavaScript — in fact I write it almost exclusively — but I don't really like it as a language.  I don't want to write a giant screed as to why I don't like the language, but suffice it to say that it lacks some really basic features (like default parameters), and its lack of clearly defined rules (semicolons, whitespace) create lots of headaches.

Something that has helped me keep JavaScript manageable and even fun is the coding styles I have developed.  I create a lot of rules for myself that result in extremely readable and descriptive code.  This equates to lots of boring style constructs and boilerplate comments that add absolutely no features to what I'm writing, but go a long way to keep the code obvious and explicit.  I write JavaScript as though it were C, at least to some extent.  Why do I create this extra work for myself?  Because reading code sucks.  It will always suck, whether you are reading your own code or somebody else's.  Especially when it comes to my [open source projects](https://github.com/jeremyckahn), I really, really want people to read and contribute to the code I write.  It is absolutely worth it to take extra time to trivially polish code so that fellow humans can easily dive right in.  Additionally, I read my code many more times than I write it, so I want to have mercy on my future self by writing painfully obvious and straightforward code.

Much of my style is rooted in the [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml).  This is largely due to the fact that I need to follow this style guide in my day job.  However, I have fallen in love with the strictness of the Google Way, and have adapted it for my own open source projects.  For said open source projects, I don't follow Google 100% because, well, I have my own opinions on clean code.  It's needless to go over every minutiae of my style, but I think there a few basic rules that go a long way in keeping large amounts of code sane and manageable.

## 80 character line limits

There's nothing more irritating when trying to grok code than scrolling around to see the entire line.  It's a mental context killer.  While any text editor worth its disk space has the option to wrap text automatically, chances are your code will be read in an environment that doesn't.  This includes CLI programs (like diff and less) and web-based source viewers like Github.  Don't make people scroll, it's mean.

At some point in computer history, somebody (arbitrarily?) created an 80 character line limit for code.  It's formally documented in the [Python Style Guide](http://www.python.org/dev/peps/pep-0008/#maximum-line-length), and I think it's totally awesome.  This has two benefits.  First, as I mentioned, you eliminate the need to horizontally scroll.  More substantively, this promotes code simplicity.  When you restrict yourself to 80 characters before a line break, you're more likely to break statements up into smaller chunks.  I don't like clever code that crams a bunch of nested function calls into lines like this:

```javascript
setTransformStyles(context, buildTransformValue(this._transformOrder, _.pick(state, transformFunctionNames)));
```

This is painful to read.  There's so much to parse mentally, and I might even have to _scroll_.  I'd much rather read each meaningful chunk line by line, and then see how it all comes together:

```javascript
// Formatted version of the above snippet.  Taken from the Rekapi source.
var transformProperties = _.pick(state, transformFunctionNames);
var builtStyle = buildTransformValue(this._transformOrder,
    transformProperties);

setTransformStyles(context, builtStyle);
```

While I can add line breaks to the original one-liner to make it conform to the 80 character limit, the limit annoys me into breaking things up into shorter, more obvious statements.  I _want_ to be annoyed into this, it makes my code more readable in the long run.

## Strict-ish typing with annotations

The Google Closure Compiler has [a lot of rules regarding code annotations](https://developers.google.com/closure/compiler/docs/js-for-compiler).  These are necessary to allow the compiler to perform the "Advanced" compile-time optimizations, and it blows up when there is a type error.  The annotations serve to clearly communicate to the compiler what the expected inputs and outputs of every function are.

It turns out that taking the time to explicitly declare the input and output types of a function to communicate to the compiler have a nice side effect: The types are also explicitly communicated to humans!  Let's take an example of some magical code:

```javascript
function addNumbers (num1, num2) {
  return num1 + num2;
}
```

Simple enough, but what if we do this:

```javascript
var sum = addNumbers('5', 10);
console.log(sum); // -> 510
```

Whoops.  If the client of this code assumes that `addNumbers` will do any typecasting for them, they will get unexpected results.  However, if we explicitly annotate the function, we leave very little open to interpretation:

```javascript
/**
 * @param {number} num1
 * @param {number} num2
 * @return {number}
 */
function addNumbers (num1, num2) {
  return num1 + num2;
}
```

Much better.  Very clear, very explicit.  We can even take this a step further and add some documentation for the poor soul who has to read this code in the future:

```javascript
/**
 * Adds two numbers.
 * @param {number} num1 The first number to add.
 * @param {number} num2 The second number to add.
 * @return {number} The result of adding num1 and num2.
 */
function addNumbers (num1, num2) {
  return num1 + num2;
}
```

Now, you by no means have to get this detailed with every function that you write.  If a function is simple and obvious enough, I often just annotate the types and omit the documentation text.  Just be pragmatic about it.

## The `new` keyword

All of the cool kids seem to really hate the `new` JavaScript keyword.  Apparently it's totally old school and not at all trendy, so therefore you shouldn't use it.  Dmitry Baranovskiy seems to have a [particular distaste](http://dmitry.baranovskiy.com/post/something-new) for it.

Well, I really like the `new` keyword.  When I see `new` in code, I read it as "make a new instance of the following."  Here's an example of why I like this clarity:

```javascript
var kitty = Cat();
```

This is simple enough, but `kitty` could be anything. `Cat` could be giving us a `number`, for all we know.  I prefer this:

```javascript
var kitty = new Cat();
```

You may prefer to just capitalize your constructors, but I feel that using `new`  helps to clearly communicate that a function is actually a constructor.

## Compile-time defines

Compilers are totally awesome.  Generally speaking, you shouldn't deploy production code unless it's been compiled with tools such as the [Google Closure Compiler](https://developers.google.com/closure/compiler/) or [UglifyJS](https://github.com/mishoo/UglifyJS).  For my open source projects, I prefer UglifyJS.  I actually get better compression with Closure Compiler, but UglifyJS is easier to develop with.  UglifyJS also has a few really awesome features.  One that I've fallen in love with is code pre-processing with [compile-time defines](https://github.com/mishoo/UglifyJS#use-as-a-code-pre-processor).  This feature is a throwback from the C world, and probably other compiled languages that are older than I.  In any case, using defines lets you tailor your compiled binaries to fulfill various requirements.  For example, you can use defines to tailor a build for mobile platforms that need different code than desktop platforms.

I'm using defines for [Rekapi](https://github.com/jeremyckahn/rekapi)'s testing hooks.  There are some methods that I want to expose for my unit tests, but I don't want to expose them in the compiled code that gets sent to users.  It's just wasted bandwidth and CPU cycles to parse it.  Here's how I set it up:

```javascript
// At the beginning of the library
if (typeof KAPI_DEBUG === 'undefined') {
  var KAPI_DEBUG = true;
}
```

```javascript
// Later on in the code
if (KAPI_DEBUG) {
  Kapi._private = {
    'calculateLoopPosition': calculateLoopPosition
    ,'updateToCurrentMillisecond': updateToCurrentMillisecond
    ,'tick': tick
    ,'determineCurrentLoopIteration': determineCurrentLoopIteration
    ,'calculateTimeSinceStart': calculateTimeSinceStart
    ,'isAnimationComplete': isAnimationComplete
    ,'updatePlayState': updatePlayState
  };
}
```

`Kapi._private` has references to a bunch of methods that will never be used publicly, but need to be exposed for testing.  `KAPI_DEBUG` is a global variable (eeek!), but is only present in the source code, not the compiled binary.  This is thanks to my [build.js](https://github.com/jeremyckahn/rekapi/blob/master/build.js) script:

```javascript
var uglifyJS = require('uglify-js');
var jsp = uglifyJS.parser;
var pro = uglifyJS.uglify;
var ast = jsp.parse( _fs.readFileSync(_distFileName, 'utf-8') );

ast = pro.ast_mangle(ast, {
    'defines': {
      'KAPI_DEBUG': ['name', 'false']
    }
  });
```

This tells UglifyJS to set `KAPI_DEBUG` to `false` when it is compiled.  Because my debugging code is wrapped in conditional that tests the boolean value of `KAPI_DEBUG`, it is marked as unreachable code and not included in the binary.  Perfect!

Something to note: At the time of this writing, this feature is poorly documented, but a [Pull Request is pending](https://github.com/mishoo/UglifyJS/pull/343).

## I code like an old man

I've been writing JavaScript for three-ish years at this point and have built up some strong stylistic preferences.  It's worth noting that I started out with C++ before switching to dynamic languages.  While my coding style may not be everyone's cup of tea, it is optimized for readability.  I think a lot of the newer coding conventions do not lend themselves to clarity and approachability.  Yes, I use semicolons, `new`, and love a nicely architected inheritance chain.  I don't do these things out of obstinance, but practicality.  I suggest that you adopt whatever coding style results in code that is readable to others.

I write code that is boring, because boring code is _readable_ code.  I would contend that readability generally has more impact on the success of a project than micro-optimizations and stylistic experimentation.  If that means writing like a C coder in the 80's, then so be it.
