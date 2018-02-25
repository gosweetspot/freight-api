# Pickup Booking

    POST api/bookpickup

## Description
Query to book a driver to pick up from your location. They will make a best effort attempt to pick up on the same day - however, if you book after 2PM it is recommended that you book again in the morning if they don't pick up on the same day.

This query is supported for the following companies:

- Castle Parcels

- Post Haste Couriers

- New Zealand Couriers

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters
- **Carrier** - Specify the carrier to book a pickup for. Supported values: "CastleParcel", "PostHaste" and "NZCouriers".

## Return format
A string indicating whether or not the pickup request was lodged successfully.

## Example
**Request**

    http://api.gosweetspot.com/api/bookpickup

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8



*Body*
``` json
{
  "Carrier": "PostHaste"
}
```


**Response**
``` 
"Success. Your booking has been accepted. #NC12345678"
```
