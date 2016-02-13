# GSS Freight API

Freight API provides programmatic access to GSS functionality and content.

The API is [REST API](http:/en.wikipedia.org/wiki/Representational_State_Transfer "RESTful") and uses single token key authentication.
Currently, return format for all endpoints is [JSON](http:/json.org/ "JSON").


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

- **[C# Sample](https://github.com/gosweetspot/freight-api-csharp-sample)**

## Endpoints

#### Publish Orders

- **[<code>GET</code> v2/pendingorders](https://github.com/gosweetspot/freight-api/blob/master/v2/GET_pendingorders.md)**
- **[<code>GET</code> v2/order](https://github.com/gosweetspot/freight-api/blob/master/v2/GET_order.md)**
- **[<code>POST</code> v2/neworder](https://github.com/gosweetspot/freight-api/blob/master/v2/POST_neworder.md)**
- **[<code>POST</code> v2/neworders](https://github.com/gosweetspot/freight-api/blob/master/v2/POST_neworders.md)**

### Rates Query

- **[<code>POST</code> ratesquery/availablerates](https://github.com/gosweetspot/freight-api/blob/master/ratesqueryv1/POST_availablerates.md)**

### Create and Print Shipments

- **[<code>POST</code> ratesquery/printcheapestcourier](https://github.com/gosweetspot/freight-api/blob/master/ratesqueryv1/POST_printcheapestcourier.md)**
- **[<code>POST</code> ratesquery/createandprint](https://github.com/gosweetspot/freight-api/blob/master/ratesqueryv1/POST_createandprint.md)**
- **[<code>POST</code> v2/publishmanifest](https://github.com/gosweetspot/freight-api/blob/master/v2/POST_publishmanifest.md)**
- **[<code>POST</code> ratesquery/reprint](https://github.com/gosweetspot/freight-api/blob/master/ratesqueryv1/POST_reprint.md)**
- **[<code>POST</code> v2/deleteconnote](https://github.com/gosweetspot/freight-api/blob/master/v2/POST_deleteconnote.md)**
- **[<code>GET</code> labels/download](https://github.com/gosweetspot/freight-api/blob/master/labels/GET_download.md)**

### Tracking

- **[<code>POST</code> v2/shipmentstatus](https://github.com/gosweetspot/freight-api/blob/master/v2/POST_ShipmentStatus.md)**

## FAQ

### How do I connect to the API?
The API is only available to authenticated clients. Clients should authenticate users using [access_key]. Once authenticated, you need to request a resource from one of the endpoints using HTTP. Generally, reading any data is done through a request with GET method.

### What return formats do you support?
Freight API currently returns data in [JSON](http:/json.org/ "JSON") format.  Some methods may return [XML] data, however we don't actively test for XML compatibility.

### What kind of authentication is required?
Applications must identify themselves to access any resource.
You need to contact your account manager to obtain a test access key.
Every request requires a http header property *ACCESS_KEY*, as well as *SUPPORT_EMAIL*. The Support Email should contain the IT Level contact for the organisation. This will be used to contacting you, should we find your requests need attention.

### Is there a request rate limit?
Presently there is no rate limiting on the api. We however reserve the right to enforce limits or block calls at our discretion.

### Shoud I crack on?
Sure, fire away, however, we do suggest you talk to us, prior to starting so we can understand your requirements and explain how best to use this api.
