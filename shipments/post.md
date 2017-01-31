# Create Shipments

    POST api/shipments

## Description
This method is used to create new shipments.

There are 2 pre-conditions that need to be considered before calling this method.
1. Does your workflow require you to display/calculate the freight costs and options prior to creating the shipment?
2. Does your workflow already know which carrier is to be used for creating the shipment?


#### 1. Display/Calculate rates first
In this scenario, you need to call the [AvailableRates](https://github.com/gosweetspot/freight-api/blob/master/ratesqueryv1/POST_availablerates.md) method first to resolve the different price options you may have.  Every option is accompanied by a **QuoteId** which needs to be retain to be used with the create shipment method.

#### 2. Create by Carrier Name and service
In this scenario, you won't know the cost of the freight for the shipment till after the shipment is created.  You will request the shipment to be used by specifying the carrier name, and service.


**Printing-**  if the access_key has an associated printer setup, the print job is activated by default.  This can be turned off by specifying *PrintToPrinter=false*

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters

You need to extend the AvailableRates post body to include other fields specified below.

When *QuoteId* is supplied, the *carrier* and *service* fields are ignored.  They should be used in exclusive pattern.

- **QuoteId** - unique quote identifier returned on the *availablerates* query.
- **Carrier** - carrier name, to select which carrier to create shipment for.
- **Service** - carrier service name, for which the shipment should be created for. If not supplied, the cheapest price option is selected.
- **origin** - blank when using site address, or provide one for freight forwards
- **destination** - JSON obect of recepient address details
- **packages** - JSON object array of package sizes
- **issaturdaydelivery** - true/false - is saturday delivery required
- **issignaturerequired** - true/false - is signature on delivery required
- **dutiesandtaxesbyreceiver**  - true/false - where duties are due, is the receiver paying for these
- **ruraloverride** - true/false - ignore all rural delivery validation and surcharges
- **deliveryreference** - string:50, order reference
- **commodities** - JSON object array of customs declared commoditiy information. Only required for international shipments.
- **printtoprinter** - true/false - if supplied, the print job is sent to the *access_token* desingated printer. For testing purpose this can be provided as "no"
- **outputs** - optional -  JSON string array. Returns output of label as a PNG or PDF. Acceptable values:  
      LABEL_PDF - label is presented on an A4 page  
      LABEL_PNG_100X175 - label is presented as a PNG image with dimension 100mm x 175mm  
      LABEL_PNG_100X150 - label is presented as a PNG image with dimension 100mm x 150mm  
      LABEL_PDF_100X175 - label is presented as a PDF with dimension 100mm x 175mm  
      LABEL_PDF_100X150 - label is presented as a PDF with dimension 100mm x 150mm  

      The 100x150 sizing is presently experimental and not available across all carriers.  
- **hasdg** - true/false - does your shipment contain any dangerous goods
- **dangerousgoods** - JSON object of dangerous goods details

*origin/destination Object*
- **name** - string:60, Company name or persons name
- **contactperson** - string:60, contact person at address, optional
- **phonenumber** - string:60, phone number, optional
- **isrural** - true/false, optional
- **deliveryinstructions** - string:120, special instructions to print on the label. For origin this field is ignored.
- **sendtrackingemail** - true/false, optional
- **costcentreid** - int, optional
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
- **name** - string:15, package custom name, if none available, use "custom"
- **length** - integer, package length in centimetres
- **width** - integer, package width in centimetres
- **height** - integer, package height  in centimetres
- **kg** - decimal, package weight in kilograms
- **type** - string:10, package type, eg, Box, Carton, Satchel, Bag, Pallet, etc
- **packagecode** - string:5, Trackpack codes, such as DLE, A5, A4 (please consult support before providing a value in this field) This feature is not available on all accounts.

*commodity Object*
- **description** - string50, description of good
- **harmonizedcode** - string50, customs related HS Code for goods.
- **units** - integer, how many units
- **unitvalue** - decimal, value per unit
- **unitkg** - decimal, weight in kg per unit
- **currency** - string:3, declared value currency designation, eg NZD, AUD, USD
- **country** - string:2, ISO Alpha 2 country code for the Country of Manufacture of goods, eg, NZ, AU, US, GB, CN, CA, etc.

*dangerousgoods Object*
- **additionalhandinginfo** - string100
- **hazchemcode** - string50
- **isradioactive** - true/false, is goods radio active
- **cargoaircraftonly** - true/false, Cargo Aircraft Only
- **lineitems** - JSON object array of items

*dangerousgoods lineitems Object*
- **description** - string100
- **classordivision** - string50
- **unoridno** - string50
- **packinggroup** - string50
- **subsidaryrisk** - string50
- **packing** - string50
- **packinginstr** - string50
- **authorization** - string50

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


## Example 1 - Domestic Outbound Shipment
This is a simple outbound, or sending out from your site, shipment.

**Request**

    POST http://api.gosweetspot.com/api/shipments

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8


*Body*
``` json
{
    "Origin": null,
    "Destination": {
        "Name": "DestinationName",
        "Address": {
            "BuildingName": "",
            "StreetAddress": "DestinationStreetAddress",
            "Suburb": "Avonside",
            "City": "Christchurch",
            "PostCode": "8061",
            "CountryCode": "NZ"
        },
        "Email": "destinationemail@email.com",
        "ContactPerson": "DestinationContact",
        "PhoneNumber": "123456789",
        "IsRural": false,
        "DeliveryInstructions": "Desinationdeliveryinstructions",
        "SendTrackingEmail": false,
        "ExplicitNotRural": false
    },
    "Packages": [
        {
            "Name": "GSS-DLE SATCHEL",
            "Length": 1,
            "Width": 10,
            "Height": 1,
            "Kg": 0.1,
        }
    ],
    "Commodities": null,
    "IsSaturdayDelivery": false,
    "IsSignatureRequired": true,
    "IsUrgentCouriers": false,
    "DutiesAndTaxesByReceiver": false,
    "RuralOverride": false,
    "DeliveryReference": "ORDER123",
    "PrintToPrinter": "false",
    "Carrier": "Post Haste"
}
```


**Response**

``` json
{
    "CarrierId": 102,
    "CarrierName": "Post Haste",
    "IsFreightForward": false,
    "IsOvernight": false,
    "IsSaturdayDelivery": false,
    "IsRural": false,
    "HasTrackPaks": false,
    "Message": "Connote created and print queued.",
    "AddressLabelMessage": null,
    "AddressLabelError": null,
    "Errors": [],
    "SiteId": 4180,
    "Consignments": [
        {
            "Connote": "SSPOT018667",
            "TrackingUrl": "http://gosweetspot.com/track/4180-SSPOT018667",
            "Cost": 4.07,
            "CarrierType": 13,
            "IsSaturdayDelivery": false,
            "IsRural": false,
            "IsOvernight": false,
            "HasTrackPaks": false,
            "ConsignmentId": 6215942,
            "OutputFiles": null,
            "Items": null
        }
    ],
    "Downloads": [],
    "CarrierType": 13,
    "AlertPath": null,
    "Notifications": [],
    "HasSaturdayDeliveryLabel": false
}
```
Base64 encoding string has been trimmed for presentation.




## Example 2 - Domestic Inbound/Returns Shipment
Creating a shipment for getting a shipment picked from an external location. The destination of the shipment can be you or even a 3rd party.
This will create a freight forward shipment, and generate an email that will be sent to the *Origin* contacts email address with the courier label attached, as well as location booking instructions.
In the case that you want to suppress the automatic email you can provide an additional attribute *DisableFreightForwardEmails=true*.

**Request**

    POST http://api.gosweetspot.com/api/shipments

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

*Body*
``` json
{
    "Origin": {
        "Name": "Bob Jones",
        "Address": {
            "BuildingName": "",
            "StreetAddress": "Bob Jones Close",
            "Suburb": "Avonside",
            "City": "Christchurch",
            "PostCode": "8061",
            "CountryCode": "NZ"
        },
        "Email": "destinationemail@email.com",
        "ContactPerson": "DestinationContact",
        "PhoneNumber": "123456789",
        "IsRural": false,
        "DeliveryInstructions": "Desinationdeliveryinstructions"
    },
    "Destination": {
        "Name": "DestinationName",
        "Address": {
            "BuildingName": "",
            "StreetAddress": "DestinationStreetAddress",
            "Suburb": "Avondale",
            "City": "Auckland",
            "PostCode": "0600",
            "CountryCode": "NZ"
        },
        "Email": "destinationemail@email.com",
        "ContactPerson": "DestinationContact",
        "PhoneNumber": "123456789",
        "IsRural": false,
        "DeliveryInstructions": "Desinationdeliveryinstructions",
        "SendTrackingEmail": false,
    },
    "Packages": [
        {
            "Name": "GSS-DLE SATCHEL",
            "Length": 1,
            "Width": 10,
            "Height": 1,
            "Kg": 0.1,
        }
    ],
    "Commodities": null,
    "IsSaturdayDelivery": false,
    "IsSignatureRequired": true,
    "IsUrgentCouriers": false,
    "DutiesAndTaxesByReceiver": false,
    "DeliveryReference": "ORDER123",
    "PrintToPrinter": "false",
    "Outputs": null,
    "CarrierId": 0,
    "Carrier": "Post Haste",
    "Service": null,
    "SiteId": 0,
    "IncludeLineDetails": false,
    "ShipType": 1,
    "HasDG": false,
    "DangerousGoods": null,
    "DisableFreightForwardEmails": false,
    "IncludeInsurance": false
}

```


**Response**

``` json
{
    "CarrierId": 129,
    "CarrierName": "Post Haste",
    "IsFreightForward": true,
    "IsOvernight": false,
    "IsSaturdayDelivery": false,
    "IsRural": false,
    "HasTrackPaks": false,
    "Message": "Connote created and print queued.",
    "AddressLabelMessage": null,
    "AddressLabelError": null,
    "Errors": [],
    "SiteId": 4180,
    "Consignments": [
        {
            "Connote": "AIG00012137",
            "TrackingUrl": "http://gosweetspot.com/track/4180-AIG00012137",
            "Cost": 14.8,
            "CarrierType": 18,
            "IsSaturdayDelivery": false,
            "IsRural": false,
            "IsOvernight": false,
            "HasTrackPaks": false,
            "ConsignmentId": 6215943,
            "OutputFiles": null,
            "Items": null
        }
    ],
    "Downloads": [],
    "CarrierType": 18,
    "AlertPath": null,
    "Notifications": [],
    "HasSaturdayDeliveryLabel": false
}
```
Base64 encoding string has been trimmed for presentation.




## Example 3 - Domestic Outbound Shipment with Dangerous Goods
Creating a standard Outbound shipment which contain Dangerous Goods.
This is the same as a standard outbound, with the additional details of the DG.  The response body will contain a base64 ecoded binary stream of the DG PDF that needs to be printed to a A4 printer.

**Request**

    POST http://api.gosweetspot.com/api/shipment

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
            "Suburb": "Avonside",
            "City": "Christchurch",
            "PostCode": "8061",
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
            "Name": "GSS-DLE SATCHEL",
            "Length": 1,
            "Width": 10,
            "Height": 1,
            "Kg": 0.1,
            "PackageCode": 0
        }
    ],
    "Commodities": null,
    "IsSaturdayDelivery": false,
    "IsSignatureRequired": true,
    "IsUrgentCouriers": false,
    "DutiesAndTaxesByReceiver": false,
    "RuralOverride": false,
    "DeliveryReference": "ORDER123",
    "PrintToPrinter": "false",
    "Outputs": [
        10
    ],
    "CarrierId": 0,
    "Carrier": "Post Haste",
    "Service": null,
    "SiteId": 0,
    "IncludeLineDetails": false,
    "ShipType": 1,
    "HasDG": true,
    "DangerousGoods": {
        "AdditionalHandlingInfo": "Some info",
        "HazchemCode": "HC",
        "IsRadioActive": false,
        "CargoAircraftOnly": false,
        "LineItems": [
            {
                "ConsignmentId": 0,
                "Description": "desc",
                "ClassOrDivision": "class",
                "UNorIDNo": "",
                "PackingGroup": "",
                "SubsidaryRisk": "",
                "Packing": "",
                "PackingInstr": "",
                "Authorization": ""
            }
        ]
    },
    "DisableFreightForwardEmails": false,
    "IncludeInsurance": false
}

```


**Response**

``` json
{
    "CarrierId": 102,
    "CarrierName": "Post Haste",
    "IsFreightForward": false,
    "IsOvernight": false,
    "IsSaturdayDelivery": false,
    "IsRural": false,
    "HasTrackPaks": false,
    "Message": "Connote created and print queued.",
    "AddressLabelMessage": null,
    "AddressLabelError": null,
    "Errors": [],
    "SiteId": 4180,
    "Consignments": [
        {
            "Connote": "SSPOT018668",
            "TrackingUrl": "http://gosweetspot.com/track/4180-SSPOT018668",
            "Cost": 4.07,
            "CarrierType": 13,
            "IsSaturdayDelivery": false,
            "IsRural": false,
            "IsOvernight": false,
            "HasTrackPaks": false,
            "ConsignmentId": 6215944,
            "OutputFiles": {
                "DG_FORM_PDF": [
                    "JVBERi0xLjQKJdP0zOEKMSAwIG9iago8PAovQ3JlYXRpb25EYXRlKEQ6MjAxNjA0MTYxMDI5MTIrMTInMDAnKQovQ3JlYXRvcihQREZzaGFycCAxLjMyLjMwNTctRU9GCg=="
                ]
            },
            "Items": null
        }
    ],
    "Downloads": [],
    "CarrierType": 13,
    "AlertPath": null,
    "Notifications": [],
    "HasSaturdayDeliveryLabel": false
}
```
Base64 encoding string has been trimmed for presentation.


## Example 4 - International Outbound Shipment
Sending overseas. These shipment require addtional details for goods description for customs reasons. This is provided in the *Commodities* property.

**Request**

    POST http://api.gosweetspot.com/api/shipments

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
            "Suburb": "Mascot",
            "City": "NSW",
            "PostCode": "2020",
            "CountryCode": "AU"
        },
        "Email": "destinationemail@email.com",
        "ContactPerson": "DestinationContact",
        "PhoneNumber": "123456789",
        "IsRural": false,
        "DeliveryInstructions": "Desinationdeliveryinstructions",
        "SendTrackingEmail": false
    },
    "Packages": [
        {
            "Name": "Custom",
            "Length": 20,
            "Width": 30,
            "Height": 50,
            "Kg": 10,
        }
    ],
    "Commodities": [
        {
            "HarmonizedCode": null,
            "Description": "Mens Socks",
            "UnitValue": 50.5,
            "Units": 10,
            "UnitKg": 1,
            "Country": "NZ",
            "Currency": "NZD"
        }
    ],
    "IsSaturdayDelivery": false,
    "IsSignatureRequired": true,
    "IsUrgentCouriers": false,
    "DutiesAndTaxesByReceiver": false,
    "RuralOverride": false,
    "DeliveryReference": "ORDER123",
    "PrintToPrinter": "false",
    "Outputs": null,
    "CarrierId": 0,
    "Carrier": "FedEx",
    "Service": null,
    "SiteId": 0,
    "IncludeLineDetails": false,
    "ShipType": 1,
    "HasDG": false,
    "DangerousGoods": null,
    "DisableFreightForwardEmails": false,
    "IncludeInsurance": false
}

```


**Response**

``` json
{
    "CarrierId": 96,
    "CarrierName": "FedEx",
    "IsFreightForward": false,
    "IsOvernight": false,
    "IsSaturdayDelivery": false,
    "IsRural": false,
    "HasTrackPaks": false,
    "Message": "Connote created and print queued.",
    "AddressLabelMessage": null,
    "AddressLabelError": null,
    "Errors": [],
    "SiteId": 4180,
    "Consignments": [
        {
            "Connote": "782847803802",
            "TrackingUrl": "http://gosweetspot.com/track/4180-782847803802",
            "Cost": 67.17,
            "CarrierType": 4,
            "IsSaturdayDelivery": false,
            "IsRural": false,
            "IsOvernight": false,
            "HasTrackPaks": false,
            "ConsignmentId": 6215945,
            "OutputFiles": null,
            "Items": null
        }
    ],
    "Downloads": [],
    "CarrierType": 4,
    "AlertPath": null,
    "Notifications": [],
    "HasSaturdayDeliveryLabel": false
}```
Base64 encoding string has been trimmed for presentation.


## Example 5 - Shipment with Pre-Rated pricing

Prior to creating shipments, you can use the **[<code>POST</code> api/rates](rates/post.md)** method to get the possible rate options.  If you would like to utilise one of these options, your workflow will be somewhat different.

1. Call **[<code>POST</code> api/rates](rates/post.md)** to get the available rate options. Each rate contains a *QuoteId*, retain this.
2. By some process of selection, identify the rate to use from (1) and get the *QuoteId*
3. Now call the current *api/shipments* method to generate a new shipment using the rates associated to the *QuoteId*. On the request message provide an additional property *QuoteId* with its value.

Note: When a *QuoteId* is not provided, the *Carrier* and *Service* properties are used to auto-rate and select the carrier/service to create against.  If either of this values are not provided the request will fail. The properties *Carrier* and *Service* can be wildcarded with '*' which will resolve to the first available rate, prioritising on cheapest first.

**Request**

    POST http://api.gosweetspot.com/api/shipments

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8



*Body*
``` json
{
    "QuoteId": "000-5465-65454-654564",
    "Origin": null,
    "Destination": {
        "Id": 0,
        "Name": "DestinationName",
        "Address": {
            "BuildingName": "",
            "StreetAddress": "DestinationStreetAddress",
            "Suburb": "Mascot",
            "City": "NSW",
            "PostCode": "2020",
            "CountryCode": "AU"
        },
        "Email": "destinationemail@email.com",
        "ContactPerson": "DestinationContact",
        "PhoneNumber": "123456789",
        "IsRural": false,
        "DeliveryInstructions": "Desinationdeliveryinstructions",
        "SendTrackingEmail": false
    },
    "Packages": [
        {
            "Name": "Custom",
            "Length": 20,
            "Width": 30,
            "Height": 50,
            "Kg": 10,
        }
    ],
    "Commodities": [
        {
            "HarmonizedCode": null,
            "Description": "Mens Socks",
            "UnitValue": 50.5,
            "Units": 10,
            "UnitKg": 1,
            "Country": "NZ",
            "Currency": "NZD"
        }
    ],
    "IsSaturdayDelivery": false,
    "IsSignatureRequired": true,
    "IsUrgentCouriers": false,
    "DutiesAndTaxesByReceiver": false,
    "RuralOverride": false,
    "DeliveryReference": "ORDER123",
    "PrintToPrinter": "false",
    "Outputs": null,
    "IncludeLineDetails": false,
    "HasDG": false,
    "DangerousGoods": null,
    "IncludeInsurance": false
}

```


**Response**

``` json
{
    "CarrierId": 96,
    "CarrierName": "FedEx",
    "IsFreightForward": false,
    "IsOvernight": false,
    "IsSaturdayDelivery": false,
    "IsRural": false,
    "HasTrackPaks": false,
    "Message": "Connote created and print queued.",
    "AddressLabelMessage": null,
    "AddressLabelError": null,
    "Errors": [],
    "SiteId": 4180,
    "Consignments": [
        {
            "Connote": "782847803802",
            "TrackingUrl": "http://gosweetspot.com/track/4180-782847803802",
            "Cost": 67.17,
            "CarrierType": 4,
            "IsSaturdayDelivery": false,
            "IsRural": false,
            "IsOvernight": false,
            "HasTrackPaks": false,
            "ConsignmentId": 6215945,
            "OutputFiles": null,
            "Items": null
        }
    ],
    "Downloads": [],
    "CarrierType": 4,
    "AlertPath": null,
    "Notifications": [],
    "HasSaturdayDeliveryLabel": false
}```
Base64 encoding string has been trimmed for presentation.
