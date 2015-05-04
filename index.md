---
layout: page
title: "A standard for building APIs in JSON."
show_masthead: true
---

If you've ever argued with your team about the way your JSON responses
should be formatted, JSON API is your anti-bikeshedding weapon.

By following shared conventions, you can increase productivity,
take advantage of generalized tooling, and focus on what
matters: your application.

Clients built around JSON API are able to take
advantage of its features around efficiently caching responses,
sometimes eliminating network requests entirely.

Here's an example response from a blog that implements JSON API:

```json
{
  "links": {
    "self": "http://example.com/posts",
    "next": "http://example.com/posts?page[offset]=2",
    "last": "http://example.com/posts?page[offset]=10"
  },
  "data": [{
    "type": "posts",
    "id": "1",
    "title": "JSON API paints my bikeshed!",
    "links": {
      "self": "http://example.com/posts/1",
      "author": {
        "self": "http://example.com/posts/1/links/author",
        "related": "http://example.com/posts/1/author",
        "linkage": { "type": "people", "id": "9" }
      },
      "comments": {
        "self": "http://example.com/posts/1/links/comments",
        "related": "http://example.com/posts/1/comments",
        "linkage": [
          { "type": "comments", "id": "5" },
          { "type": "comments", "id": "12" }
        ]
      }
    }
  }],
  "included": [{
    "type": "people",
    "id": "9",
    "first-name": "Dan",
    "last-name": "Gebhardt",
    "twitter": "dgeb",
    "links": {
      "self": "http://example.com/people/9"
    }
  }, {
    "type": "comments",
    "id": "5",
    "body": "First!",
    "links": {
      "self": "http://example.com/comments/5"
    }
  }, {
    "type": "comments",
    "id": "12",
    "body": "I like XML better",
    "links": {
      "self": "http://example.com/comments/12"
    }
  }]
}
```

The response above contains the first in a collection of "posts", as well as
links to subsequent members in that collection. It also contains resources
linked to the post, including its author and comments. Last but not least,
links are provided that can be used to fetch or update any of these
resources.

JSON API covers creating and updating resources as well, not just responses.
