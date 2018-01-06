---
layout: post
title: Everyone Should Use Generics Except You
tags: [featured, go, programming]
---

As I was on hour six of debugging how to read an object from the database, my brain suddenly noticed the slight difference in two lines of code. The compiler error had been off, too vague to help me realize that I was never hinting the correct type to the function. Generics had struck again. I cursed in the general direction of my cat (unintentionally), and moved on. There was nothing I could do but accept that we've all been there, and move on.

The creators of the [Go](https://en.wikipedia.org/wiki/Go_(programming_language)) language have so far resisted the notion of adding generics. They have a well considered argument that adding generics into the language will add to it's complexity, so much so that the power of the feature will be outweighed by the complications that the feature brings. What proponents of generics say is that the core team is not properly considering all the benefits of generics. The language's surface will be simplified, your code as a consumer will be easier to write, and even that Go already has generics but only for certain blessed types that are built into the language.

---

Combining the two thoughts above, I had a thought of my own, since everything's a remix after all. We boil down our problems to platitudes, as if fixing that one problem will be salvation for our existence. Functional is better than object oriented. React is better than Angular. Static is better than dynamic (it is…).

Writing generic code is one of those trade offs. It can be mind bending, it's no walk in the park, but it can be incredibly powerful. I don't personally agree with the Go authors, but I'll boil the problem down to a platitude of my own:

>I want generics in my language. I don't want anything to do with them myself 95% of the time, but I would love the features that others can build which capitalize on generics to make my life easier.
