---
layout: post
title: The Expressive Nature of Swift
tags: [featured, swift, programming, iOS]
---


<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Ignores commenting on another static vs. dynamic dispatch article because people won’t accept Swift is a hybrid not plain static.</p>&mdash; Joe Fabisevich 🐶🐳™ (@mergesort) <a href="https://twitter.com/mergesort/status/735132240808706050">May 24, 2016</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Guess that didn’t last long.

There’s a [conversation](http://khanlou.com/2016/05/six-months-of-swift/) [happening](http://chris.eidhof.nl/post/dynamic-swift/) [in](https://twitter.com/wilshipley/status/735609509993807873) [the](http://inessential.com/2016/05/25/oldie_complains_about_the_old_old_ways) [iOS](https://www.noodlesoft.com/blog/2016/05/23/on-dynamism/) [community](http://bitsplitting.org/2016/05/24/not-perfected-here/) [at](http://www.manton.org/2016/05/apples-mindset-on-swift-dynamic-features.html) [the](http://blog.metaobject.com/2016/05/what-missing-in-discussion-about.html) [moment](http://shapeof.com/archives/2016/5/dynamic_swift.html), [static](https://ashfurrow.com/blog/adulterated-objective-c/) vs. [dynamic](http://inessential.com/2016/05/15/the_case_for_dynamic-swift_optimism) [programming](http://inessential.com/2016/05/14/the_tension_of_swift). On one side we have many people who have been writing Objective-C for over 20 years (wow!) saying that the dynamism of Objective-C is the reason why it is an amazing language, and has succeeded. The argument is predicated on the fact that those nay-saying it don’t understand the power of dynamism, and how it’s empowered programmers. On the other end you have many people saying that static languages are the way forward, and that a whole class of errors is avoided, and that we should look at all the bugs prevented by having a good type system!

This back and forth ignores that Chris Lattner, the creator of Swift, has himself stated that [Swift is a hybrid,](https://lists.swift.org/pipermail/swift-evolution/Week-of-Mon-20151207/001948.html) not explicitly static or dynamic. His explanation is very interesting, because it takes the argument from being black vs. white and turns it into many gray shades. Other languages have explored these concepts before, with ideas like [gradual typing](https://en.wikipedia.org/wiki/Gradual_typing), which was born out of the idea of grafting a type system onto dynamic languages, not making static languages more expressive.

But what exactly is expressiveness? As this [StackOverflow post](https://stackoverflow.com/questions/638881/what-does-expressive-mean-when-referring-to-programming-languages) explains (always cite your StackOverflow posts kids):
> ‘Expressive’ means that it’s easy to write code that’s easy to understand, both for the compiler and for a human reader.<br><br>
> Two factors that make for expressiveness:<br><br>
> • Intuitively readable constructs<br>
> • Lack of boilerplate code

Peter Norvig has a [great talk](https://norvig.com/design-patterns/design-patterns.pdf) on design patterns in programming languages. One slide stuck out to me as I was reading it recently.

![Design Patterns by Peter Norvig]({{ site.url }}/assets/img/design-patterns-norvig.png)


Let’s break that down:

1. There are fewer design patterns in expressive languages, because the type system does not prevent programmers from trying to express a concept.

1. Dynamic languages by their very nature of a weak type system have less issue being expressive.

1. This does not rule out static languages from being expressive!

The lack of expressiveness of static languages is dogma attached from other static languages that have existed before. I’d argue that Go is as expressive as Python, and Swift, even in its incomplete state, is nearly as expressive as many dynamic languages. You can recreate the advantages Objective-C offers through its dynamic nature by using different expressive techniques, like protocols and generics, in a statically typed language.

One more thing: Many arguments imply that Apple hasn’t thought about writing apps, that they built a static language, and forgot to take into account. Care to tell me which company writes apps on the most iPhones in the world? That’s right, Apple. I don’t think they’re stupid enough to create a language which they believe is objectively worse for writing apps.

Regardless of how this whole static vs. dynamic “conversation” turns out, one thing’s for certain, I’m #TeamSwift.
