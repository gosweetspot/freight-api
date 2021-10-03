# Delete Stock Size

    DELETE api/stocksizes

## Description
Delete a stock size from the system.

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Parameters

A comma seperated list of stock size ids to be deleted.

## Return format
A JSON object array, with stock size id and assosiated outcome

Valid outcome states are
* Invalid Package Stock.
* Cannot be deleted. 
* Deleted. 

***

## Example
**Request**
```
http://api.gosweetspot.com/api/stocksizes?id=159872,159873,159874
```
*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8
    Accept: application/json  
    
**Response**
``` json
{
    "159872": "Deleted",
    "159873": "Deleted",
    "159874": "Deleted"
}
```
