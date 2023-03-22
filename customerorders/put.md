[![](../obsolete-banner.png)](https://api-docs.gosweetspot.com/)

# Submit New Customer Order Batched

    PUT api/customerorders

## Description
Saves a new orders or updates a pending order. If the packing slip number has already been processed, the message will be ignored.

This method will accept orders as a array.

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

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
- **rawaddress** - full, unvalidated address body for display purposes only. Use \n for newline in this field. Optional.
- **costcentre** - Put the exact name of a cost centre here and the cost centre will be pre-selected when fulfilling the order. Optional.
- **products** - optional, JSON object of product descriptions
- **packages** - optional, JSON object of packages on order. Currently not supported for SpeedPrint workflow.
- **iconUrl** - optional, custom icon Url link.

### products json object
- **productcode** - string:20, your unique product code for the good.
- **description** - string:20, goods description of the product
- **units** - decimal, number of units of product
- **unitvalue** - decimal, per unit value of product
- **countryofmanufacture** - string:2, ISO Alpha 1 code of country, eg, NZ, AU
- **unitkg** - decimal, per unit weight in KG
- **imageurl** - string:500, product image url if available. Should be an open/public url.
- **currency** - string:3, currency code for value, eg NZD, AUD, USD
- **alreadySent** - decimal, units of product that have already been sent prior to this shipment. This should be less than the "units" provided.

### packages json object
- **PackageStockName** specify the name of the package here, e.g. GSS-A5 Satchel. The package needs to be previously configured [here](https://ship.gosweetspot.com/stocksizes) with length/width/height parameters.
- **Quantity** - required int.
- **WeightKg** - optional float. If this is not present, will use the default weight of the package.
- **LengthCm** - optional float. This parameter will be ignored if the package is a SATCHEL type.
- **WidthCm** - optional float. This parameter will be ignored if the package is a SATCHEL type.
- **HeightCm** - optional float. This parameter can be edited even if the package is a SATCHEL type.


***

## Return format
JSON object array per order with *true* for a successfult submit or *false* for an ignored submit

***

## Errors
None

***

## Example
**Request**

    https://api.gosweetspot.com/api/customerorders

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
    "email": null,
    "iconUrl": null,
    "Products": [{
        "productcode": "ABC",
        "Description": "Wall Paint",
        "Units": 1.0,
        "UnitValue": 10.0,
        "CountryofManufacture": null,
        "UnitKg": 1.0,
        "ImageUrl": null,
        "Currency": "NZD"
    }, {
        "productcode": "DCF",
        "Description": "Wall Art",
        "Units": 1.0,
        "UnitValue": 10.0,
        "CountryofManufacture": null,
        "UnitKg": 1.0,
        "ImageUrl": null,
        "Currency": "NZD"
    }]
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
