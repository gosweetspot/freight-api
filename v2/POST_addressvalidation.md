# Address Validation

    POST v2/addressvalidation

## Description
Query to validation customer address details.
For NZ addresses, the addresses are also assessed for rural delivery, saturday delivery and residential delivery .

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters

*JSON Object*
- **name** - string:50, Company name or persons name
- **contactperson** - string:50, contact person at address, optional
- **phonenumber** - string:50, phone number, optional
- **deliveryinstructions** - string:120, special instructions to print on the label. For origin this field is ignored.
- **email** - string:200, email address
- **address** - JSON Object as described below

*address Object*
- **buildingname** - string:60, property identifier, such as Unit 1, Level 10, Panasonic House, etc
- **streetaddress** - string:60, street number and name. 
- **suburb** - string:60, suburb name
- **city** - string:60, city or state name. In countries where there are official states, use use use state abbreviations, such as California = CA, New South Wales = NSW, etc.
- **postcode** - string:10, postal code
- **countrycode** - string:2, ISO Alpha 2 country code, eg, NZ, AU, US, GB, CN, CA, etc.



## Return format
A JSON object with validation response.

- **validated** - true/false, result of state/suburb/postcode/country validation
- **address** - address object as posted, with additional property AvailableServices
- **errors** - list of validation messages

*availableservice Object*
- **carrier** - name of carrier
- **isresidential** - indicates if this is a residential service
- **isrural** - indicates if this is a rural service
- **hassaturdayservice** - indicates if saturday delivery is a possible service
- **branchcode** - the branch code of the branch serving this address
- **runnumber** - run number

***

## Example
**Request**

    http://api.gosweetspot.com/v2/addressvalidation

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

    

*Body*
``` json
{
	"Consignee": "0123456789 0123456789 0123456789 0123456789",
	"Address": {
		"BuildingName": "",
		"StreetAddress": "1 Some Street",
		"Suburb": "MascotX",
		"City": "NSW",
		"PostCode": "2020",
		"CountryCode": "AU",
		"IsRural": false
	},
	"Email": "",
	"ContactPerson": "",
	"PhoneNumber": "",
	"DeliveryInstructions": "",
	"AvailableServices": []
}
```


**Response** 

Invalid address example
``` json
{
	"Address": {
		"Consignee": "0123456789 0123456789 0123456789 0123456789",
		"Address": {
			"BuildingName": "",
			"StreetAddress": "1 Some Street",
			"Suburb": "MascotX",
			"City": "NSW",
			"PostCode": "2020",
			"CountryCode": "AU",
			"IsRural": false,
			"IsResidential": false
		},
		"Email": "",
		"ContactPerson": "",
		"PhoneNumber": "",
		"DeliveryInstructions": "",
		"AvailableServices": []
	},
	"Validated": false,
	"Errors": ["Suburb/City-State/Postcode invalid"]
}

```
Valid address example

```
{
	"Address": {
		"Consignee": "0123456789 0123456789 0123456789 0123456789",
		"Address": {
			"BuildingName": "",
			"StreetAddress": "1 Chesham Lane",
			"Suburb": "Clevedon",
			"City": "Auckland",
			"PostCode": "2248",
			"CountryCode": "NZ",
			"IsRural": false,
			"IsResidential": false
		},
		"Email": "",
		"ContactPerson": "",
		"PhoneNumber": "",
		"DeliveryInstructions": "",
		"AvailableServices": [{
				"Carrier": "NZCouriers",
				"IsResidential": true,
				"IsRural": true,
				"HasSaturdayService": false,
				"BranchCode": "MKC",
				"RunNumber": ""
			}, {
				"Carrier": "PostHaste",
				"IsResidential": true,
				"IsRural": true,
				"HasSaturdayService": false,
				"BranchCode": "AKL",
				"RunNumber": ""
			}, {
				"Carrier": "CastleParcel",
				"IsResidential": true,
				"IsRural": true,
				"HasSaturdayService": false,
				"BranchCode": "AKL",
				"RunNumber": ""
			}, {
				"Carrier": "NOWCouriers",
				"IsResidential": true,
				"IsRural": true,
				"HasSaturdayService": false,
				"BranchCode": "AKL",
				"RunNumber": ""
			}
		]
	},
	"Validated": true,
	"Errors": []
}
```
