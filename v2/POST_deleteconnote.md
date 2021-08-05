# Delete Consignment

    POST v2/deleteconnote

## Description
Delete an unprocessed consignment from the system.

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Parameters

The body of the message should be sent as an JSON array.

A JSON list of consignment numbers.

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
Http 409 - Max consignmnet limit 50 exceeded.

***

## Example
**Request**

    http://api.gosweetspot.com/v2/deleteconnote

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8
    Accept: application/json  

*Body*
``` json
[
  "SSPOT014115",
  "SSPOT014114",
  "SSPOT014113",
  "SSPOT014112"
]
```


**Response**
``` json
{
  "SSPOT014112": "Deleted",
  "SSPOT014113": "Deleted",
  "SSPOT014114": "Cannot be deleted. Already deleted.",
  "SSPOT014115": "Cannot be deleted. Already deleted."
}
```
