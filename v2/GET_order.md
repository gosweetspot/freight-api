# Pending Orders

    GET order/[packingslipno]

## Description
Gets the current status of an order

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters
- **packingslipno** - Specify the unique order number from your source system, that was used as the packing slip no when the order was published

***

## Return format
A JSON object with order status:

- **packingslipno** � unique order number or packing slip number from your system
- **consignee** � receipient name
- **status** � current status of order, options PENDING/PICKED/DELIVERED
- **ticketnumber** � unique consignment number
- **trackingurl** � track and trace website url
- **picked** � localised to pickup timezone, pickup time stamp. *null* if not picked yet
- **delivered** � localised to destintation timezone, delivery time stamp. *null* if not delivered yet

***

## Example
**Request**

    http://api.gosweetspot.com/v2/order/SSORDER5840
    

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

    

**Response** 
``` json
{"packingslipno":"SSORDER5840","consignee":"PHOTOSHACK LIMITED","Status":"DELIVERED","ticketnumber":"SSPOT012671","trackingurl":"http://sweetspotgroup.co.nz/track/4180/SSPOT012671","Picked":"2014-06-03T08:40:00","Delivered":"2014-06-03T14:46:45"}
```

