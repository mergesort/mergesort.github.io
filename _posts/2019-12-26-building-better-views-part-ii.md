---
layout: post
title: Building Better Views (Part II), Next Steps
tags: [programming, swift]
---

If you haven't checked out [Part I]({{ site.url }}/12/26/building-better-views-part-i), I recommend reading it because if you don't, none of writing below will make sense!

## Three Unanswered Questions

#### 1. What happens when the views you want to configure are more complex?

My recommended approach is to construct a one-time use struct, specifically for displaying in that one place. This type should only have the properties you need to render the view.


    struct HomeScreenCourseProgressViewDisplay {
        let course: Course
        let enrollment: Enrollment
        let customization: SchoolCustomization
    }

Creating the `ViewData` should look familiar. We're going to do the exact same thing we did before.

    extension HomeScreenCourseProgressViewDisplay: CourseProgressViewData {
    
      var titleLabelText: String {
        return self.course.name
      }
    
      var subtitleLabelText: String {
        return self.course.author.name
      }
    
      var statusLabelText: String {
      // FIX THIS SYNTAX
        return NSLocalizedString("%@ complete", "The percentage a course is complete")
        return "\(self.enrollment.percentComplete)% \("complete".localized())"
      }
    
      var progress: CGFloat {
        return CGFloat(self.enrollment.percentComplete) / 100
      }
    
      var imageUrl: URL? {
        return self.course.imageUrl
      }
    
    }

Using this `ViewData` object is just as simple as it was before. On our home screen, we now create the struct, and configure our custom view with it. Same as before, just leveraging how lightweight creating types in Swift is!

    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
      guard let currentUser = self.userAtIndexPath(indexPath: indexPath), self.hasCoursesAtIndexPath(indexPath: indexPath) else { fatalError("Ruh roh"!) }
    
      let currentCourse = currentUser.courses[indexPath.row]
      let currentEnrollment = currentUser.enrollments[indexPath.row]
      let schoolCustomization = currentUser.school.customization
    
      let homeScreenDisplay = HomeScreenCourseProgressViewDisplay(
        course: currentCourse, 
        enrollment: currentEnrollment, 
        customization: schoolCustomization
      )
    
      cell.customView.configure(viewData: homeScreenDisplay)
    
      return cell
    }


#### 2. How does the `ViewData` pattern deal with user interaction?

I advise keeping user actions in the `UIView` realm. You can continue using the delegate pattern, closures, or wherever your preferences may lie. If you’re looking to get a little more advanced, I’d consider reading Dave DeLong’s [A Better MVC](https://davedelong.com/blog/2017/11/06/a-better-mvc-part-1-the-problems/) series.


#### 3. Where does logic code reside, and what happens if you have more complex transformations?

The scenarios so far have worked great. The models you received from the server looked a lot like the way you plan to display them, but that's not always the case. Sometimes you're going to need business logic, and that's ok.

This is the question I had the most trouble coming up with one answer for. I realized the reason I couldn't come up with one answer is because there isn't only one answer.

Looking back at our `Comment` model, we see that there is a `Date` object in there.

    public struct Comment {
      let text: String
      let commenter: String
      let createdAt: Date
      let imageUrl: URL?
    }

In our first example we simply glossed over the fact that we were translating a `Date` into a `String`, by using a simple function that already exists in a third party library.

    extension Comment: CommentViewData {
    
      var timestamp: String {
        return self.createdAt.timeAgoSinceNow
      }
    
    }

But now let's pretend we don't have `timeAgoSinceNow` available to us. Where does that transformation code live? The answer is, it's up to you!

Some people prefer to make an object to handle business logic, to make their code more testable. If it makes you happy to keep it in the `ViewData` file, go right ahead. If not, then don't. Who am I to tell people how to be happy?

    extension Comment: CommentViewData {
    
      var timestamp: String {
        let dateTransformer = DateTransformer(self.createdAt)
        return dateTransformer.asString()
      }
    
      private static func transformDateToString(date: Date) -> String {
        return someMagicalWayToTransformDatesToStrings()
      }
    }
    
    struct DateTransformer {
    
      let date: Date
    
      func asString() -> Date {
        return someMagicalDateTransformer()
      }
    
    }

My personal preference is to use private static functions, keeping in tune with the functional nature of this approach.

    extension Comment: CommentViewData {
    
      var timestamp: String {
        return transformDateToString(self.createdAt)
      }
    
    }
    
    private extension Comment {
    
      static func transformDateToString(date: Date) -> String {
        return someMagicalDateTransformer()
      }
     
    }

The important thing to note is that when it comes to business logic, you have the agency to structure your codebase however you'd like. The `ViewData` pattern isn't prohibitive or prescriptive, it's just there to aid you in transforming models into views.

----------

These are the big questions I've received while using this pattern over the last few years. I'm excited to hear your thoughts, and am always receptive to [feedback](https://twitter.com/mergesort)!

