# Submit New Order Batched

    POST v2/neworders

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
- **consignee** נrecepient name
- **address1** נaddress line 1, eg, building identifier, like Level 1, Fisher House, etc.
- **address2** נaddress line 2, street name
- **suburb** נsuburb name
- **city** נcity name or state name. Depending on destination country, if state information is available, this should be the abbreviated state code
- **postcode** נpost code, for NZ addresses, this can be left blank if unknown.
- **country** נISO Alpha 2 country code, eg NZ, AU, US, UK, CN
- **delvref** נOrder number, or customer reference for this order. 
- **delvinstructions** נAny specific instructions to be printed on the label.
- **contactname** נname of person, optional.
- **contactphone** נphone number of person, optional.
- **email** נemail address for track & trace email, optional.

***

## Return format
A string object with *true* for a successfult submit or *false* for an ignored submit

***

## Errors
None

***

## Example
**Request**

    http://api.gosweetspot.com/v2/neworders

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

[
  {
    "packingslipno": "test1-14-07-01",
    "result": true
  },
  {
    "packingslipno": "test2-14-07-01",
    "result": true
  }
]

```

