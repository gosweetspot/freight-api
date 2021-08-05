# Labels

    POST api/labels/enqueue

## Description
Queues the provided image file for printing via the print agent.

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Parameters
<table>
    <tr>
      <td>struct</td>
      <td>
          <table>
                <tr>
                  <th>Field</th>
                  <th>Description</th>
                </tr>
                  <tr>
                      <td valign="top">**copies**</td>
                      <td>
                        number of copies to print
                      </td>
                  </tr>
                  <tr>
                    <td>image</td>
                    <td>byte array of image file. Supported format is *png*. The file size should be 1350px by 1175px</td>
                  </tr>
                  <tr>
                    <td>printtoprinter</td>
                    <td>optional value. If not supplied, the access_key profile printer is used</td>
                  </tr>
          </table>
    </td>
  </tr>
</table>
## Return format
A string text of response message.

***

## Errors
Error messages will range in the below
- Supplied document stream does not represent an image.
- Print job sent
- Print job queued
- API Key not associated with a valid printer

***

## Example
**Request**

    https://api.gosweetspot.com/api/labels/en

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

*Body*
``` json
    {
    	"Copies": 1,
    	"Image": "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUN1akNDQWlPZ0F3SUJBZ0lKQU02VEt0b09KSWpGTUEwR0NT",
      "PrintToPrinter" : "SMITH-PC >> ZDESIGNER LP 2844 (3227)"
    }
```

**Response**
``` json
Print job sent

```
