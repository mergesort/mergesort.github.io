---
layout: post
title: Debugging shortcuts for UIKeyCommand
tags: [swift, programming, iOS]
---

I recently re-discovered `UIKeyCommand` while listening to [Caleb Davenport](undefined)’s, [podcast](https://overcast.fm/+GuhgtcBa4), Runtime. He’s also got a [blog post](https://calebd.me/posts/uikeycommand) which shows you exactly how simple it is to create `UIKeyCommand` shortcuts for your app.

After reading that, I decided that it would be neat to implement them across my app, so I could also start navigating around my UI with lightning speed while I’m debugging in the simulator. I quickly realized that by using Swift extensions, I could automatically get these behaviors for free throughout our entire app.

Below is a code snippet which you can drop into your app to help you speed up your workflow. With just one tap on your keyboard, you’ll be able to pop a UIViewController from a navigation stack and dismiss any presented `UIViewController`.

```swift
extension UIViewController {

    open override var keyCommands: [UIKeyCommand]? {
        return [
            UIKeyCommand(input: UIKeyInputLeftArrow, modifierFlags: [], action: #selector(popViewControllerWithKeyCommand)),
            UIKeyCommand(input: UIKeyInputDownArrow, modifierFlags: [], action: #selector(dismissViewControllerWithKeyCommand)),
        ]
    }

}

private extension UIViewController {

    dynamic func popViewControllerWithKeyCommand() {
        self.navigationController?.popViewController(animated: true)
    }

    dynamic func dismissViewControllerWithKeyCommand() {
        self.dismiss(animated: true, completion: nil)
    }

}
```

Don’t forget, you can make your own default shortcuts too.

**Happy debugging!**