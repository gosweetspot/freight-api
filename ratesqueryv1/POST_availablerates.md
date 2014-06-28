# Available Rates

    POST ratesquery/availablerates

## Description
Query to get available courier services and rates for the destination.

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters
- **origin** - Specify the unique order number from your source system, that was used as the packing slip no when the order was published
- **destination** נrecepient name
- **packages** נaddress line 1, eg, building identifier, like Level 1, Fisher House, etc.
- **issaturdaydelivery** נaddress line 2, street name
- **issignaturerequired** נsuburb name
- **dutiesandtaxesbyreceiver** נpost code, for NZ addresses, this can be left blank if unknown.
- **ruraloverride** נISO Alpha 2 country code, eg NZ, AU, US, UK, CN
- **deliveryreference** נOrder number, or customer reference for this order. 

*origin/destination Object*
- **name** - string:60, Company name or persons name
- **contactperson** - string:60, contact person at address, optional
- **phonenumber** - string:60, phone number, optional
- **isrural** - true/false, optional
- **deliveryinstructions** - string:120, special instructions to print on the label. For origin this field is ignored.
- **sendtrackingemail** - true/false, optional
- **costcenterid** - int, optional
- **explicitnotrural** - true/false, when true not rural surcharges are added.
- **address** - JSON Object as described below

*address Object*
- **buildingname** - string:60, property identifier, such as Unit 1, Level 10, Panasonic House, etc
- **streetaddress** - string:60, street number and name. 
- **suburb** - string:60, suburb name
- **city** - string:60, city or state name. In countries where there are official states, use use use state abbreviations, such as California = CA, New South Wales = NSW, etc.
- **postcode** - string:10, postal code
- **countrycode** - string:2, ISO Alpha 2 country code, eg, NZ, AU, US, GB, CN, CA, etc.

*package Object*
- **length** - decimal, package length in centimetres
- **width** - decimal, package width in centimetres
- **height** - decimal, package height  in centimetres
- **kg** - decimal, package weight in kilograms
- **type** - string:10, package type, eg, Box, Carton, Satchel, Bag, Pallet, etc
- **packagecode** - string:5, Trackpack codes, such as DLE, A5, A4 (please consult support before providing a value in this field) This feature is not available on all accounts.


## Return format
A JSON object array of available rates. These are group into *Available*, *Hidden*, *Rejected*

**Available/Hidden**
- **quoteId** - unqiue rates calculation identifier
- **carriername** - unqiue rates calculation identifier
- **deliverytype** - unqiue rates calculation identifier
- **cost** - unqiue rates calculation identifier
- **servicestandard** - unqiue rates calculation identifier
- **comments** - unqiue rates calculation identifier
- **route** - unqiue rates calculation identifier
- **isruraldelivery** - unqiue rates calculation identifier
- **issaturdaydelivery** - unqiue rates calculation identifier
- **isfreightforward** - unqiue rates calculation identifier
- **carrierservicetype** - unqiue rates calculation identifier

**Rejected**
- **carriername** - unqiue rates calculation identifier
- **deliverytype** - unqiue rates calculation identifier
- **reason** - unqiue rates calculation identifier

**ValidationErrors**
- **key** - unqiue rates calculation identifier
- **value** - unqiue rates calculation identifier

    
    
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
    "packingslipno": "TEST0002",
    "consignee": "CHASE SYSTEMS",
    "Status": "DELIVERED",
    "TicketNumber": "SSPOT010702",
    "TrackingUrl": "http://sweetspotgroup.co.nz/track/4180/SSPOT010702",
    "Picked": "2012-11-01T17:59:00",
    "Delivered": "2012-11-02T13:44:00"
}
```


**Response** 
``` json
true
```

