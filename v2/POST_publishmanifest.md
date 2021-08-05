# Publish Manifest

    POST v2/publishmanifest

## Description
This function accepts as input all pending consignments that are ready for manifesting. These consignmnets are manifested to their respective carriers and a summary manifest report is
returned as a PDF.

This method will accept consignment numbers as an array.

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Parameters

The body of the message should be sent as an JSON array.

A JSON list of consignment numbers.

***

## Return format
JSON object array per manifest generated. This is in a key/value pair collection, with the manifest number being the key and value is the base64 encoded byte stream of the PDF.

***

## Errors
HTTP 400.Bad request - when no consignment numbers supplied or when invalid consignment numbers supplied.

***

## Example
**Request**

    http://api.gosweetspot.com/v2/publishmanifest

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8


*Body*
``` json
[
	"4WD0002186",
	"4WD0002187",
	"4WD0002188"
]
```


**Response** 
A JSON object array of order and save status.

``` json
{
  "CZA0001": "JVBERi0xLjcgCiXi48/TIAoxIDAgb2JqIAo8PCAKL1R5cGUgL0NhdGFsb2cgCi9QYWdlcyAyIDAgUiAKL1BhZ2VNb2RlIC9Vc2VOb25lIAovVmlld2VyUHJlZmVyZW5jZXMgPDwgCi9GaXRXaW5kb3cgdHJ1ZSAKL1BhZ2VMYXlvdXQgL1NpbmdsZVBhZ2UgCi9Ob25GdWxsU2NyZWVuUGFnZU1vZGUgL1VzZU5vbmUgCj4+IAo+PiAKZW5kb2JqIAo1IDAgb2JqIAo8PCAKL0xlbmd0aCAxMjAzIAovRmlsdGVyIFsgL0ZsYXRlRGVjb2RlIF0gCj4+IApzdHJlYW0KeJylV9ly4kYUfddX9MM8kIqRu1u9SH6TgbEJZolghkpSedCA7CFl0AzGmcrf5/aiDQmJSAKMDAwMDAzNTk3NSAwMDAwMCBuIAowMDAwMDE2Njc3IDAwMDAwIG4gCjAwMDAwMzYzNzUgMDAwMDAgbiAKMDAwMDAzNjY1MSAwMDAwMCBuIAowMDAwMDE3MzYyIDAwMDAwIG4gCjAwMDAwMzY2OTQgMDAwMDAgbiAKMDAwMDAzNjczNCAwMDAwMCBuIAowMDAwMDM2NzcxIDAwMDAwIG4gCnRyYWlsZXIgCjw8IAovU2l6ZSAyNCAKL1Jvb3QgMSAwIFIgCi9JbmZvIDIzIDAgUiAKPj4gCnN0YXJ0eHJlZiAKMzY4NTkgCiUlRU9GDQo=",
  "CZA0002": "sqFS1If3XOXc2+3CMLwR+DnM4o2e32L0fHFMRfRg0N81Icfp9gVqO9jgY6Js3YOgPjh/AHveuhPQG4dylDf89He4VLoq1dnad7GgYt5tmDv8kXBXE+t+dLNb7NFSgKX82LV3ufLkrl+aVXfqsXv2plAIMlduCBEMVq371cOsVErEMEc4lrtndsA+S5Fq2enN0gPh/SU/IRWfzmjlWNgQjFT3w1QH6tLMPfs/ApUhFzDpVFNZFGySXZ/J8eMzQINXeASXuU7c98jELIyGCP9hrK4/JEkp+W39IQ+HpPdy9dTZtqkBQotaXtSOLFuxrmb0/iwe07eTmj2vv+SHO8ymyoDDIqtzPKW+DWmxW6yrZgkmGqThOKWnCoQ2OTn9fs9xBiTiouBsee3uRg0m6PwMCBuIAowMDAwMDM0ODA1IDAwMDAwIG4gCjAwMDAwMzQ4OTcgMDAwMDAgbiAKMDAwMDAzNTA3NiAwMDAwMCBuIAowMDAwMDM1MjUxIDAwMDAwIG4gCjAwMDAwMDE0ODAgMDAwMDAgbiAKMDAwMDAzNTY1MSAwMDAwMCBuIAowMDAwMDM1OTMyIDAwMDAwIG4gCjAwMDAwMDIxNTUgMDAwMgbi"
}
```

Base64 pdf data has been trimmed for presentation.
