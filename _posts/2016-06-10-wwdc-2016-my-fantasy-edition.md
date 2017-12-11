---
layout: post
title: WWDC 2016 — My Fantasy Edition
tags: [iOS, apple, programming]
---


WWDC is right around the corner! This post isn’t intended to be a prediction, as much as what I hope unfolds.

As Betrand Serlet, a former Apple engineer discussed in this 90 second video [clip](https://www.youtube.com/watch?v=jd97us27eSg), Apple often ships features iteratively. Projects start off private, only to be used internally, often times for a year or two. When they feel stable enough, Apple opens them up to 3rd party developers, and makes it an official API. Features that are deemed noteworthy and successful continue to build on, while others are simply forgotten.

The three technologies below have gone through this lifecycle the last few years, and I think they are ready to converge into a big way, changing how we use iOS every day.

### Universal Links

Since the first days of iOS, URL schemes were a way to take you from one app to another. You could provide some context with URLs like `myapp://profile`, but nothing more.

Then iOS 8 finally began allowing developers to break out of apps. Apple started allowing developers to create extensions, little parts of your app that can run in another app.

In iOS 9, Apple went even further down that route by adding Spotlight. This method of universal search combined with the `NSUserActivity` API allowed a developer to define entry points into their app. Most importantly though, Apple introduced ‘universal links’, real URLs like ones you’d find on the internet that would open a corresponding app instead of Safari. For example, if I sent you this Medium article in a text message and you had the app installed, it would open up in the Medium app, not a website. While a great idea, the implementation still left room for improvement, as users often get bounced into to an app without wanting or expecting to be.

### Remote View Controllers

If you’ve ever been in an app and wanted to send an email, Apple provides a way to pull up the Mail app without leaving the app you’re currently in. Apple lets developers open up this Mail view (`MFMailComposeViewController` for you nerds out there), to send messages from within another app. And so you have remote view controllers, screens from another app presented within your app.

Currently, if you want an experience like this, you’d have to integrate an SDK or do a one-off partnership with a company. I think iOS 10 will finally bring this functionality to all 3rd party developers. Imagine how quickly you could post a tweet by pressing a tweet button within an app and having it present a Compose Tweet screen instead of opening the Twitter app. How about calling an Uber when you’re in Google Maps, Yelp, or Foursquare? The possibilities are endless.

Implementing this can be made especially simple if you can just piggy back off the universal links that we mentioned before. Add a URL, and if the user has the app installed, it will present in your app without them having to go anywhere.

### Siri

Having been a part of iOS for almost 5 years now, Siri has gone through a similar lifecycle as these other technologies. Initially, Siri was a concierge for Apple’s apps from setting reminders to making phone calls. Apple started adding additional partners like Yelp, Wikipedia, and HomeKit vendors. People have been saying it for years, and at this point the tech world is convinced that a Siri API is most certainly coming in iOS 10.

I also believe Apple is ready to take this next step, and open it up to 3rd party developers. While I don’t think we will have the ability to add Siri functionality into our apps, I’m confident that we will be able to add our own app functionality into Siri. A likely implementation would be building queries that Siri can respond to by presenting the remote view controllers discussed above. Asking Siri to “find me an Italian restaurant” will pull up the remote view controller from Yelp, so you can satisfy those pasta cravings. Those who wish to dive into your app’s richer experience could use the `NSUserActivity` API and deep links, to have Siri launch you into the app in the exact place you wanted.

### Conclusion

Whether my fantasy becomes a reality, I think WWDC is going to be huge. I’m very excited, more so than I have been the last few years. If you see something like this Monday on stage at WWDC, I told you so. And if you don’t, then just remember I’ve been wrong before, but that doesn’t mean I won’t be right some day. 😉