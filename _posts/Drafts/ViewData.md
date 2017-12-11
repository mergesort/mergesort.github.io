# ViewData

As iOS developers, a lot of our daily work involves taking models from a server, and transforming them for display purposes on an iPhone or iPad. This sounds like a job for some declarative architecture. 🤔

https://twitter.com/mergesort/status/720706593982062592

Confession: I've never fully bought into MVVM. I don't think it's worse than MVC. I use View Models as a place to store state and actions for View Controllers, and preferably stateless functions for manipulating data. In my experience things become harder to maintain when they start becoming a crutch, as a place to put your code if it doesn't neatly fall into the Model, View, or Controller label.

With this in mind, I realized we need an answer for configuring our views in a way that's maintainable, and ultimately transforms a model (or models) into a view. This led me to the idea of `ViewData`. I started working on this with [@shengjundong](https://twitter.com/shengjundong) at Timehop, and have been using it successfully across apps of all sizes since.

There are 3 parts to this approach.
1) A UIView instance. This is your standard view that you'll be displaying in an app. It can be a regular class, or a custom subclass as you need.
2) A ViewData protocol. This is what's going to keep track of the data that needs to be displayed in your view. Most commonly this will be a slice of a model, used specifically for rendering the view.
3) A `configure(viewData: ViewData)` function. This is what's going to map your View to your ViewData.

A simple example of how ViewData would look, is this.

```swift 
// This is the protocol, representing all the data that should be displayed in the view.
protocol CommentViewData {

    var title: String { get }
    var subtitle: String { get }
    var timestamp: String { get }
    var replyText: String { get }
    var imageUrl: URL? { get }

}
```

```swift
// The original model, which we'll later be manipulating for display.
public struct Comment {

    public let text: String
    public let commenter: String
    public let createdAt: Date
    public let imageUrl: URL?
    public let indentationLevel: Int

}

```

```swift
// The original data source is made to conform to the protocol which we are using for display, CommentViewData.
extension Comment: CommentViewData {

    var title: String {
        return self.commenter
    }

    var subtitle: String {
        return self.text
    }

	 var replyText: String {
	     return "Reply".localized()
	 }

    var timestamp: String {
        return self.createdAt.timeAgoSinceNow
    }

    // The imageUrl property automatically conforms to the CommentViewData protocol, so we don't need to add anything here if we plan to use it directly.

}
```

```swift
// We configure the view, using the ViewData.
extension CommentView {

    func configure(viewData: CommentViewData) {
        self.titleLabel.text = viewData.title
        self.subtitleLabel.text = viewData.subtitle
        self.statusLabel.text = viewData.timestamp
        self.replyButton.setTitle(viewData.replyText for: .normal)
        self.avatarImageView.kf.setImage(with: viewData.imageUrl)
    }

}
```

```swift
// At our call-site, we use the comment which we were given, to configure the view.
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(forIndexPath: indexPath) as GenericTableCell<CommentView>

    let currentComment = self.comments[indexPath.row]
    cell.customView.configure(viewData: currentComment)

    return cell
}
```

Sometimes objects don't map to protocols 1 to 1, so instead we can construct a one-time use object, specifically for displaying in one place.

```swift
struct CourseProgressViewHomeScreenDisplay {
    let course: Course
    let enrollment: Enrollment
    let customization: SchoolCustomization
}
```

In this case, we need to display data about a course, and enrollment, and using the school's customized colors. We name the object with the pattern [View To Configure][Screen It's Displaying On][Display]. The example above is configuring the CourseProgressView on the HomeScreenViewController.
