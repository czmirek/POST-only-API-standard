# README

Hello all.

This is a for fun project aimed at creating a POST only API standard.

## Critique of the REST convention

**REST does not say anything about common topics related to API development.**

As far as conventions go there's not much else in what REST APIs offer for a common API developer. REST implementations vary considerably in practice (in my opinion and experience) because the convention does not go very far in standardizing common needs of common API developers such as:

- validations
- data filtering, paging, column sorting and column visibility
- versioning
- sane HTTP status code logic

**REST has constraints that API developers mostly ignore**.

The standard also, as far as I can tell, imposes some other constraints on APIs that in practice most developers ignore.

**Caching**

Using HTTP header `Cache-Control` you can alter behavior on how browsers cache your `GET` responses.

*"The goal of caching is never having to generate the same response twice."* [^1]

This requirement is normally ignored because:
- Caching should be considered only when we optimize things. And we should optimize things only when we find that our things don't run as fast as we want them to.
- Caching is a hard problem. How to cache? When to cache? What to cache? For how long? Do we need to reset the cache reactively? Or on timed manner? How is the cache stored?
- Utilizing `Cache-Control` can be just a single part of multilayered cache solution that utilizes the browser cache and/or the server cache.

**Hypermedia links**

Hypermedia links are references to URLs of other resources that are in some relation to the data you are returning.

This is an example from the site [What is REST?](https://restfulapi.net/)

```json
{
  "id": 123,
  "title": "What is REST",
  "content": "REST is an architectural style for building web services...",
  "published_at": "2023-11-04T14:30:00Z",
  "author": {
    "id": 456,
    "name": "John Doe",
    "profile_url": "https://example.com/authors/456" //---------- REST link
  },
  "comments": {
    "count": 5,
    "comments_url": "https://example.com/posts/123/comments" //-- REST link
  },
  "self": {
    "link": "https://example.com/posts/123" //------------------- REST link
  }
}
```

This is almost never implemented because it is **difficult** to implement for no benefit.
- Your API now depends on at least a single domain. This complicates architectures considerably. Can the domain change? Who's in charge of configuring this? What if the API is available from multiple hosts?
- You need some kind of mapping between your API endpoints and their URL representations. This complicates API code. Also how do you handle API versioning with this (e.g. when only the `comments` API is updated)?
- ...what is this for anyway? For example, why on earth would you ever need to utilize the `self:link`? Trying to build on this smells like a bad project architecture than anything else.

**HATEOAS**

According to [Wikipedia](https://en.wikipedia.org/wiki/HATEOAS): *With HATEOAS, a client interacts with a network application whose application servers provide information dynamically through hypermedia. A REST client needs little to no prior knowledge about how to interact with an application or server beyond a generic understanding of hypermedia.*

This is overengineering. No one in common commercial practice is building applications like that.
- It is very difficult to implement. You can either do this manually (`<sarcasm>`because that's what we developers love, do manual stuff`</sarcasm>`) or your API must have a great reflective knowledge about the resources and their relations.
- Clients are commonly hardwired to their APIs in practice because of UI/UX constraints.
- Independent clients depending only on a *generic understanding of hypermedia* means you cannot have meaningful UI/UX

**The REST convention is very old (2000)**

And from the time where we didn't know much about how IT projects and APIs are going to evolve.

## The standard!




[^1]: [Caching your REST API](https://restcookbook.com/Basics/caching/)
