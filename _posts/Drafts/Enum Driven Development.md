---

Help: Code blocks

https://docs.decksetapp.com/English.lproj/Formatting/06-code-blocks.<html id="highlight-lines-of-code"></html>


---

## Drag & Drop images

### Simply *drop an image onto the Deckset window* and the Markdown you need to display the image is automatically created and *copied to the clipboard.*

---

* This works with both local files and web images
* You don’t _have_ to drag the file, you can also type the Markdown yourself if you know how

![left,filtered](http://deckset-assets.s3-website-us-east-1.amazonaws.com/colnago1.jpg)

---

Write a blog version of your talk. Seriously.

---

Read before starting:

https://medium.com/@loic/what-great-speakers-do-6ec030348ab

https://mislavjavor.github.io/2017-04-19/Swift-enums-are-sum-types.-That-makes-them-very-interesting/?utm_campaign=This%2BWeek%2Bin%2BSwift&utm_medium=email&utm_source=This_Week_in_Swift_128

---

[collage of tweets about enums with heart eyes emoji over them]

I told my wife I was going to talk about enums,

She's a JS programmer

[Pause for boos and hisses slide]


 and she just did a ¯\_(ツ)_/¯
Isn't it like enums in any language? And I was like, NO! They're powerhouses in Swift

---

https://twitter.com/mergesort/status/844666442352148480
https://twitter.com/mergesort/status/730144887971192832
https://twitter.com/mergesort/status/786019354429231105
https://twitter.com/mergesort/status/507922584709496833

---

### Intro

---

• Everyone talks about protocol oriented programming, but I'm going to talk about enum oriented programming instead.

---

• I believe that you can make your code a lot simpler, easier to follow, and even maintainable if you focus on utilizing enums.

---
• In fact, my approach is to make everything an enum, until I see the need otherwise.

---

• Not only that, enums are will get you a pony.

---

• Enums are great. They are my favorite language feature in Swift.

---

### First let's look back at Objective-C

---

* Enums were fine… Like the way that your first date is fine, and then you just never go on a second date.
• All enums were was a bunch of numbers. Literally. They were shortcuts to integers, nothing more, and nothing less.

---

### Now let's look at everything they can do in Swift.

---

- enumerating - like old languages and such

---

- Union types - this is what everyone's most familiar with, a situation where something is one or the other or the other.

---

- Associated values - be able to model out new APIs where the case not only represents a state, but has data that goes with it. Show how that can be valuable

---

- State machines - an example of how you can do unloaded, loading, loaded state machine, transferring values between 'em, onboarding

---

Declarative architecture - Enums define their own values as extensions, and perform transforms from one data type to another.

As a developer, my goal isn't to make code more testable, but to reduce as much code that needs to be tested.

---
- Namespaces - api wrapper or something else like that… benefits, uninstantiatable, static lets/vars, hide away abstraction details from consumers of your API

---

### Conclusion

---
Now let's see how that all comes together, you can build a whole app really only using enums for all your data. (Maybe a simple Instagram clone type thing?)

---
When I finished explaining this to my wife, she said, you know what, that's pretty legit. And I hope you do too.
