# README

Hello all.

This is a for fun project aimed at creating a POST only API standard.

## Critique of the REST convention

REST convention is a defacto today's standard for building APIs. [^1] It focuses on considering URL paths as *resources*, utilizing the URLs and HTTP verbs to either read (`GET`), create (`POST`), modify (`PUT`), partially modify (`PATCH`) or delete (`DELETE`) the data behind.

### REST does not say anything about common topics related to API development

However as far as conventions go there's not much else in what REST APIs offer for a common API developer. REST implementations vary considerably in practice (in my opinion and experience) because the convention does not go very far in standardizing common needs of common API developers such as:

- validations
- data filtering, paging, column sorting and column visibility

### REST has constraints that API developers mostly ignore
The standard also, as far as I can tell, imposes some other constraints on APIs that in practice most developers ignore.

Namely:

#### Caching

Using HTTP header `Cache-Control` you can alter behavior on how browsers cache your `GET` responses.

*"The goal of caching is never having to generate the same response twice."* [^3]

This requirement is normally ignored because:
- Caching should be considered only when we optimize things. And we should optimize things only when we find that our things don't run as fast as we want them to.
- Caching is a hard problem. How to cache? When to cache? What to cache? For how long? Do we need to reset the cache reactively? Or on timed manner? How is the cache stored?
- Utilizing `Cache-Control` can be just a single part of multilayered cache solution that utilizes the browser cache and/or the server cache.

#### Hypermedia links

Hypermedia links are references to URLs of other resources that are in some relation to the data you are returning.

This is the example on the site [What is REST?](https://restfulapi.net/)

json
```
{
  "id": 123,
  "title": "What is REST",
  "content": "REST is an architectural style for building web services...",
  "published_at": "2023-11-04T14:30:00Z",
  "author": {
    "id": 456,
    "name": "John Doe",
    "profile_url": "https://example.com/authors/456" <----------- REST link
  },
  "comments": {
    "count": 5,
    "comments_url": "https://example.com/posts/123/comments" <--- REST link
  },
  "self": {
    "link": "https://example.com/posts/123" <-------------------- REST link
  }
}
```






## The standard

[^1]: [2023 State of the API Report](https://www.postman.com/state-of-api/api-technologies/#:~:text=While%20REST%20remains%20the%20most,and%2092%25%20the%20year%20prior.)
[^2]: [How to understand "RESTful API is stateless"?](https://stackoverflow.com/questions/34130036/how-to-understand-restful-api-is-stateless)
[^3:] [Caching your REST API](https://restcookbook.com/Basics/caching/)
