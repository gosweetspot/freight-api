# Pending Orders

    GET pendingorders

## Description
Gets a list of orders published but not processed.

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters
- none

***

## Return format
An array orders:

- **packingslipno** — unique order number or packing slip number from your system
- **consignee** — receipient name
- **address1** — address line 1, eg, building identifier, like Level 1, Fisher House, etc.
- **address2** — address line 2, street name
- **suburb** — suburb name
- **city** — city name or state name. Depending on destination country, if state information is available, this should be the abbreviated state code
- **postcode** — post code, for NZ addresses, this can be left blank if unknown.
- **country** — ISO Alpha 2 country code, eg NZ, AU, US, UK, CN
- **delvref** — Order number, or customer reference for this order. 
- **delvinstructions** — Any specific instructions to be printed on the label.
- **contactname** — name of person, optional.
- **contactphone** — phone number of person, optional.

***

## Errors
None

***

## Example
**Request**

    http://api.gosweetspot.com/v2/pendingorders

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

        
**Return** __shortened for example purpose__
``` json
[
    {
        "packingslipno": "123",
        "consignee": "NAME",
        "address1": "LEVEL 1",
        "address2": "1",
        "suburb": "Avondale",
        "city": "Auckland",
        "postcode": "0600",
        "country": "NZ",
        "delvref": "XYZ123",
        "delvinstructions": "please deliver to right hand",
        "contactname": "Bob",
        "contactphone": "021212121"
    },
    {
        "packingslipno": "634854611262635524",
        "consignee": "TEST RECEIVER",
        "address1": "LEVEL 1",
       "address2": "1",
        "suburb": "Auckland Central",
        "city": "Auckland",
        "postcode": "1010",
        "delvref": "Order # 123",
        "delvinstructions": "Please leave next to pot plant",
        "contactname": "Tom Jones",
        "contactphone": "0800 123 456"
    }
]

```

