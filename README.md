# GSS Freight API

Freight API provides programmatic access to GSS functionality and content.

The API is [REST API](http://en.wikipedia.org/wiki/Representational_State_Transfer "RESTful")
and uses single token key authentication.
Currently, return format for all endpoints is [JSON](http://json.org/ "JSON").


***

## Checklist
* You need a GSS access token
* Familiarize yourself with API functionality
* Hack away

***

## Changes

* 2014-03-27 Deprecated photo object's image_url key.

## SDK

- **[C#](https://github.com/500px/500px-js-sdk)**

## Endpoints


#### Publish Orders

- **[<code>POST</code> comments/:id/comments](https://github.com/500px/api-documentation/blob/master/endpoints/comments/POST_comments_id_comments.md)**

## Rates Query

- **[<code>POST</code> oauth/request_token](https://github.com/500px/api-documentation/blob/master/authentication/POST_oauth_requesttoken.md)**
- **[<code>POST</code> oauth/authorize](https://github.com/500px/api-documentation/blob/master/authentication/POST_oauth_authorize.md)**
 
## Create and Print Shipments

- **[<code>POST</code> oauth/access_token](https://github.com/500px/api-documentation/blob/master/authentication/POST_oauth_accesstoken.md)**
- **[Upload key](https://github.com/500px/api-documentation/blob/master/authentication/upload_key.md)**


## FAQ
### What do I need to know before I start using the API?
Got rust on your skills? No worries. Here are the docs you might need to get started:

- HTTPS protocol
- [REST software pattern][]
- Authentication with [OAuth][] (or the official [Beginner’s Guide][])
- Data serialization with [JSON][] (or see a [quick tutorial][])

### How do I connect to the 500px.com API?
The API is only available to authenticated clients. Clients should authenticate users using [OAuth][]. Once authenticated, you need to request a resource from one of the endpoints using HTTPS. Generally, reading any data is done through a request with GET method. If you want our server to create, update or delete a given resource, POST or PUT methods are required.

### What return formats do you support?
Freight API currently returns data in [JSON](http://json.org/ "JSON") format.

### What kind of authentication is required?
Applications must identify themselves to access any resource.
You need to contact your account manager to obtain a test access key.

### Is there a request rate limit?
Presently there is no rate limiting on the api. We however reserve the right to enforce limits or block calls at our discretion.


[REST software pattern]: http://en.wikipedia.org/wiki/Representational_State_Transfer
[JSON]: http://json.org
[quick tutorial]: http://www.webmonkey.com/2010/02/get_started_with_json/
https://github.com/500px/api-documentation#what-do-i-need-to-know-before-i-start-using-the-api

