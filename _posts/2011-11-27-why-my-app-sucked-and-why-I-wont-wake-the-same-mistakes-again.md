---
layout: post
title: Why My App Sucked And Why I Won’t Make The Same Mistakes Again
tags: [programming, iOS]
---

When you’re learning, it’s important to make mistakes, that’s how you learn. When you spend 10 hours looking for what is wrong, and it turns out you wrote `if(x=1)` when you meant `if(x==1)`, I can guarantee you the next time you look for why a piece of code is magically broken, that will be the first thing you’ll check. If you do this enough times, you’ll find yourself fixing stupid mistakes before you even make them. That’s how you get good. 

### Preface 

The most important thing for me over the last 2 years of learning iOS development has been getting things wrong. This piece is about everything I got wrong in developing my first app, [Batting Goggles](http://www.hardballtimes.com/tht-live/introducing-batting-goggles-for-the-iphone-and-ipod-touch/). It's also about how fixed those mistakes.

I’m no self-help guru, this is just my experience with mistake making. Only now do I even feel confident that I can go into making an app without screwing up the things I’ve messed up in the past. I can do this because I am very wary of repeating these mistakes. So without further ado, I present to you Batting Goggles by the numbers. 

### Version 1.0

I finished Batting Goggles and I felt an immediate sense of accomplishment. It was the first thing I had ever truly created from scratch. The idea was [Craig’s](https://twitter.com/sabometrics) (my partner in app development), the execution was all mine. At first we weren’t on the same page of how to make what we wanted to make, but once we came up with the interface, it was smooth sailing. The app was very bare, but did everything that we had wanted it to do. You could find a player and pull up his heat map and find his stats for the last season. Then Craig asked me to add a feature. He wanted to be able to set Favorites, and a lineup for each of the current teams playing. This would make it easier to navigate through the app, instead of having to go through thousands of players every time you wanted to look for someone. (There was a search, but the point still holds). 

### Version 1.1

And with a lot of effort, I added a tab bar to the bottom of the screen with items for favorites and lineups. The reason it was so tough was because I had 1 view controller and a lot of booleans to check on the current status of the app. This was not a good idea and will never be one. Anyone who does this, please heed these words… don’t ever do anything that stupid in any aspect of your life. The amount of code that went into it was tremendous, but when it was done, I decided I would take a nice break from working on the app. Then the bugfixes came. 

### Versions 1.2-1.3

The break didn’t really happen, but eventually I got the bugs fixed up. Apple had just released the iPhone 3G[S] \(remember the box around the [S]?). They tested it on that the next time I wanted to submit, and for some reason it didn’t work. My guess is they actually hadn’t been doing a great job of testing it before, because the bugs that were added were pretty damn noticeable when you used the app when you switched between screens quickly. I had not been testing it like that, just how I would use it, so I didn’t notice it being broken. The lesson I learned: Test for even the oddest and most accidental ways to use an app. There are infinite ways to do things, and your way is only right to you. 

### Version 1.5

This was the last release for the 2010 season. We got a lot of bugs out of the way, and nothing too major feature-wise, so we called it a day. People were still downloading, but some were complaining that the stats in the app were out of date. This was true, we had no way of updating the numbers in the app, so they were based off the prior season which had ended 365 days earlier. At this point I resolved to add a lot of features to version 2.0 and turn those frowns upside down. It was November, and the new season started in April, so we had hoped to get it out in early March right in time for the baseball season. As it turns out, I wasn’t so good at estimating. 

### The Offseason

Craig and I talked over the features we wanted, and we decided that the first thing to tackle would be live stats. We wanted to make sure that people couldn’t complain about that anymore, and we figured out a pretty simple solution involving some Python scripts and Dropbox. We also wanted to expand the data all the way back to when MLB started keeping track of this info, so now we would have 3 years of data instead of 1. Then I found an app that I liked, and it had a baseball card view, so I added that to the app. I wanted to make Goggles multi-dimensional, instead of just providing heat maps. With this, you’d be able to just use our app as your go to for your daily baseball stats questions. I then decided to add on the side of the list, markers denoting what letter of the alphabet the person’s last name was, so you could navigate far quicker through the player list, much like you see in the Contacts app. From using Goggles I realized that clearing and editing the lists users made was a pain, so I was going to make that experience more in line with Apple’s standard apps.

### Version 2.0

As I was getting close to finishing version 2.0, I realized that I had done everything that involved the iPhone wrong. I didn’t understand Model-View-Controller. I used mismatching bracket/dot syntax which made it incredibly confusing to read. I’m pretty sure that some of the code I had written just worked by sheer witchcraft and backdoor deals with the devil. When I couldn’t figure out how to integrate some of the new features I was hoping to add, I realized it was time to tear it all down and rewrite it. I rewrote Batting Goggles over the course of a week. It didn’t take too long because the thought behind the original code was right, just often redundant and convoluted. I was able to bring in all the features that I had hoped to, and felt a lot better about my app. In all likelihood no one else even cared or noticed. When I released it I felt that same personal accomplishment, because really, I had made 2 apps, a broken one, and a better one. It is still not perfect, but it is actually decipherable now, and much more flexible if/when I want to add features or fix things. 

### Conclusion

I made lots and lots of mistakes, but it’s ok because it really was my first big project. One mistake that I failed to mention was that when I released version 2.0, it was August, and the baseball season was almost over. I felt bad for a bit to the customers who paid for it and were essentially beta testers for a year and change, and had no use for the app for almost the entire 2011 season. All that personal accountability has made me far more detail oriented, and anal-retentive about releasing sloppy work. Since then I have released 3 apps, all of which I can [proudly point to](https://fabisevi.ch/#work). I have another one coming out very soon, hopefully it’ll be more of a homerun than Batting Goggles.