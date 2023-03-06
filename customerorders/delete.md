# Delete Customer Orders

    DELETE api/customerorders

## Description
Delete an unprocessed customer orders from the system.

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.

***

## Parameters

A comma seperated list of orders numbers(packing slip numbers) to be deleted.

A maximum of 50 orders can be deleted per call.

## Return format
A JSON object, with orders number and assosiated outcome

Valid outcome states are
* Invalid packing slip number
* Cannot be deleted. Already deleted.
* Cannot be deleted. Already processed.
* Max delete limit is 50 packing slip numbers.

***

## Errors
Http 400 - No packing slip numbers supplied.
Http 409 - Max delete limit is 50 packing slip numbers.
***

## Example
**Request**
```
https://api.gosweetspot.com/api/customerorders?packingslipno=test%231234,test%231235,test%231236
```
*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8
    Accept: application/json  
    
**Response**
``` json
{
  "test#1234": "Cannot be deleted. Already processed.",
  "test#1235": "Cannot be deleted. Already deleted.",
  "test#1236": "Deleted.",
}
```
