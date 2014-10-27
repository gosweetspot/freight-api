# Reprint

    POST ratesquery/reprint

## Description
Requeues the consignment for printing.

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters
- **consignmentno** - consignment number to be re-printed

## Return format
A string text of response message.

***

## Errors
Error messages will range in the below
- Not a valid consignment number
- Print job sent
- API Key not associated with a valid printer

***

## Example
**Request**

    http://api.gosweetspot.com/ratesqueryv1/reprint?consignmentno=ABC123

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8



**Response**
``` json
Print job sent

```
