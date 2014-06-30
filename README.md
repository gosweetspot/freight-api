# GSS Freight API

Freight API provides programmatic access to GSS functionality and content.

The API is [REST API](http://en.wikipedia.org/wiki/Representational_State_Transfer "RESTful") and uses single token key authentication.
Currently, return format for all endpoints is [JSON](http://json.org/ "JSON").


***

## Checklist
* You need a GSS access token
* Familiarize yourself with API functionality
* Hack away

***

## Things you should know

* Ensure you calls to the api are capable of handling errors and downtime
* Fields may be added to the endpoints are any time, ensure you conversions are capable of handling this
* Fields names are not case sensitive

## SDK

- **[C# Sample](https://github.com/gosweetspot/freight-api-c#-sample)**

## Endpoints

#### Publish Orders

- **[<code>GET</code> v2/pendingorders](https://github.com/gossweetspot/freight-api/pendingorders/GET_pendingorders.md)**

### Rates Query

- **[<code>POST</code> oauth/request_token](https://github.com/500px/api-documentation/blob/master/authentication/POST_oauth_requesttoken.md)**
- **[<code>POST</code> oauth/authorize](https://github.com/500px/api-documentation/blob/master/authentication/POST_oauth_authorize.md)**
 
### Create and Print Shipments

- **[<code>POST</code> oauth/access_token](https://github.com/500px/api-documentation/blob/master/authentication/POST_oauth_accesstoken.md)**


## FAQ
### What do I need to know before I start using the API?
Got rust on your skills? No worries. Here are the docs you might need to get started:

- HTTPS protocol
- [REST software pattern][]
- Data serialization with [JSON][] (or see a [quick tutorial][])

### How do I connect to the API?
The API is only available to authenticated clients. Clients should authenticate users using [access_key]. Once authenticated, you need to request a resource from one of the endpoints using HTTP. Generally, reading any data is done through a request with GET method.

### What return formats do you support?
Freight API currently returns data in [JSON](http://json.org/ "JSON") format.  Some methods may return [XML] data, however we don't actively test for XML compatibility.

### What kind of authentication is required?
Applications must identify themselves to access any resource.
You need to contact your account manager to obtain a test access key.

### Is there a request rate limit?
Presently there is no rate limiting on the api. We however reserve the right to enforce limits or block calls at our discretion.
