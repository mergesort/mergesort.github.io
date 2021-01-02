---
layout: post
title: Context-Bound Types
tags: [programming, swift, featured]
---

I've been thinking about privacy lately. No, not [online](https://www.fabisevi.ch/2018/01/16/the-future-will-be-signed/) [privacy](https://www.fabisevi.ch/2019/01/01/pushing-the-boundaries-of-technology/), but about how APIs can balance exposing the right amount of implementation details without revealing too much.

I'll walk through a task I find myself doing often when building iOS apps, creating a view controller with header view, and four different ways to go about it.

----------

### Regular View Configured as a Header

*SettingsViewController.swift*

```
final class SettingsViewController: UIViewController {
    
    private let headerView = UIView()
    
    private let tableView = UITableView()
    
    override func viewDidLoad() {
        super.viewDidLoad()
    
        self.view.addSubview(self.tableView)
        self.setupTableView()
        self.configureHeaderView()
    }
    
    func setupTableView() {
        self.tableView.translatesAutoresizingMaskIntoConstraints = false
        NSLayoutConstraint.activate([
            self.tableView.leadingAnchor.constraint(equalTo: self.view.leadingAnchor),
            self.tableView.trailingAnchor.constraint(equalTo: self.view.trailingAnchor),
            self.tableView.topAnchor.constraint(equalTo: self.view.topAnchor),
            self.tableView.bottomAnchor.constraint(equalTo: self.view.bottomAnchor),
        ])
    }
    
    func configureHeaderView() {
        // Some code configuring self.headerView
        // ...
        // ...
        self.tableView.tableHeaderView = self.headerView
    }

}
```

For folks new to iOS development, this is a common approach I see when adding a header. It makes sense, you want to have a header, and a header is a view, so why not configure and style  `UIView` to be the  `UITableView` header. While this is a good first try, it lacks the encapsulation that makes your code easy to edit and reason about.

----------

### Separate Class For The Header

*SettingsViewController.swift*

```
final class SettingsViewController: UIViewController {
    
    private let headerView = SettingsTableHeaderView()
    
    private let tableView = UITableView()
    
    override func viewDidLoad() {
        super.viewDidLoad()
    
        self.view.addSubview(self.tableView)
        self.setupTableView()
    
        self.tableView.tableHeaderView = self.headerView
    }
}
```

*SettingsTableHeaderView.swift*

```
final class SettingsTableHeaderView: UIView {
    // Some code creating and configuring SettingsTableHeaderView
    // ...
    // ...
}
```

A naive approach to improve our readability would have been to move our configuration code into a function, but an even nicer improvement is to move it into its own class. This looks a lot better, it's easier to reason about and it's well-encapsulated. But a new problem this introduces is adding `SettingsTableHeaderView` into our module’s namespace. Now I'll admit this isn't the world's biggest problem, but as you start adding different view controllers with different headers, suddenly finding the right header view for a given view controller becomes difficult.

----------

### Private Class for the Header

*SettingsViewController.swift*

```
final class SettingsViewController: UIViewController {
    
    private let headerView = HeaderView()
    
    private let tableView = UITableView()
    
    override func viewDidLoad() {
        super.viewDidLoad()
    
        self.view.addSubview(self.tableView)
        self.setupTableView()
    
        self.tableView.tableHeaderView = self.headerView
    }
    
    private final class HeaderView: UIView {
      // Some code creating and configuring SettingsViewController.HeaderView
      // ...
      // ...
    }
    
}
```

Now this is a solution that I'm really liking. We've moved `SettingsTableHeaderView` out of our module’s namespace and into one dependent on the context it's in,  `SettingsViewController`. When referring to  `SettingsViewController.HeaderView` inside of this class we can plainly refer to it as `HeaderView`, which is not only less verbose, but emphasizes the pairing between  `HeaderView` and  `SettingsViewController`. 

There is a downside to this approach though, the more views we add to  `SettingsViewController`, the harder this file becomes to parse. Now again this may not seem like a big problem, but if you have a well encapsulated view, you may have many subviews that belong to either `SettingsViewController` or `HeaderView`, and your file can get pretty large. (Trust me, I’ve ~~seen~~ written some pretty large files.)

----------

### Two Files with Namespaced Internal Classes

*SettingsViewController.swift*

```
final class SettingsViewController: UIViewController {
    
    private let headerView = HeaderView()
    
    private let tableView = UITableView()
    
    override func viewDidLoad() {
        super.viewDidLoad()
    
        self.view.addSubview(self.tableView)
        self.setupTableView()
    
        self.tableView.tableHeaderView = self.headerView
    }

}
```    

*SettingsViewController.HeaderView.swift*

```
extension SettingsViewController {
    
    final class HeaderView: UIView {
      // Some code creating and configuring SettingsViewController.HeaderView
      // ...
      // ... 
    }
    
}
```

This is the approach I've settled on today. You'll notice that  `HeaderView` is no longer private, but it's also not particularly easy to access publicly. You still end up with the benefits from namespacing the API, and this extension can go into its own file, unlike the earlier approach.

If you were to accidentally misuse this API, it would be pretty clear. When calling  `HeaderView` inside of  `SettingsViewController` the call-site is clean and simple. But if someone were to attempt to use it from another class, they would have to reference the fully-qualified type,  `SettingsViewController.HeaderView`.

----------

While I’ve walked through one example with four approaches, binding a type to its context is something you can do throughout a codebase. In an ideal world Swift would have a `submodule` keyword to make types less ambiguous, but in the mean time this is a reasonable substitute that developers can take advantage of. While we don’t have a `submodule` keyword, we have a close approximation by using empty enums. One notable example is Combine’s usage of [Publishers](https://developer.apple.com/documentation/combine/publishers) and [Subscribers](https://developer.apple.com/documentation/combine/subscribers/) to help people have context and understanding for their subtypes.

As always, I’d love to know what you think or if you’ve come up with better solutions, so please don’t be shy about [reaching out](https://twitter.com/mergesort).

----------

Special shoutout to [Jasdev](https://twitter.com/jasdev) for taking a *very rough* first draft and helping me turn it into something coherent.