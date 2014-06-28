# Submit New Order

    POST v2/neworder

## Description
Saves a new order or updates a pending order. If the packing slip number has already been processed, the message will be ignored.

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters
- **packingslipno** - Specify the unique order number from your source system, that was used as the packing slip no when the order was published
- **consignee** — recepient name
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
- **email** — email address for track & trace email, optional.

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

