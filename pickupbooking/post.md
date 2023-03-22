[![](../obsolete-banner.png)](https://api-docs.gosweetspot.com/)

# Pickup Booking

    POST api/bookpickup

## Description
Query to book a driver to pick up from your location. They will make a best effort attempt to pick up on the same day - however, if you book after 2PM it is recommended that you book again in the morning if they don't pick up on the same day. Each call to this endpoint will ping the driver, so do not call this endpoint excessively.

This query is supported for the following companies:

- Castle Parcels

- Post Haste Couriers

- New Zealand Couriers

- Mainstream Freight

- Fedex

- New Zealand Post

- First Global Logistics

### Mainstream Freight
When booking for Mainstream Freight you must manifest the consignments first using this [endpoint]( https://github.com/gosweetspot/freight-api/blob/master/v2/POST_publishmanifest.md).

### TIL Freight
TIL Freight cannot be booked through this endpoint. However, when you manifest TIL Freight consignments it will be booked at the same time. Use the above link for manifesting.

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Parameters
- **Carrier** - Specify the carrier to book a pickup for. Supported values: "CastleParcel", "PostHaste", "NZCouriers", "Mainstream", "FedEx", "NZPost", "FirstGlobal". This value can be obtained from the AvailableServices endpoint. Mandatory field.
- **Consignments** - An array of consignment number strings representing the consignments to be picked up. This field is mandatory when booking for *Mainstream*, *FedEx* and *NZPost*. You can include it for other carriers but it will do nothing.
- **TotalKg** - A decimal number indicating the total weight of parcels. This field is mandatory when booking for *FirstGlobal*. You can include it for other carriers but it will do nothing.
- **Parts** - An integer number indicating the total number of parcels. This field is mandatory when booking for *FirstGlobal*. You can include it for other carriers but it will do nothing.

## Return format
A string indicating whether or not the pickup request was lodged successfully. The HTTP status code will be 200 if successful.

## Example
**Request**

    https://api.gosweetspot.com/api/bookpickup

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8



*Body (for FedEx, NZPost, Mainstream)
``` json
{
  "Carrier": "FedEx",
  "Consignments":["789663088020"]
}
```

*Body (for FirstGlobal)
``` json
{
  "Carrier": "FirstGlobal",
  "TotalKg": 1.5,
  "Parts": 1
}
```

*Body (for others)
``` json
{
  "Carrier": "PostHaste"
}
```


**Response**
``` 
"Success. Your booking has been accepted. #NC12345678"
```
