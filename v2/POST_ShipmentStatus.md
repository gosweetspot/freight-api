[![](../obsolete-banner.png)](https://api-docs.gosweetspot.com/)

# Shipment Status

    POST v2/shipmentstatus

## Description
This method returns the current status of the shipment, including line by line events for pickup, handling, to delivery.

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
A JSON object array, with consignment number and assosiated events
- **consignmentno** : the queried shipment
- **status** : current status of shipment
- **picked** : date and time picked from sender. Local time at pickup address. Blank when not picked yet.
- **delivered** : date and time delivered to receiver. Local time at delivery address. Blank when not delivered yet.
- **tracking** : tracking url
- **events** : an array of line level events for all pieces in the shipment

**event**
- **eventdate**: date and time of event. Local to region where it occurred.
- **code**: event status code, CR - Created, INTL - International Transit - CUST - Customs Cleared, COUR - Courier picked up, COURU - courier update, DEL - Delivered
- **description**: event description
- **location**: locality of where event took place
- **part** : shipment item identifier
***

## Errors
HTTP 400.Bad request - when no consignment numbers supplied or when invalid consignment numbers supplied.

***

## Example
**Request**

    https://api.gosweetspot.com/v2/shipmentstatus

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8


*Body*
``` json
[
  "WRR1406658",
  "WRR1406659"
]
```


**Response**
A JSON object array of order and save status.

``` json
[
  {
    "ConsignmentNo": "WRR1406658",
    "Status": "Delivered to SANDRA",
    "Picked": "2014-11-04T19:07:00.36",
    "Delivered": "2014-11-17T08:55:53",
    "Tracking": "http:\/\/track.gosweetspot.com\/1218110-WRR1406658",
    "Events": [
      {
        "EventDT": "2014-11-03T13:20:00",
        "Code": "CR",
        "Description": "Tracking number allocated & order ready",
        "Location": "NSW",
        "Part": "WRR1406658001"
      },
      {
        "EventDT": "2014-11-04T17:06:00",
        "Code": "INTL",
        "Description": "International transit to destination country ",
        "Location": "AU, SYD",
        "Part": "WRR1406658001"
      },
      {
        "EventDT": "2014-11-14T09:47:00",
        "Code": "CUST",
        "Description": "Customs cleared",
        "Location": "NZ",
        "Part": "WRR1406658001"
      },
      {
        "EventDT": "2014-11-14T13:20:00",
        "Code": "COURU",
        "Description": "Scan activity. Imported on runsheet AVWRR14315",
        "Location": "Auckland",
        "Part": "WRR1406658001"
      },
      {
        "EventDT": "2014-11-15T07:42:00",
        "Code": "COURU",
        "Description": "Scan activity. Scanned into Palmerston North",
        "Location": "Palmerston Nth",
        "Part": "WRR1406658001"
      },
      {
        "EventDT": "2014-11-17T06:11:00",
        "Code": "COURU",
        "Description": "On courier vehicle for delivery",
        "Location": "Palmerston Nth",
        "Part": "WRR1406658001"
      },
      {
        "EventDT": "2014-11-17T08:55:00",
        "Code": "DEL",
        "Description": "Delivered to SANDRA",
        "Location": "Palmerston Nth",
        "Part": "WRR1406658001"
      }
    ]
  },
  {
    "ConsignmentNo": "WRR1406659",
    "Status": "Delivered to ANNA",
    "Picked": "2014-11-04T19:07:00.36",
    "Delivered": "2014-11-14T15:02:31",
    "Tracking": "http:\/\/track.gosweetspot.com\/1218110-WRR1406659",
    "Events": [
      {
        "EventDT": "2014-11-03T13:20:00",
        "Code": "CR",
        "Description": "Tracking number allocated & order ready",
        "Location": "NSW",
        "Part": "WRR1406659001"
      },
      {
        "EventDT": "2014-11-04T17:06:00",
        "Code": "INTL",
        "Description": "International transit to destination country ",
        "Location": "AU, SYD",
        "Part": "WRR1406659001"
      },
      {
        "EventDT": "2014-11-14T09:47:00",
        "Code": "CUST",
        "Description": "Customs cleared",
        "Location": "NZ",
        "Part": "WRR1406659001"
      },
      {
        "EventDT": "2014-11-14T12:11:00",
        "Code": "COURU",
        "Description": "Scan activity. Scanned into Auckland",
        "Location": "Auckland",
        "Part": "WRR1406659001"
      },
      {
        "EventDT": "2014-11-14T13:20:00",
        "Code": "COURU",
        "Description": "Scan activity. Imported on runsheet AVWRR14315",
        "Location": "Auckland",
        "Part": "WRR1406659001"
      },
      {
        "EventDT": "2014-11-14T13:34:00",
        "Code": "COURU",
        "Description": "On courier vehicle for delivery",
        "Location": "Auckland",
        "Part": "WRR1406659001"
      },
      {
        "EventDT": "2014-11-14T15:02:00",
        "Code": "DEL",
        "Description": "Delivered to ANNA",
        "Location": "Auckland",
        "Part": "WRR1406659001"
      }
    ]
  }
]

```
