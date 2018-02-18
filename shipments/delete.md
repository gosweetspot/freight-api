# Delete Consignment

    DELETE api/shipments

## Description
Delete an unprocessed consignment from the system.

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters

A comma seperated list of consignment numbers to be deleted.

A maximum of 50 consignments can be deleted per call.

## Return format
A JSON object array, with consignment number and assosiated outcome

Valid outcome states are
* Invalid ticket number
* Cannot be deleted. Already deleted.
* Cannot be deleted. Already delivered.
* Cannot be deleted. Already in transit.
* Cannot be deleted. Already manifested.

***

## Errors
Http 409 - Max consignment limit 50 exceeded.

***

## Example
**Request**
```
http://api.gosweetspot.com/api/shipments?id="SSPOT014115","SSPOT014114","SSPOT014113","SSPOT014112"
```
*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8
    Accept: application/json  
    
**Response**
``` json
{
  "SSPOT014112": "Deleted",
  "SSPOT014113": "Deleted",
  "SSPOT014114": "Cannot be deleted. Already deleted.",
  "SSPOT014115": "Cannot be deleted. Already deleted."
}
```
