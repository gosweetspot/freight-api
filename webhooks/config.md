[![](../obsolete-banner.png)](https://api-docs.gosweetspot.com/)

# Webhooks

    To configure you need to use https://ship.gosweetspot.com/developer/webhooks

## Description
GSS is able to provide feedback to your site using webhooks for certain action triggers.
Actions that can be subscibed to include:
- Shipment created
- Shipment pickup registered by courier
- Shipment delivery registered by courier
- Shipment tracking activity update(**coming soon**, including events into the post body)

Once you have configured the URL, we will post events to that URL as they become available.

***
## Debugging

Webhooks can be hard to debug. You can use tools like http://requestb.in to view data sent by GSS.
***
## Caveats

Keep in mind that your servers need to be robust enough to handle the post requests and return a valid response code in a timely manner.

Our webhooks have a high limit timeout of 10 seconds. If a response isn't received in 10 seconds, the request will be terminated and queued for retry.

In case a failed response is received, the request will be re-queued with a 10 minute delay. Every failed attempt, extends the next retry window by 10 minutes.  After 10 retries we will abort the batch.

Also, ensure your end is able to receive the same input multiple times. A shipment can have 3 posts, one for created, one for picked, and one for delivered.  They could be posted in any order.

***

## Data format
<table>
        <tr>
            <td valign="top">return<br />struct</td>
            <td>
              a list of up to 50 shipments
              <table>
                  <tr>
                      <td>ConsignmentNo</td>
                      <td>string</td>
                      <td>shipment consignment number</td>
                  </tr>
                  <tr>
                      <td>Consignee</td>
                      <td>string</td>
                      <td>shipment consignee name</td>
                  </tr>
                  <tr>
                      <td>ManualTicket</td>
                      <td>boolean</td>
                      <td>False when the shipment originated from an external orders source, such as an integrated system or shopfiy. True when the ticket was create using the GSS UI.</td>
                  </tr>
                  <tr>
                      <td>PackingSlipNo</td>
                      <td>string</td>
                      <td>Order/packing slip number for integrated orders or Delivery Reference when created using the GSS UI.</td>
                  </tr>
                  <tr>
                      <td>Picked</td>
                      <td>date time</td>
                      <td>date/time goods picked by courier. Time local to pickup origin</td>
                  </tr>
                  <tr>
                      <td>Delivered</td>
                      <td>date time</td>
                      <td>date/time goods delivered to receiver. Time local to delivery address</td>
                  </tr>
                  <tr>
                      <td>Status</td>
                      <td>string</td>
                      <td>latest courier tracking status of the shipment</td>
                  </tr>
                  <tr>
                      <td>TotalCost</td>
                      <td>decimal</td>
                      <td>total cost of the shipment excluding taxes where applicable</td>
                  </tr>
                  <tr>
                      <td>Tracking</td>
                      <td>string</td>
                      <td>track and trace url for live tracking of the order</td>
                  </tr>
              </table>                      
            </td>
        </tr>
    </table>
    
***

## Example
The webhook will do a POST to your url with a JSON data packet as below.

**POST Body**
``` json
[
    {
        "ConsignmentNo": "XYV00010931",
        "Status": "Delivered to PTL FRONT DOOR",
        "Picked": "2016-03-23T10:18:44",
        "Delivered": "2016-03-29T09:12:49",
        "Tracking": "http://gosweetspot.com/track/XYV00010931",
        "TotalCost": 16.34,
        "CreatedUtc": "2016-03-22T21:56:58.007",
        "PackingSlipNo": "",
        "ManualTicket": true,
        "Consignee": "TITAHI BAY MARLINS RLC"
    },
    {
        "ConsignmentNo": "XYV00010923",
        "Status": "Delivered to KARL",
        "Picked": "2016-03-30T11:19:23",
        "Delivered": "2016-04-01T15:31:02",
        "Tracking": "http://gosweetspot.com/track/XYV00010923",
        "TotalCost": 12.74,
        "CreatedUtc": "2016-03-17T01:34:14.903",
        "PackingSlipNo": "",
        "ManualTicket": true,
        "Consignee": "VERONICA HENDRIKSE"
    },
    {
        "ConsignmentNo": "XYV00010938",
        "Status": "Delivered to SAM",
        "Picked": "2016-04-06T13:40:51",
        "Delivered": "2016-04-07T11:07:58",
        "Tracking": "http://gosweetspot.com/track/XYV00010938",
        "TotalCost": 12.66,
        "CreatedUtc": "2016-04-02T22:27:33.177",
        "PackingSlipNo": "P133138809",
        "ManualTicket": false,
        "Consignee": "SAM PEMBERTON CIVIL LTD"
    },
    {
        "ConsignmentNo": "XYV00010953",
        "Status": "Delivered to [AUTHORITY TO LEAVE]",
        "Picked": "2016-04-12T13:11:29",
        "Delivered": "2016-04-13T14:45:21",
        "Tracking": "http://gosweetspot.com/track/XYV00010953",
        "TotalCost": 18.3,
        "CreatedUtc": "2016-04-11T22:10:46.157",
        "PackingSlipNo": "P133372665",
        "ManualTicket": false,
        "Consignee": "CATHERINE MCGRORY"
    },
    {
        "ConsignmentNo": "XYV00010932",
        "Status": "Delivered to PETER",
        "Picked": "2016-03-31T09:51:14",
        "Delivered": "2016-04-02T12:08:41",
        "Tracking": "http://gosweetspot.com/track/XYV00010932",
        "TotalCost": 68.2,
        "CreatedUtc": "2016-03-29T23:31:12.597",
        "PackingSlipNo": "",
        "ManualTicket": true,
        "Consignee": "PETER WHITE"
    }
]

```
