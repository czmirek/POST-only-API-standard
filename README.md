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

> The goal of caching is never having to generate the same response twice. [^3]

This is normally ignored because:
- Caching should be considered only when we optimize things. We should optimize things only when we find that our things don't run as fast as we want them to.
- Caching is a hard problem. How to cache? When to cache? What to cache? Utilizing `Cache-Control` is one of many solutions. You can cache in the browser, on server





- HTTP is already stateless so the *statelessness of REST* is not really a thing.
- Context dependent HTTP request is impossible to qualify.  


- It's a completely arbitrary convention over how HTTP should be used
- The REST API convention does not identify solutions to common pitfals when building APIs such as how to handle validations, server errors, 
- 





## The standard

[^1]: [2023 State of the API Report](https://www.postman.com/state-of-api/api-technologies/#:~:text=While%20REST%20remains%20the%20most,and%2092%25%20the%20year%20prior.)
[^2]: [How to understand "RESTful API is stateless"?](https://stackoverflow.com/questions/34130036/how-to-understand-restful-api-is-stateless)
[^3:] [Caching your REST API](https://restcookbook.com/Basics/caching/)
