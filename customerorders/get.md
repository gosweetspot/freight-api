# Customer Orders

    GET api/customerorders

## Description
Get the list of customer orders published to the queue. You can filter on processed or non-processed.

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters
<table>
  <tr>
    <th colspan="2">Parameters</th>
  </tr>
  <tr>
    <td>packingslipno</td>
    <td>comma separated list of packing slip numbers to apply filter on</td>
  </tr>
  <tr>
    <td>createdfrom</td>
    <td>UTC formatted date and time to filter the shipments on. This field is for earliest date</td>
  </tr>
  <tr>
    <td>createdto</td>
    <td>UTC formatted date and time to filter the shipments on. This field is for latest date</td>
  </tr>
  <tr>
    <td>excludecompleted</td>
    <td>true/false - when true excludes all completed packing slip and only returns pending orders</td>
  </tr>
  <tr>
    <td>page</td>
    <td>when multi pages of results are available specifies which page to get</td>
  </tr>
  <tr>
    <td>pagesize</td>
    <td>how many records to return per page. Default = 100 records</td>
  </tr>
      <tr>
    <td>includeProducts</td>
    <td>true/false - when true, each customer order record will also include the product lines associated with the record.</td>
  </tr>
</table>

***

## Return format
### Root Object
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
- **email** - email address.
- **isrural** - is the address a rural delivery address
- **notrural** - override and declared as not rural.
- **costcentre** - cost centre to use.
- **status** - JSON object of current status
- **products** - JSON list of line items on order

### Status
- **status** - current status.
- **ticketnumber** - if printed already, the current ticket number
- **trackingurl** - url to track the order
- **picked** - local date time of when shipment was picked up
- **delivered** - local date time of when shipment was Delivered
- **manualticket** - true/false - whether the ticket was created manually or via an integrated channel feed.

### Products
- **productcode** - SKU of Product
- **description** - Name of Product
- **units"** - Units ordered
- **unitvalue** - Value per unit
- **countryofManufacture** ISO Alpha 2 country code, eg NZ, AU, US, UK, CN
- **unitkg** - Weight per unit
- **imageurl** - An image of the product
- **currency** - 3 letter code for currency
- **alreadySent** - Amount of product fulfilled prior to this order
- **fulfilledQty** - Amount of product fulfilled on this order
- **linetotal"** - Total value of this order

## Example
**Request**

    https://api.gosweetspot.com/api/customerorders?createdfrom=Monday,%2015%20February%202016%207:26:15%20AM&page=2

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8


**Return** __shortened for example purpose__
``` json
{
    "Page": 1,
    "PageSize": 100,
    "Pages": 6,
    "Results": [
        {
            "packingslipno": "SSORDER13667",
            "consignee": "LITTLE LAMB",
            "address1": "",
            "address2": "103 HAVENWOOD PLACE",
            "suburb": "BIRKENHEAD",
            "city": "NORTH SHORE CITY",
            "postcode": "0626",
            "country": "NZ",
            "delvref": "SSORDER13667",
            "delvinstructions": "A5SHEET X 1  A5 X 1",
            "contactname": "BROOKES STONE",
            "contactphone": "021 123456",
            "email": "info@littlelamb.co.nz",
            "isrural": null,
            "notrural": null,
            "costcentre": null,
            "status": {
                "Status": "DELIVERED",
                "ticketnumber": "SSPOT018162",
                "trackingurl": "http://gosweetspot.com/track/4180-SSPOT018162",
                "Picked": "2016-02-22T15:31:21",
                "Delivered": "2016-02-23T12:46:45",
                "manualticket": true
            },
		"products": [{
				"productcode": "ABC",
				"description": "WALL PAINT",
				"units": 1.00000000,
				"unitvalue": 10.0000,
				"countryofManufacture": "",
				"unitkg": 1.00000000,
				"imageurl": null,
				"currency": "NZD",
				"alreadySent": 0.00000000,
				"fulfilledQty": 1.00000000,
				"linetotal": 10.000000000000
			}
		]
        },
        {
            "packingslipno": "SSORDER13668",
            "consignee": "ROCK ON",
            "address1": "",
            "address2": "226 STEWART ROAD",
            "suburb": "RAMARAMA",
            "city": "AUCKLAND",
            "postcode": "2579",
            "country": "NZ",
            "delvref": "SSORDER13668",
            "delvinstructions": "A5 X 2  A4 X 5  OVERNIGHT X 2",
            "contactname": "ALBERT",
            "contactphone": "021212563",
            "email": "albert@rockon.co.nz",
            "isrural": null,
            "notrural": null,
            "costcentre": null,
            "status": {
                "Status": "DELIVERED",
                "ticketnumber": "SSPOT018161",
                "trackingurl": "http://gosweetspot.com/track/4180-SSPOT018161",
                "Picked": "2016-02-22T15:31:21",
                "Delivered": "2016-02-24T08:42:22",
                "manualticket": true
            },
		"products": [{
				"productcode": "ABC",
				"description": "WALL PAINT",
				"units": 1.00000000,
				"unitvalue": 10.0000,
				"countryofManufacture": "",
				"unitkg": 1.00000000,
				"imageurl": null,
				"currency": "NZD",
				"alreadySent": 0.00000000,
				"fulfilledQty": 1.00000000,
				"linetotal": 10.000000000000
			}
		]
        },
        {
            "packingslipno": "SSORDER13669",
            "consignee": "PREMIUM BLUE LTD",
            "address1": "5C",
            "address2": "102 ELLICE RD",
            "suburb": "GLENFIELD",
            "city": "NORTH SHORE CITY",
            "postcode": "0629",
            "country": "NZ",
            "delvref": "SSORDER13669",
            "delvinstructions": "A4 X 1  A2 X 1  OVERNIGHT X 1",
            "contactname": "ANDREW BURNS",
            "contactphone": "09 444 2131",
            "email": "andy@blueltd.co.nz",
            "isrural": null,
            "notrural": null,
            "costcentre": null,
            "status": {
                "Status": "DELIVERED",
                "ticketnumber": "SSPOT018160",
                "trackingurl": "http://gosweetspot.com/track/4180-SSPOT018160",
                "Picked": "2016-02-25T15:24:10",
                "Delivered": "2016-02-26T08:11:14",
                "manualticket": true
            },
		"products": [{
				"productcode": "ABC",
				"description": "WALL PAINT",
				"units": 1.00000000,
				"unitvalue": 10.0000,
				"countryofManufacture": "",
				"unitkg": 1.00000000,
				"imageurl": null,
				"currency": "NZD",
				"alreadySent": 0.00000000,
				"fulfilledQty": 1.00000000,
				"linetotal": 10.000000000000
			}
		]
        }
    ]
}

```
