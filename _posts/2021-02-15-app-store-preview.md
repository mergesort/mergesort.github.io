---
layout: post
title: App Store [P]review
tags: [society, industry, featured]
---

Apple's been [in the news](https://9to5mac.com/2021/02/12/developer-reveals-fake-app-store-reviews-and-scams/) quite a bit lately over concerns that many apps on the App Store are [little more than scams](https://twitter.com/keleftheriou/status/1356011069395755009). Some of these apps aren't even functional, they don't provide anything more than a screen with no functionality, only a button to purchase an indefinite weekly subscription. Many developers and consumers are confused or surprised that Apple isn't catching these scams, given Apple has a process for App Review which every app must go through, and while I'm not surprised given the breadth of the problem, I find myself thinking it's very problematic for the digital economy and consumer confidence in buying services through what once was considered a safe place.

Twitter, the company I work for, deals a lot with content moderation. I'd argue it's the largest existential threat to the company. Whether Apple likes it or not they've walked into the same position with the App Store. This may be news to them, having spent decades curating all sorts of content from music to workouts, but as the App Store has grown, they now serve billions of customers and work with millions of developers. Those developers are creating content that Apple has little control over, other than acting as a gating mechanism, and so their ability to exercise control over that content has diminished significantly.

Let’s skip past the debate about whether or not Apple should have this much level of control or whether the system needs to be reformed. Instead I'd like to talk about where I think Apple can patch the cracks in a broken App Store, before it breaks itself apart or is broken apart from the outside.

### The App Store

Apple treats every developer [the same](https://www.gamesindustry.biz/articles/2020-07-30-apples-claim-that-we-treat-every-developer-the-same-tested-by-us-congress) (😉), or at least let's say so for the sake of this argument.[^1] From my own work, what I've seen is that when you don't have any way of validating whether someone is a good actor or bad actor, the reasonable default assumption is that everyone is a bad actor, and that's how Apple treats developers. This leads to many false negatives and false positives, good developers getting much more scrutiny than they should, and bad developers sliding through when they are in need of scrutiny. There's no thorough process for validation, there's no process for [restorative justice](https://en.wikipedia.org/wiki/Restorative_justice), only Apple doing their best to remain hyper-vigilant at all times, and accepting the human errors that come along with that.

While you can't eliminate bad actors, they're always going to exist in any system, what you can do is minimize the total bad actor surface area, and minimize the effects of these bad actors. A simple equation: if you treat 100% of developers as potential threats, there's no way to avoid hyper-vigilance, but if you only have to watch out for 20%, then you can be five times more efficient at rooting out bad behavior such as scams.

So we need a way to let bad actors tell us that they're bad? No, we need a way for good actors to signal to us that they're good, leaving everyone else in questionable territory. Apple needs an internal scoring system to know where to devote their investigative resources. If you don't need to pay attention to the well-meaning app developer trying to make an honest buck, you can devote more resources, or your limited resources to the people who haven't done the work to show that they're good actors.

### Incentive Design

Let’s take a step back to understand our friend from the world of behavioral economics, incentive design. [To quote liberally:](https://www.behavioraleconomics.com/resources/mini-encyclopedia-of-be/incentives/)


> An incentive is something that motivates an individual to perform an action. It is therefore essential to the study of any economic activity. Incentives, whether they are intrinsic or extrinsic (traditional), can be effective in encouraging behavior change, such as ceasing to smoke, doing more exercise, **complying with laws or increasing public good contributions**. Traditional incentives can effectively encourage behavior change, as they can help to both create desirable and break undesirable habits. 

I don't have all the answers for fixing the App Store, but I don't think you need all the answers up front to start improving the system. Taking what we learned about incentive design above, what I see Apple having is a resource allocation problem due to them not knowing who’s complying with the rules and contributing to the public good. With that in mind, a scoring system is where I would invest resources to know who’s having a net-positive and a net-negative effect on the App Store system.

There can be many contributors to this scoring system. Right now reviews and downloads are already used, but they are gameable due to their public nature, an example of poor incentive design. Surely new metrics can be added, such as how many times they've passed the scrutiny of app review, or how closely the instructions a developer gives match the reviewer's expectations. While those are relatively weak signals, Apple surely has dozens if not hundreds more internal signals they can apply to understanding a developer’s net outcome on the App Store. And yet I think there's room for a much stronger signal.

### App Store Preview

App Store Preview would work similar to Apple's current [DTS system](https://developer.apple.com/support/technical/), where you can get hands-on help with a technical problem you're having. A developer should be able to get pre-approval for an idea[^2], in the context of their application, without having to build an entire feature (or application) before App Review deems it worthy. This would also provide context for future reviewers, knowing what to look for and what's changed. The more a pre-approved version matches the reviewer's expectations come review time, the higher the score would the developer would receive. The higher their overall score over time (by some to be established scoring mechanism), the less scrutiny they would receive in the future.

More importantly though is the inverse. If someone doesn't go through review, they implicitly receive more scrutiny. Bad actors will be disincentivized to have their app in Apple's hands for longer, and to be put under a microscope. This aversion makes them inherently less trustworthy, and would lead to them getting more scrutiny in the future.

By letting good actors prove they're good actors, we've isolated the bad actors to show their cards and prove through implicit means that they're not good actors.

---

This wouldn't fix the mistakes that App Review makes, and bless them, it's a very tough job. This doesn’t even solve many of the App Store's problems, it’s only one idea and there are many other problems that Apple needs to solve. But it does show that Apple has lots of levers to pull when designing resilient systems, and can lay the foundation for a system where Apple can trust developers. And that's increasingly necessary for maintaining the consistency quality Apple, developers, and customers all want for the App Store.

As always, I’m excited to hear your thoughts, and am receptive to [feedback](https://twitter.com/mergesort), so if you want to talk don't be shy about sending me a trustworthy tweet.

[^1]: To paraphrase George Orwell, "all developers are equal but some are more equal than others."

[^2]: Given this is time intensive, you could make validation finite, maybe 2-4 tickets per year, or even have a system where people can pay for more tickets to have more previews, something that would surely be valuable for many developers and Apple.
