[![](../obsolete-banner.png)](https://api-docs.gosweetspot.com/)

# Get Order Status

    GET order/[packingslipno]

## Description
Gets the current status of an order

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Parameters
- **packingslipno** - Specify the unique order number from your source system, that was used as the packing slip no when the order was published

***

## Return format
A JSON object with order status:

- **packingslipno** - unique order number or packing slip number from your system
- **consignee** - receipient name
- **status** - current status of order, options PENDING/PICKED/DELIVERED
- **ticketnumber** - unique consignment number
- **trackingurl** - track and trace website url
- **picked** - localised to pickup timezone, pickup time stamp. *null* if not picked yet
- **delivered** - localised to destintation timezone, delivery time stamp. *null* if not delivered yet
- **ticketprinteddate** - localised to origin timezone, when the shipment ticket was created. *null* if not created yet
- **ticketprintedby** - username of the user, creating the ticket
- **ticketdeleteddate** - localised to NZ timezone, date and time when the ticket was deeted, if deleted. *null* if not deleted
- **ticketdeletedby** - username of the user, deleting the ticket


***

## Example
**Request**

    https://api.gosweetspot.com/v2/order/SSORDER5840
    

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

    

**Response** 
``` json
{
  "packingslipno": "SSORDER5840",
  "consignee": "PHOTO DREAMS LIMITED",
  "status": "DELIVERED",
  "ticketnumber": "SSPOT012671",
  "trackingurl": "http://gosweetspot.com/track/4180-SSPOT012671",
  "picked": "2014-06-03T08:40:00",
  "delivered": "2014-06-03T14:46:45",
  "ticketprinteddate": "2014-06-03T08:30:00",
  "ticketprintedby": "abc@accompany.co.nz",
  "ticketdeleteddate": null,
  "ticketdeletedby": null
}
```

