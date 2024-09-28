# README

Hello all.

This is a for fun project aimed at creating a sensible POST only API standard.

## Critique of the REST convention

🤨 **REST does not say anything about common topics related to API development.**

As far as conventions go there's not much else in what REST APIs offer for a common API developer. REST implementations vary considerably in practice (in my opinion and experience) because the convention does not go very far in standardizing common needs of common API developers such as:

- validations
- data filtering, paging, column sorting and column visibility
- versioning
- sane HTTP status code logic

🤨 **Caching**

Using HTTP header `Cache-Control` you can alter behavior on how browsers cache your `GET` responses.

*"The goal of caching is never having to generate the same response twice."* [^1]

This requirement is normally ignored because:
- Caching should be considered only when we optimize things. And we should optimize things only when we find that our things don't run as fast as we want them to.
- Caching is a hard problem. How to cache? When to cache? What to cache? For how long? Do we need to reset the cache reactively? Or on timed manner? How is the cache stored?
- Utilizing `Cache-Control` can be just a single part of multilayered cache solution that utilizes the browser cache and/or the server cache.

🤨 **Hypermedia links**

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

🤨 **HATEOAS**

According to [Wikipedia](https://en.wikipedia.org/wiki/HATEOAS): *With HATEOAS, a client interacts with a network application whose application servers provide information dynamically through hypermedia. A REST client needs little to no prior knowledge about how to interact with an application or server beyond a generic understanding of hypermedia.*

- This is overengineering. No one in common commercial practice is building applications like that.
- It is difficult to implement. You can either do this manually (`<sarcasm>`*because that's what we developers love, do manual stuff*`</sarcasm>`) or you must implement something for the reflective knowledge about the resources and their relations.
- Clients are commonly hardwired to their APIs in practice because of UI/UX constraints.
- Independent clients depending only on a *generic understanding of hypermedia* means you cannot have meaningful UI/UX

🤨 **The REST convention is very old (2000)**

And from the time where we didn't know much about how IT projects and APIs are going to evolve.

🤨 **[Richardson maturity model](https://en.wikipedia.org/wiki/Richardson_Maturity_Model) is pure bullshit (and also old (2008))**

So according to someone named *Leanord Richardson* the REST convention is so important that there are official **maturity models** to it.

Short version so you don't have to read the Wikipedia article

- Level 0 = one HTTP endpoint equals to multiple functions.
  - For example, you send a POST over for `/bookings` and for creating booking you send `{ "operationId": "createBooking" ...}`, for updating the booking you send `{ "operationId": "updateBooking" ...}`
- Level 1 = one HTTP endpoint equals to a single function (e.g. `/bookings/createBooking`, `/bookings/updateBooking` etc.)
- Level 2 = you use HTTP verbs as defined by REST e.g. `GET` for reading resources, `POST` to update resources, `PUT` to create resources, etc.
- Level 3 = you use HATEOAS

This is complete nonsense built on ideas of another nonsense. I've seen it personally being promoted in corporations by IT architects with no knowledge in programming.

## Identifying the needs for common API developers

## Philosophy of the POST only API standard

## The standard itself! (finally)


[^1]: [Caching your REST API](https://restcookbook.com/Basics/caching/)
