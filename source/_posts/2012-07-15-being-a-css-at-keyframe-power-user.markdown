---
layout: post
title: "Being a CSS @keyframe Power User"
date: 2012-07-15 14:56
comments: true
categories: 
---

Animation on the web should be done with CSS and not JavaScript.

JavaScript is powerful and versatile tool.  And that's good, because it's all web developers have to work with.  Especially [now](http://weblog.bocoup.com/javascript-arduino-programming-with-nodejs/) [that](https://github.com/charliesome/jsos/) [it's](https://github.com/grantgalitz/GameBoy-Online) [everywhere](http://nodejs.org/), we're really lucky that JavaScript is so flexible.  We live in kind of a strange reality where there's almost nothing that JavaScript _can't_ do that another language can.  However, it's kind of like a [multitool](http://www.multitool.org/) — it can do everything but it doesn't really excel at anything.  Certain situations call for specialized tools, and animation is one of those.

At first blush, animation doesn't seem like a "style" in the same sense that `border-radius` is a style.  The taxonomy is a little broken, but so it goes with technology.  CSS 3 gives us APIs and performance that let us bring the web to life with interfaces that would make [Minority Report](http://www.youtube.com/watch?v=NwVBzx0LMNQ) jealous.  This article discusses how to optimize for performance and eye-catching motion.

## All hail the GPU

First off, why is CSS the de facto better tool for building animations?  Simply put, __CSS can take advantage of a computer's GPU__.  This is a game changer for performance and animation fidelity.  A JavaScript animation operates by invoking a callback function many times a second.  This isn't fundamentally wrong, but it introduces quite a bit of complexity to an app.  JavaScript is single threaded, so it can only do one thing at a time.  If JavaScript is animating something, it's not responding to user input or network activity, and vice versa.

That much is more or less common knowledge, but what isn't discussed as much is the Garbage Collector and its impact on performance.  Because JavaScript takes care of memory allocation, the Garbage Collector has to come along and clean up the mess that we've made from time to time.  In most applications, this is fine and not noticeable.  However, this is a huge problem for animations.  The Garbage Collector literally stops all JavaScript from running, including animation callback functions, so there is a distinctive stutter from time to time.  This is especially noticeable in animations with a high frame rate, because code is being run more frequently and the Garbage Collector runs accordingly.

So, what to do about stuttering JavaScript bogging down our animations?  Sidestep the problem entirely: Let's kick our animations over to the GPU and free up the JavaScript thread and Garbage Collector.  With CSS `@keyframes`, we can allocate our resources more efficiently and let the browser optimize our animations.

## The prefix problem

One CSS rule isn't cool anymore.  You know what's cool?  A _billion_ CSS rules.  That's the current state of affairs with CSS 3, anyways.  This problem extends to `@keyframes`:

```css
.myAnimation {
  -moz-animation-name: myAnimation;
  -moz-animation-duration: 2000ms;
  -moz-animation-delay: 0ms;
  -moz-animation-fill-mode: forwards;
  -moz-animation-timing-function: linear;
  -ms-animation-name: myAnimation;
  -ms-animation-duration: 2000ms;
  -ms-animation-delay: 0ms;
  -ms-animation-fill-mode: forwards;
  -ms-animation-timing-function: linear;
  -o-animation-name: myAnimation;
  -o-animation-duration: 2000ms;
  -o-animation-delay: 0ms;
  -o-animation-fill-mode: forwards;
  -o-animation-timing-function: linear;
  -webkit-animation-name: myAnimation;
  -webkit-animation-duration: 2000ms;
  -webkit-animation-delay: 0ms;
  -webkit-animation-fill-mode: forwards;
  -webkit-animation-timing-function: linear;
  animation-name: myAnimation;
  animation-duration: 2000ms;
  animation-delay: 0ms;
  animation-fill-mode: forwards;
  animation-timing-function: linear;
}
```

This is our reality.  We're actually expected to do this.  This is currently what is necessary to have our animations run in all modern browsers.

Believe it or not, nobody really wants to write all this out.  Thankfully there are a [number](http://thecssguru.freeiz.com/animate/) of [tools](http://animationfillcode.com/) to ease the pain, but the current situation is innately broken.  Be kind to yourself, use these tools to automate this problem away.

## Multilayered easing

[Easing](http://matthewlein.com/ceaser/) formulae are a crucial component of any compelling animation.  A while back I discovered something kind of cool about easing formulae: If you animate different properties synchronously with different easing formulae, you can get some very natural and intriguing motion.  Most animations that we see on the web use the same easing formula for X and Y, so things move in a straight line.  However, if we mix and match formulae — say, `easeFrom` for X and `easeTo` for Y — we get [fun curves](http://rekapi.com/demo/bubbles.html) and [transitions](http://jeremyckahn.github.com/hackapi/squares.html).  I have written [Shifty](http://jeremyckahn.github.com/shifty/) and [Rekapi](http://rekapi.com/), JavaScript libraries that make it really easy to decouple animation properties from easing formulae.

Combining easing formulae is just as important for CSS animations as it is for JavaScript.  Fortunately, the [`animation-timing-function`](https://developer.mozilla.org/en/CSS/animation-timing-function) property allows for this:

```css
.combined-formulae {
  position: absolute;
  -webkit-animation-name: top-property-animation, left-property-animation;
  -webkit-animation-timing-function: linear, cubic-bezier(.895,.03,.685,.22);
  -webkit-animation-duration: 2000ms;
}

@-webkit-keyframes top-property-animation {
  0% { top: 0px; }
  100% { top: 300px; }
}

@-webkit-keyframes left-property-animation {
  0% { left: 0px; }
  100% { left: 300px; }
}
```

Definitely experiment with different easing formulae combinations.  I've built [a little tool](http://rekapi.com/ease.html) to make this easier.

## Automation is awesome

Getting an animation to look _just right_ involves a lot of iteration and tweaking.  CSS is absolutely not conducive to this.  Neither Chrome Dev Tools nor Firebug currently allow you to easily modify `@keyframes` dynamically, so we are mostly left to modify the source code and reload for every minor change.  This problem is exacerbated by the vendor prefix problem that was discussed previously.  There is a lot of boilerplate in CSS animations, and we shouldn't have to deal with any of that when designing an animation.

I think it is critically important to have powerful, high-level tools for this sort of thing.  Animations should be made graphically, not programmatically.  There are a [number](http://www.sencha.com/products/animator/) of [tools](http://labs.adobe.com/technologies/edge/) being [developed](https://github.com/Motorola-Mobility/ninja) that do exactly this, which is totally awesome.  We are essentially rebuilding in HTML 5 what the Flash world has enjoyed for over a decade with their authoring environment.

I think there needs to be good open source tools for this as well, which is why I am developing [Stylie](http://jeremyckahn.github.com/stylie/).  Stylie is an app that makes creating CSS 3 `@keyframes` animations a drag-and-drop experience.  It uses Rekapi to generate optimized, cross-browser CSS that you can copy and paste into your stylesheets.

## Choose the best approaches

The tools you choose to generate animations are largely irrelevant.  Use whatever tool makes you most efficient, be it open or closed, free or paid.  What matters is that you solve a problem with the correct strategy.  In the case of web animation, CSS is often a better approach than JavaScript because of GPU performance optimization and the lack of Garbage Collector pauses.  And, since actually writing an animation is such a slow and tedious task, let the computer do the work for you and iterate with a graphical tool.