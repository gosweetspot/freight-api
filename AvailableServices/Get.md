# Pickup Booking

    GET api/availableservices

## Description

Query for all available carriers and services for this account.

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters

- None.

## Return format
A JSON Object of available carriers. 

#### Root Object

* Carriers - Array of Carrier

#### Carrier
* AccountNumber - string
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
      "CarrierName": "FedEx",
      "CarrierType": "FedEx",
      "Services": [
        "All"
      ],
      "AccountNumber": "1234"
    },
    {
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
