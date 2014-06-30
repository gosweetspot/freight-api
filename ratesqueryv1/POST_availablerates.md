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
A JSON object array of available rates. These are group into *Available*, *Hidden*, *Rejected*.
The *Hidden* rates, are available rates, but have been filtered out due to user preference, based on cost centre, or destination courier preference.

**Available/Hidden**
- **quoteId** - unqiue rates calculation identifier
- **carriername** - display name of courier provider
- **deliverytype** - courier delivery/service type
- **cost** - freight cost
- **servicestandard** - courier service wording. 
- **comments** - any extra comments supplied with this rate
- **route** - courier provider specific freight routing
- **isruraldelivery** - if delivery has been identified as a rural aread delivery
- **issaturdaydelivery** - if delivery has been flagged for saturday delivery
- **isfreightforward** - if pickup is originating from an address other then the site address
- **carrierservicetype** - carrier provider service type

**Rejected**
- **carriername** - courier provider name
- **deliverytype** - courier delivery/service type
- **reason** - reason why this rates line was ignored.

**ValidationErrors**
- **key** - field name
- **value** - reason for validation failure

    
    
***

## Errors
If there are any validation errors these are reported via the *ValidationErrors* JSON object.

***

## Example
**Request**

    http://api.gosweetspot.com/ratesqueryv1/availablerates

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

    

*Body*
``` json
{
	"Origin": null,
	"Destination": {
		"Id": 0,
		"Name": "DestinationName",
		"Address": {
			"BuildingName": "",
			"StreetAddress": "DestinationStreetAddress",
			"Suburb": "Oamaru",
			"City": "Oamaru",
			"PostCode": "7980",
			"CountryCode": "NZ"
		},
		"Email": "destinationemail@email.com",
		"ContactPerson": "DestinationContact",
		"PhoneNumber": "123456789",
		"IsRural": false,
		"DeliveryInstructions": "Desinationdeliveryinstructions",
		"SendTrackingEmail": false,
		"CostCentreId": 0,
		"ExplicitNotRural": false
	},
	"Packages": [
		{
			"Id": 0,
			"Name": "Custom",
			"Length": 10,
			"Width": 10,
			"Height": 10,
			"Kg": 10,
			"Type": “Box”,
			“PackageCode” : “A5”
		}
	],
	"IsSaturdayDelivery": false,
	"IsSignatureRequired": true,
	"IsUrgentCouriers": false,
	"DutiesAndTaxesByReceiver": false,
"RuralOverride": false,
    "DeliveryReference": "ORDER123"
}
```


**Response** 
``` json
{
	"Available": [
		{
			"QuoteId": "65a5f660-13f7-4a1b-a338-06444e632a37",
			"CarrierName": "Post Haste",
			"DeliveryType": "2 Day Inter Island",
			"Cost": 27.86,
			"ServiceStandard": "By 11am second business day",
			"Comments": "Weight ",
			"Route": "AKL- LOCAL->AKL- SI",
			"IsRuralDelivery": false,
			"IsSaturdayDelivery": false,
			"IsFreightForward": false,
			"CarrierServiceType": "DomesticCourier"
		},
		{
			"QuoteId": "46a958d1-4441-4d4a-9507-5c60f7c444c4",
			"CarrierName": "Post Haste",
			"DeliveryType": "Overnight",
			"Cost": 83.27,
			"ServiceStandard": "By 11am next business day",
			"Comments": "Weight ",
			"Route": "AKL- LOCAL->AKL- SI",
			"IsRuralDelivery": false,
			"IsSaturdayDelivery": false,
			"IsFreightForward": false,
			"CarrierServiceType": "DomesticCourier"
		}
	],
	"Rejected": [],
	"ValidationErrors": {}
}
```

