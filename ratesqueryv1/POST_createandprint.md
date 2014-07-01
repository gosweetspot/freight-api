# Print Available Rate

    POST ratesquery/printcheapestcourier

## Description
Once a freight option has been identified using the AvailableRates(https://github.com/gosweetspot/freight-api/blob/master/ratesqueryv1/POST_availablerates.md) method, you can use this method to create the shipment.

Upon creating the shipment, the print command can also be automatically initiated. This print command requires the Print Agent to be installed and available.

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters

You need to extend the AvailableRates post body to include other fields specified below.

- **QuoteId** - unique quote identifier returned on the *availablerates* query. 
- **origin** - blank when using site address, or provide one for freight forwards
- **destination** - JSON obect of recepient address details
- **packages** - JSON object array of package sizes
- **issaturdaydelivery** - true/false - is saturday delivery required
- **issignaturerequired** - true/false - is signature on delivery required
- **dutiesandtaxesbyreceiver**  - true/false - where duties are due, is the receiver paying for these
- **ruraloverride** - true/false - ignore all rural delivery validation and surcharges
- **deliveryreference** - string:50, order reference
- **commodities** - JSON object array of customs declared commoditiy information. Only required for international shipments.
- **printtoprinter** - yes/no - if supplied, the print job is sent to the *access_token* desingated printer. For testing purpose this can be provided as "no"
- **outputs** - JSON string array. Return output of label as a PNG or PDF. Acceptable values: "LABEL_PDF"/"LABEL_PNG"

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
 
*commodity Object*
- **units** - decimal, how many units
- **unitvalue** - decimal, value per unit
- **unitkg** - decimal, weight in kg per unit
- **currency** - string:3, declared value currency designation, eg NZD, AUD, USD
- **country** - string:2, ISO Alpha 2 country code for the Country of Manufacture of goods, eg, NZ, AU, US, GB, CN, CA, etc.



## Return format
A JSON object with the created shipment details.

- **carrier** - internal system carrier identifier
- **carriername** - courier provider name
- **isfreightforward** - is shipment a freight forward shipment.
- **message** - action outcome message
- **errors** - JSON string array of error messages
- **siteid** -  account site id
- **consignments** - JSON object arrary or consignments created. Generally only 1 is created, however were a split is required, more could be created

**Consignment**
- **connote** - courier provider connote number
- **trackingurl** - direct url to track and trace this shipment
- **cost** - total cost of shipment, excluding taxes
- **carriertype** - internal carrier classification
- **issaturdaydelivery** - true/false - whether saturday delivery service was applied
- **isrural** - true/false - whether delivery identified as rural
- **isovernight** - true/false - whether service is overnight where delivery is inter island
- **hastrackpaks** - true/false - whether this shipment has any trackpaks on it
- **outputs** - JSON object byte array with requested output file as Base64 encoded string

***


## Example
**Request**

    http://api.gosweetspot.com/ratesqueryv1/createandprint

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

    

*Body*
``` json

```


**Response** 
``` json

```

