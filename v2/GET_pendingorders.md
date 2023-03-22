[![](../obsolete-banner.png)](https://api-docs.gosweetspot.com/)

# Pending Orders

    GET pendingorders

## Description
Gets a list of orders published but not processed.

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Parameters
- none

***

## Return format
An array orders:

- **packingslipno** - unique order number or packing slip number from your system
- **consignee** - receipient name
- **address1** - address line 2, street name
- **suburb** - suburb name
- **city** - city name or state name. Depending on destination country, if state information is available, this should be the abbreviated state code
- **postcode** - post code, for NZ addresses, this can be left blank if unknown.
- **country** - ISO Alpha 2 country code, eg NZ, AU, US, UK, CN
- **delvref** - Order number, or customer reference for this order. 
- **delvinstructions** - Any specific instructions to be printed on the label.
- **contactname** - name of person, optional.
- **contactphone** - phone number of person, optional.

***

## Example
**Request**

    https://api.gosweetspot.com/v2/pendingorders

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

        
**Return** __shortened for example purpose__
``` json
[
  {
    "packingslipno": "test-14-07-01",
    "consignee": "Test,",
    "address1": "",
    "address2": "1 Queens Street",
    "suburb": "Auckland Centrol",
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
    "packingslipno": "test1-14-07-01",
    "consignee": "TEST 1",
    "address1": "",
    "address2": "1 QUEENS STREET",
    "suburb": "Auckland Central",
    "city": "Auckland",
    "postcode": "1010",
    "country": "NZ",
    "delvref": null,
    "delvinstructions": null,
    "contactname": null,
    "contactphone": null,
    "email": null
  },
  {
    "packingslipno": "test2-14-07-01",
    "consignee": "TEST 2",
    "address1": "",
    "address2": "1 QUEENS STREET",
    "suburb": "Auckland Central",
    "city": "Auckland",
    "postcode": "1010",
    "country": "NZ",
    "delvref": null,
    "delvinstructions": null,
    "contactname": null,
    "contactphone": null,
    "email": null
  }
]

```

