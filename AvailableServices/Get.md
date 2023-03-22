[![](obsolete-banner.png)](https://api-docs.gosweetspot.com/)

<div style="background-color: rgb(255, 243, 205); border: solid 1px rgb(255, 230, 156); border-radius: 0.375rem">
  This documentation is now obsolete. Please see our current documentation at <a href="https://api-docs.gosweetspot.com/">https://api-docs.gosweetspot.com/</a>.
</div>

# Available Services

    GET api/availableservices

## Description

Query for all available carriers and services for this account.

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.
***

## Parameters

- None.

## Return format
A JSON Object of available carriers. 

#### Root Object

* Carriers - Array of Carrier

#### Carrier
* AccountNumber - string
* CarrierId - integer
* CarrierName - string
* CarrierType - string
* Services - Array of strings

## Example
**Request**

    https://api.gosweetspot.com/api/availableservices

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

**Response**
```
{
  "Carriers": [
    {
      "CarrierId": 779,
      "CarrierName": "FedEx",
      "CarrierType": "FedEx",      
      "Services": [
        "All"
      ],
      "AccountNumber": "1234"
    },
    {
      "CarrierId": 432,
      "CarrierName": "Post Haste",
      "CarrierType": "PostHaste",
      "Services": [
        "Overnight",
        "Standard",
        "2 Day Inter Island"
      ],
      "AccountNumber": "1234"
    }
    ,
    {
      "CarrierId": 805,
      "CarrierName": "NZ Post",
      "CarrierType": "NZPost",
      "Services": [
        "Air Parcels",
        "Air Parcels Small",
        "Air Satchel Tracked",
        "Intl Courier",
        "Intl Courier (EX)"
      ],
      "AccountNumber": "1234"
    },
    {
      "CarrierId": 205,
      "CarrierName": "Mainstream AKL",
      "CarrierType": "Mainstream",
      "Services": [
        "Standard",
        "Standard m3+",
        "Bulk Freight"
      ],
      "AccountNumber": "1234"
    },
    {
      "CarrierId": 542,
      "CarrierName": "NZ Couriers",
      "CarrierType": "NZCouriers",
      "Services": [
        "Overnight",
        "Standard",
        "2 Day Inter Island"
      ],
      "AccountNumber": "1234"
    }
  ]
}
```
