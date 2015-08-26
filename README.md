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
* If you system has more then one company utilising it, it is strongly recommended to not hardcode the access key and the api url

## SDK

- **[C# Sample](https://github.com/gosweetspot/freight-api-csharp-sample)**

## Endpoints

#### Customer Orders

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

### Shipments
- **[<code>GET</code> /api/shipments](https://github.com/gosweetspot/freight-api/blob/master/shipments/get.md)** returns all shipments filtered by date, number, etc

### Printing
- **[<code>GET</code> /api/printers](https://github.com/gosweetspot/freight-api/blob/master/printers/get.md)** returns a list of available printers

- **[<code>GET</code> /api/labels](https://github.com/gosweetspot/freight-api/blob/master/labels/get.md)** download the labels as png or pdf

- **[<code>POST</code> /api/labels](https://github.com/gosweetspot/freight-api/blob/master/labels/post.md)** enqueues the supplied shipment for printing

- **[<code>POST</code> /api/labels/enqueue](https://github.com/gosweetspot/freight-api/blob/master/labels/enqueue.md)** enqueues a raw image into the print queue for printing


## SOME COMMON USE CASES
### You have a custom bespoke e-commerce or orders platform
Your site does not allow external systems to feed information into it directly.
Your approach will be to publish orders to GSS once the orders are ready for dispatch/labelling. On the GSS system your user would process the order.
At some stage your system will request the order status update from GSS.
The api interactions would be:
1. **[<code>POST</code> v2/neworder](https://github.com/gosweetspot/freight-api/blob/master/v2/POST_neworder.md)** - triggered from your site when order is ready for ticketting
2. Using the GSS web portal, your dispatcher tickets the goods.
3. **[<code>GET</code> v2/order](https://github.com/gosweetspot/freight-api/blob/master/v2/GET_order.md)** - triggered by your system every 6 hours, to get status update on the order published earlier.

### You have a very specialised dispatch workflow
You might have a special requirement to integrate the ticketing directly into your existing system.  Using a external system to do one part of the workflow may affect performance and may not be acceptable.  You can use the GSS api to build the ticketing into your system.
The api interactions would be:
1. **[<code>POST</code> ratesquery/availablerates](https://github.com/gosweetspot/freight-api/blob/master/ratesqueryv1/POST_availablerates.md)** - your system at dispatch, calls the api to get all available freight options and rates
2. **[<code>POST</code> ratesquery/createandprint](https://github.com/gosweetspot/freight-api/blob/master/ratesqueryv1/POST_createandprint.md)** - the dispatcher reviews the freight options from (1) and makes a selection. A second call to generate the shipment is triggered.

### You use an open source platform
A lot of open source systems, also have a open api platform that GSS is able to tap into to build the integration directly from within GSS. We would consider any platform that our customers are using.  However depending on platform popularity the implementation time frames would be considered.  In the case that there are very few users on the platform, it may not be a sufficient business case for us to undertake the integration.

### Others
Surely there will be other cases that the api can be applied to.  Talk to us, and we will be able to help.


## FAQ

### How do I connect to the API?
The API is only available to authenticated clients. Clients should authenticate users using [access_key]. Once authenticated, you need to request a resource from one of the endpoints using HTTP. Generally, reading any data is done through a request with GET method.

### What return formats do you support?
Freight API currently returns data in [JSON](http:/json.org/ "JSON") format.  Some methods may return [XML] data, however we don't actively test for XML compatibility.

### What kind of authentication is required?
Applications must identify themselves to access any resource.
You need to contact your account manager to obtain a test access key.

### Is there a request rate limit?
Presently there is no rate limiting on the api. We however reserve the right to enforce limits or block calls at our discretion.  We request that you limit your requests to 60 calls per minute. If you expect to call at a higher rates, please contact us.

### Should I crack on?
Sure, fire away, however, we do suggest you talk to us, prior to starting so we can understand your requirements and explain how best to use this api.
