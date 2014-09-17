# Submit New Order

    POST v2/neworder

## Description
Saves a new order or updates a pending order. If the packing slip number has already been processed, the message will be ignored.

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters
- **packingslipno** - string:20, Specify the unique order number from your source system, that was used as the packing slip no when the order was published
- **consignee** - string:60, recepient name
- **address1** - string:60, address line 1, eg, building identifier, like Level 1, Fisher House, etc.
- **address2** - string:60, address line 2, street name
- **suburb** - string:60, suburb name
- **city** - string:60, city name or state name. Depending on destination country, if state information is available, this should be the abbreviated state code
- **postcode** - string:10, post code, for NZ addresses, this can be left blank if unknown.
- **country** - ISO Alpha 2 country code, eg NZ, AU, US, UK, CN
- **delvref** - string:50, Order number, or customer reference for this order. 
- **delvinstructions** - string:120, Any specific instructions to be printed on the label.
- **contactname** - string:60, name of person, optional.
- **contactphone** - string:60, phone number of person, optional.
- **email** - string:60, email address for track & trace email, optional.

***

## Return format
A string object with *true* for a successfult submit or *false* for an ignored submit

***

## Errors
None

***

## Example
**Request**

    http://api.gosweetspot.com/v2/neworder

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

    

*Body*
``` json
{
  "packingslipno": "test-14-07-01",
  "consignee": "Test,",
  "address1": "1 Queens Street",
  "address2": "",
  "suburb": "Auckland Centrol",
  "city": "Auckland",
  "postcode": "",
  "country": null,
  "delvref": null,
  "delvinstructions": null,
  "contactname": null,
  "contactphone": null,
  "email": null
}
```


**Response** 
``` json
true
```

