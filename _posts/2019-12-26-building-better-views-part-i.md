---
layout: post
title: Building Better Views (Part I)
tags: [programming, swift, featured]
---

As iOS developers, a lot of our work involves taking models from a server, and transforming them to be displayed on an iPhone or iPad. This sounds like a job for some declarative architecture. 🤔

<blockquote class="twitter-tweet" data-theme="dark"><p lang="en" dir="ltr">If you ask 3 programmers how to define MVVM, expect to get 7 different responses.</p>&mdash; ✨ Joe Fabisevich™ ✨ (@mergesort) <a href="https://twitter.com/mergesort/status/720706593982062592?ref_src=twsrc%5Etfw">April 14, 2016</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Confession: I’ve never fully bought into MVVM. I don’t think it’s worse than MVC. I use View Models as a place to store state and actions for View Controllers, and preferably stateless functions for manipulating data. In my experience, things become harder to maintain when they start becoming a crutch, as a place to put your code if it doesn’t neatly fall into the Model, View, or Controller label.

With this in mind, I realized we need an answer for configuring our views in a way that’s maintainable, and ultimately transforms one or multiple models into a view. This led me to the idea of `ViewData`. I started working on this with [@shengjundong](https://twitter.com/shengjundong) at [Timehop](https://www.timehop.com/), and have been using it successfully across apps of varying sizes since.

There are three parts to this approach:

1. A `UIView` instance. This is your standard view that you’ll be displaying in an app. It can be a regular class, or a custom subclass as you need.

2. A `ViewData` protocol. This is what’s going to keep track of the data that needs to be displayed in your view. Most commonly this will be a slice of a model, used specifically for rendering the view.

3. A `configure(viewData: ViewData)` function. This is what’s going to map your View to your ViewData.

![A diagram explaining the interaction flow of ViewData]({{ site.url }}/assets/img/view_data_diagram.png)

##### An Example

Let’s start with an example, where we’re building a view to display a comment. It will have a few properties you’d expect from a comment view. A commenter, their avatar, some text, and a timestamp. To make it easier to visualize, let’s imagine it looks like this:


![A visual example of a commment box we're going to build in code]({{ site.url }}/assets/img/comment_example.png)

We start with a simple model. This is what we’ll be later manipulating for display purposes.

    public struct Comment {
      let text: String
      let commenter: String
      let createdAt: Date
      let avatarURL: URL?
    }

A simple `UIView` subclass to display the comment.

    public final class CommentView: UIView {
      let titleLabel = UILabel()
      let subtitleLabel = UILabel()
      let statusLabel = UILabel()
      let replyButton = UIButton(type: .custom)
      let avatarImageView = UIImageView()
    } 

Now we get a little to the fun stuff.

We’ll make our first  `ViewData` protocol. This represents how we will render the data we’re trying to populate the `UIView` with.

    protocol CommentViewData {
      var title: String { get }
      var subtitle: String { get }
      var timestamp: String { get }
      var replyText: String { get }
      var avatarURL: URL? { get }
    }

Let’s conform our model to our `CommentViewData` protocol. This will be how we tell our `CommentView` how it should display our model whenever it comes across an instance of it.

    // The original data source is made to conform to the protocol which we are using for display, CommentViewData
    
    extension Comment: CommentViewData {
    
      var title: String {
        return self.commenter
      }
    
      var subtitle: String {
        return self.text
      }
        
      var replyText: String {
        return NSLocalizedString("Reply", comment: "Text for replying to a comment")
      }
    
      var replyImage: UIImage? {
        return UIImage(named: "reply")
      }
    
      var timestamp: String {
        return self.createdAt.timeAgoSinceNow
      }
    
    }

One thing to note is that the `avatarURL` property automatically conforms to the `CommentViewData`! As long as we plan to use it directly, we don’t have to add it to our extension.

Last but not least, we need to configure the `CommentView` with a `CommentViewData`.

    extension CommentView {
    
      func configure(viewData: CommentViewData) {
        self.titleLabel.text = viewData.title
        self.subtitleLabel.text = viewData.subtitle
        self.statusLabel.text = viewData.timestamp
        self.replyButton.setTitle(viewData.replyText, for: .normal)
        self.replyButton.setImage(viewData.replyImage, for: .normal)
        self.avatarImageView.setImage(from: viewData.avatarURL)
      }
    
    }

We’ve got everything configured in a nice declarative fashion, but how do we actually use this? This is in my opinion the best part. Let’s look at the call-site.

    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
      // My own homegrown solution, you're under no obligation to use it of course 😇
      let cell = tableView.dequeueReusableCell(forIndexPath: indexPath) as GenericTableCell<CommentView>
        
      // This is of type `Comment`
      let currentComment = self.comments[indexPath.row]
    
      // Comment conforms to `CommentViewData`, so we can use it directly!
      cell.customView.configure(viewData: currentComment)
    
      return cell
    }

And that’s it! All you need to do is pass the original model object to the view, and as long as it conforms to the right protocol, you’ve got it working without any intermediate objects.


----------

This may seem like a lot of boilerplate, and to be honest, it's more than I would like. There are other languages with features such as [row polymorphism](https://github.com/purescript/documentation/blob/a15f4e6b40e0a8dc874285526afe13f3074b6d26/language/Types.md#row-polymorphism) or [extensible records](https://medium.com/@ckoster22/advanced-types-in-elm-extensible-records-67e9d804030d) which would make this easier. Until Swift supports these language features, or macros, or more powerful tooling that can fill the gaps, this is the best solution I’ve found to enforcing good practices and leveraging compile-time safety for view configuration.


----------

Now you may also be thinking “sometimes my models don’t map to how they’re displayed one to one, how can I make that work?” Follow along with [part 2]({{ site.url }}/12/26/building-better-views-part-ii), where we'll cover that, and a few other questions you may have.

As always, I'm excited to hear your thoughts, and am receptive to [feedback](https://twitter.com/mergesort)!

