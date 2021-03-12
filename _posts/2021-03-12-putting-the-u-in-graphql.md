---
layout: post
title: Putting the U in GraphQL
tags: [swift, programming, featured]
---

GraphQL has been on my list of technologies to learn for a few months now, and last week I came across [Majid Jabrayilov's post](https://swiftwithmajid.com/2021/02/24/graphql-in-swift/), feeling pretty excited to tackle the subject. The post was very good, but it didn't answer the one question I've had as I've gone through numerous exercises to understand GraphQL, how do I make GraphQL requests without a library?

I've read about how to create a GraphQL query and how to integrate GraphQL on your server a dozen times, but one topic that's highly under-covered is how to make a GraphQL request from the client. In the world of GraphQL it's very common to reach for [Apollo](https://www.apollographql.com), a library that handles turning GraphQL queries into functions, leveraging tooling to turn those functions into type-safe API requests the client can make.

While this is a perfectly reasonable approach, and actually a pretty good developer experience, it still didn't answer the questions I had as an ever-curious engineer, how would I do this on my own?

I broke the problem I saw down into two smaller problems, request-generation and request-making. Generating a request, especially in Swift, it turns out is pretty easy. I really like the approach that [SociableWeaver](https://github.com/NicholasBellucci/SociableWeaver) takes, leveraging Swift's function builders to let you build a type-safe directly in Swift. The second problem was a bit fiddlier. I knew that I had to make a `POST` request, and I knew the endpoint that was being hit, and through some trial and error (along a friend's help[^1]), I was able to start making GraphQL requests without any external libraries needed.

```swift
extension URLSession {

    func graphQLRequest(url: URL, query: String) -> URLSession.DataTaskPublisher {
        var request = URLRequest(url: url)
        request.httpMethod = "POST"
        request.addValue("application/json", forHTTPHeaderField: "Content-Type")

        let body =
        """
            { "query": "\(query)" }
        """
        let queryData = body.data(using: .utf8)
        request.httpBody = queryData

        return self.dataTaskPublisher(for: request)
    }

    // If using SociableWeaver or a similar GraphQL query generator, you can do it in a type-safe manner.
    func graphQLRequest(url: URL, query: Weave) -> URLSession.DataTaskPublisher {
        return self.executeGraphQLQuery(url: url, query: query.description)
    }

}
```

After looking over the above code a few times I realized that the majority of it was handling the creation of a `URLRequest`. That served as a hint to me that we could refactor the code into a custom `URLRequest` initializer. This would be less prescriptive about how the `URLRequest` is used, since my first code snippet assumes you always want to return a `URLSession.DataTaskPublisher`.

```swift
extension URLRequest {

    init(url: URL, graphQLQuery query: String) {
        self.init(url: url)

        self.httpMethod = "POST"
        self.addValue("application/json", forHTTPHeaderField: "Content-Type")

        let body =
        """
            { "query": "\(query)" }
        """
        let queryData = body.data(using: .utf8)
        self.httpBody = queryData
    }
    
    // If we're going all in on SociableWeaver we can make a similar initializer that takes a `Weave` parameter instead of a `String`.

}
```

Now if you'd like to use `URLSession.DataTaskPublisher` you're free to by creating a `URLRequest` from our new initializer and using it, but you can also return a `URLSession.DataTask` or any other reason mechanism that involves a `URLRequest`.

```swift
extension URLSession {

    func graphQLRequest(url: URL, query: String) -> URLSession.DataTaskPublisher {
        let request = URLRequest(url: url, graphQLQuery: query)
        return self.dataTaskPublisher(for: request)
    }

    func graphQLRequest(url: URL, query: Weave) -> URLSession.DataTaskPublisher {
        return self.graphQLRequest(url: url, query: query.description)
    }

}
```

That looks a lot cleaner, and our responsibilities seem a lot more well-divided.

---

![A text message saying "Take that multi-million dollar company, not gonna use your so called library."]({{ site.url }}/assets/img/not-using-apollo.jpg)

Is there room for tools like Apollo? Absolutely! I'm not going to pretend that my dozen lines of code replaces the value that a multimillion dollar company provides. (I'll only make sick jokes about it.) But before importing a library like Apollo, any library really, it's worth asking yourself whether you need a big solution for a small probelm. Or maybe question the better question to ask before that is, have you really understood the problem you're trying to solve?

Perhaps the best question to ask though is, where exactly should we put the U in GraphQL?

[^1]: Special thanks to [Dave DeLong](https://twitter.com/davedelong) for his debugging prowess.