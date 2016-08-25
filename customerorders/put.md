# Submit New Customer Order Batched

    PUT api/customerorders

## Description
Saves a new orders or updates a pending order. If the packing slip number has already been processed, the message will be ignored.

This method will accept orders as a array.

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters

The body of the message should be sent as an JSON array.

- **packingslipno** - Specify the unique order number from your source system, that was used as the packing slip no when the order was published
- **consignee** - recepient name
- **address1** - address line 1, eg, building identifier, like Level 1, Fisher House, etc.
- **address2** - address line 2, street name
- **suburb** - suburb name
- **city** - city name or state name. Depending on destination country, if state information is available, this should be the abbreviated state code
- **postcode** - post code, for NZ addresses, this can be left blank if unknown.
- **country** - ISO Alpha 2 country code, eg NZ, AU, US, UK, CN
- **delvref** - Order number, or customer reference for this order.
- **delvinstructions** - Any specific instructions to be printed on the label.
- **contactname** - name of person, optional.
- **contactphone** - phone number of person, optional.
- **email** - email address for track & trace email, optional.

***

## Return format
JSON object array per order with *true* for a successfult submit or *false* for an ignored submit

***

## Errors
None

***

## Example
**Request**

    http://api.gosweetspot.com/api/customerorders

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8



*Body*
``` json
[
  {
    "packingslipno": "test1-14-07-01",
    "consignee": "Test 1",
    "address1": "1 Queens Street",
    "address2": "",
    "suburb": "Auckland Central",
    "city": "Auckland",
    "postcode": "",
    "country": null,
    "delvref": null,
    "delvinstructions": null,
    "contactname": null,
    "contactphone": null,
    "email": null
  },
  {
    "packingslipno": "test2-14-07-01",
    "consignee": "Test 2",
    "address1": "1 Queens Street",
    "address2": "",
    "suburb": "Auckland Central",
    "city": "Auckland",
    "postcode": "",
    "country": null,
    "delvref": null,
    "delvinstructions": null,
    "contactname": null,
    "contactphone": null,
    "email": null
  }
]

```


**Response**
A JSON object array of order and save status.

``` json
[
  {
    "packingslipno": "test1-14-07-01",
    "result": true,
    "msg":""
  },
  {
    "packingslipno": "test2-14-07-01",
    "result": false,
    "msg":"already processed"
  }
]

```
