---
layout: post
title: Go for Objective-C developers
tags: [go, programming, iOS]
---

I’ve been doing Objective-C for almost 5 years (woo!), so at this point I think I have a better understanding than most of Apple’s motivations and intentions, with relation to building the language.

That said, recently I’ve been loving working with Go, and there’s a few reasons for that.

### Not traditionally object-oriented

With the rise of ReactiveCocoa, I’ve been thinking about what programming principles might work for UI-driven frameworks. Go is not traditionally Object-Oriented. You cannot inherit your `Cat` class from `Animal`, but you can anonymously embed an `Animal` into your `Cat`, so it gets all the traits of `Animal`. That’s because you don’t have objects, you have structs and interfaces. Interfaces are functions that act on structs. This doesn’t sound quite that different than OO methodologies, but it’s a big distinction when thinking about how to construct your software.

Gothic (go-like) programming seems like it would be a great style for people looking to explore signal-driven frameworks, which Go is great for.

### Type inference

```objective-c
UIView *view = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 480))]
```

I write that dozens of times per day when doing iOS development. In Go, it would look like this:

```go
view := UIView{CGRect{0, 0, 320, 480}}
```

Considering how often I write that, I would love type inference to clean up my code. Type inference is the biggest reason writing in Go feels like working with a scripting language.

### Garbage collection

Let me start off by saying, ARC is amazing. I think what Apple’s done with LLVM, and what it’s enabled is one of the best things I’ve seen in my short career. That said, not having to worry about ARC not cleaning up properly, or where to use a strong vs. weak reference does get tenuous. If software development is about reducing mental strain on a programmer, then garbage collection is something that goes a long way to that.

### Native concurrency

Go handles concurrency in a few ways. The simplest is to just stick the go keyword in front of your method, and it will run it asynchronously.

```go
doSomethingAwesome      // Runs synchronous 
go doSomethingAwesome   // Runs asynchronous
```

The second is channels. As an Objective-C developer you can think of channels similarly to `NSNotification`s. You pass values to a certain channel, and it responds accordingly, as you’ve set it up to respond. One nice thing is that unlike `NSNotification` it’s statically typed, because this mechanism is built into the Go language. Channels also can talk in both directions, so you can pass messages back and forth along a channel. package main

```go
import (
    "fmt" "time"
)

func main() { 
    ok := make(chan bool, 1)
    go doSomething(ok)
    fmt.Println("Waiting")
    <-ok
    fmt.Println("Did something") 
} 

func doSomething(ok chan bool) {
    time.Sleep(time.Second)
    ok <- true
}
```

I don’t know about you, but I’d much rather be doing concurrency this way rather than thinking about what thread to run a function on.

### Packages

One thing that Objective-C has struggled with for 30 years is namespaces. `JFMyClass`, `AFNYourClass`, `THOSomeOtherClass`! All this prefixing is done to avoid collisions. The accepted practice is to now prefix your classes with 3 letters, because that will solve everything obviously. If your implementation of a class has a method `doSomething`, and yours does as well, with Objective-C’s dynamic runtime there is no way to know when your version will be ran or mine will. Go solves that in the classic way, with packages. Packages can be built into static libraries, which get put into your go directory (where all libraries are stored on your computer).

### Go as a tool

Go has built terrific tooling into the language's standard offerings.

#### go get

`go get` fetches remote repositories and installs the packages and dependencies. In fact, you can even import from a url, like `import “github.com/go-sql-driver/mysql”` and have your MySQL driver ready to go when you compile your application.

#### go fmt

Isn’t it awful when you use BSD style brackets, and your coworker uses Allman, and you want to use K&R? Go only has one style. You run the `go fmt` tool, and it automagically converts all the brackets, new lines, and everything else to one standard go format. Most IDE’s have built in support which runs the go fmt tool when you save the file, so your code always looks right.

#### go test

Tests are built into the language. Tests live in the same package, so you don’t have to worry about exposing any variables just for your test cases’ sake.

#### go be happy!

This one is just my personal advice.

Go isn’t the world’s most perfect language, but it’s one of the biggest advancements for software development principles in a while. That’s why I’m excited about it, and I’d implore you all to try Go!

As usual, if you have any feedback feel free to leave a comment for me [@mergesort](https://www.twitter.com/mergesort) or on this Hacker News [thread](https://news.ycombinator.com/item?id=7226218).