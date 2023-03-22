[![](../obsolete-banner.png)](https://api-docs.gosweetspot.com/)

# Shipments

    GET https://api.gosweetspot.com/api/shipments

## Description
Get status updates for shipments

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Parameters
<table>
  <tr>
    <th colspan="2">Parameters</th>
  </tr>
  <tr>
    <td>shipments</td>
    <td>comma separated list of consignment numbers to apply filter on</td>
  </tr>
  <tr>
    <td>ordernumbers</td>
    <td>comma separated list of order numbers to apply filter on</td>
  </tr>
  <tr>
    <td>lastupdateminutc</td>
    <td>UTC formatted date and time to filter the shipments on. This field is for earliest date</td>
  </tr>
  <tr>
    <td>lastupdatemaxutc</td>
    <td>UTC formatted date and time to filter the shipments on. This field is for latest date</td>
  </tr>
</table>
* when the *shipments* or *ordernumbers* values is provided, the *lastupdateminutc* & *lastupdatemaxutc* values are ignored.


***

## Return format
<table>
        <tr>
            <td valign="top">return<br />struct</td>
            <td>
                paged result set
                <table>
                    <tr>
                        <td>page</td>
                        <td>current page number</td>
                    </tr>
                    <tr>
                        <td>pages</td>
                        <td>total number of pages</td>
                    </tr>
                    <tr>
                        <td>pagesize</td>
                        <td>how many records returned per result set</td>
                    </tr>
                    <tr>
                        <td valign="top">results[]</td>
                        <td>
                            a list of up to 250 shipments
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
                                    <td>CreatedUtc</td>
                                    <td>datetime</td>
                                    <td>when the shipment has been created</td>
                                </tr>
                                <tr>
                                    <td>CreatedBy</td>
                                    <td>string</td>
                                    <td>who created the shipment</td>
                                </tr>
                                <tr>
                                    <td>Tracking</td>
                                    <td>string</td>
                                    <td>track and trace url for live tracking of the order</td>
                                </tr>
                                <tr>
                                    <td>OriginZone
                                    </td>
                                    <td>string</td>
                                    <td>Short code for the origin zone of the consignment.</td>
                                </tr>
                                <tr>
                                    <td>DestinationZone</td>
                                    <td>string</td>
                                    <td>Short code for the destination zone of the consignment.</td>
                                </tr>
                                <tr>
                                    <td>
                                        CostCentre
                                    </td>
                                    <td>
                                        string
                                    </td>
                                    <td>Name of the associated cost centre.</td>
                                </tr>
                                <tr>
                                    <td>Carrier</td>
                                    <td>string</td>
                                    <td>Carrier name.</td>
                                </tr>
                                <tr>
                                    <td>DeliveryInstructions</td>
                                    <td>string</td>
                                    <td>Instructions for delivery driver.</td>
                                </tr>
                                <tr>
                                    <td>IsSaturdayDelivery</td>
                                    <td>bool</td>
                                    <td>If delivery will be attempted on Saturday, when applicable.</td>
                                </tr>
                                <tr>
                                    <td>IsRuralDelivery</td>
                                    <td>bool</td>
                                    <td>If the destination has been determined to be rural.</td>
                                </tr>
                                <tr>
                                    <td>IsPOBox</td>
                                    <td>bool</td>
                                    <td>If the destination has been determined to be a PO Box, ParcelPod, etc.</td>
                                </tr>
                                <tr>
                                    <td>CustomerReference</td>
                                    <td>string</td>
                                    <td>Reference number.</td>
                                </tr>
                                <tr>
                                    <td>TotalCubic</td>
                                    <td>decimal</td>
                                    <td>Sum of cubic volume of all items in this consignment. Denoted in m3.</td>
                                </tr>
                                <tr>
                                    <td>TotalKg</td>
                                    <td>decimal</td>
                                    <td>Sum of weight of all items in this consignment. Denoted in kg.</td>
                                </tr>
                                <tr>
                                    <td>Parts</td>
                                    <td>int</td>
                                    <td>Number of items in this consignment.</td>
                                </tr>
                                <tr>
                                    <td>IsSignatureRequired</td>
                                    <td>bool</td>
                                    <td>True if the delivery driver needs to collect a signature.</td>
                                </tr>
                                <tr>
                                    <td>IsFreightForward</td>
                                    <td>bool</td>
                                    <td>True if this is a freight-forward consignment.</td>
                                </tr>
                                <tr>
                                    <td>Parts</td>
                                    <td>int</td>
                                    <td>Number of items in this consignment.</td>
                                </tr>
                                <tr>
                                    <td>Origin</td>
                                    <td>Struct</td>
                                    <td>
                                        <table>
                                            <tr>
                                                <td>Building</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Address</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Name</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Suburb</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Town</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>PostalCode</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Country</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>ContactName</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>ContactPhone</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Email</td>
                                                <td>string</td>
                                            </tr>
                                        </table>
                                </tr>
                                <tr>
                                    <td>Destination</td>
                                    <td>Struct</td>
                                    <td>
                                        <table>
                                            <tr>
                                                <td>Building</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Address</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Name</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Suburb</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Town</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>PostalCode</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Country</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>ContactName</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>ContactPhone</td>
                                                <td>string</td>
                                            </tr>
                                            <tr>
                                                <td>Email</td>
                                                <td>string</td>
                                            </tr>
                                        </table>
                                </tr>
				    <tr>
                                    <td>Items</td>
                                    <td>Struct</td>
                                    <td>
                                        <table>
                                            <tr>
                                                <td>PartNo</td>
                                                <td>int</td>
						<td>The part number of the consignment - e.g. 1, 2 , 3 etc.</td>
                                            </tr>
                                            <tr>
                                                <td>LengthCm</td>
                                                <td>decimal</td>
						<td> </td>
                                            </tr>
                                            <tr>
                                                <td>WidthCm</td>
                                                <td>decimal</td>
						<td> </td>
                                            </tr>
                                            <tr>
                                                <td>HeightCm</td>
                                                <td>decimal</td>
						<td> </td>
                                            </tr>
                                            <tr>
                                                <td>WeightKg</td>
                                                <td>decimal</td>
						<td> </td>
                                            </tr>
                                            <tr>
                                                <td>PackageName</td>
                                                <td>string</td>
						<td>Name of the package - e.g. GSS A4 Satchel.</td>
                                            </tr>
                                            <tr>
                                                <td>Charge_LineTotal</td>
                                                <td>decimal</td>
						<td>Total charge determined for this item at the time of consignment creation.</td>
                                            </tr>
                                            <tr>
                                                <td>Charge_MarkedUpLineTotal</td>
                                                <td>decimal</td>
						<td>Total charge with mark up (if defined) determined for this item at the time of consignment creation.</td>
                                            </tr>
                                            <tr>
                                                <td>PickedAt</td>
                                                <td>Nullable DateTime</td>
						<td>Date and time this item was picked up - will be null if not yet picked up.</td>
                                            </tr>
                                            <tr>
                                                <td>DeliveredAt</td>
                                                <td>Nullable DateTime</td>
						<td>Date and time this item was delivered - will be null if not yet delivered.</td>
                                            </tr>
                                            <tr>
                                                <td>RatingCode</td>
                                                <td>string</td>
						<td>The rating code of this item.</td>
                                            </tr>
                                        </table>
                                </tr>
                                <tr>
                                    <td>Events</td>
                                    <td>return[] <br />struct</td>
                                    <td>
                                        a list of track and trace events per part of the shipment
                                        <table>
                                            <tr>
                                                <td>Part</td>
                                                <td>string</td>
                                                <td>shipment part number</td>
                                            </tr>
                                            <tr>
                                                <td>Code</td>
                                                <td>string</td>
                                                <td>
                                                    event milestone code.<br />
                                                    <ul>
                                                        <li>CR - Label created</li>
							<li>INTL - International Transit</li>
							<li>CUST - Customs Clearance Processing</li>
                                                        <li>COUR - Collected from sender/in delivery(final mile) courier network</li>
                                                        <li>COURU - Courier status update provided</li>
                                                        <li>EXCP - delivery exception, or service update</li>
							<li>DEL - Delivery completed</li>
                                                    </ul>
                                                </td>
                                            </tr>
                                            <tr>
                                                <td>Description</td>
                                                <td>string</td>
                                                <td>Event description</td>
                                            </tr>
                                            <tr>
                                                <td>eventDt</td>
                                                <td>date time</td>
                                                <td>date/time of event/activity local to location of event</td>
                                            </tr>
                                            <tr>
                                                <td>Location</td>
                                                <td>string</td>
                                                <td>Area/locality of where the event occurred</td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                            </table>
                        </td>
                    </tr>
                </table>
            </td>
        </tr>
    </table>
***

## Example
**Request**

    GET https://api.gosweetspot.com/api/shipments?lastupdateminutc=2015-08-13%2008:15:13&page=1&shipments=ABC0001,ABC0002,ABC20303

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8


**Return** __shortened for example purpose__
``` json
{
  "Page": 1,
  "PageSize": 2,
  "Pages": 1,
  "Results": [
    {
      "OriginZone": "AKLW",
      "DestinationZone": "AKL",
      "Origin": {
        "Building": "**** TEST ********* TEST *****",
        "Address": "**** TEST ********* TEST *****",
        "Name": "TEST ACCOUNT",
        "Suburb": "MT ROSKILL",
        "Town": "AUCKLAND",
        "PostalCode": "0600",
        "Country": "NZ",
        "ContactName": "TEST",
        "ContactPhone": "123456",
        "Email": ""
      },
      "Destination": {
        "Building": "GOSWEETSPOT",
        "Address": "102 STATION ROAD EAST",
        "Name": "DON ZHANG",
        "Suburb": "PENROSE",
        "Town": "AUCKLAND",
        "PostalCode": "1061",
        "Country": "NZ",
        "ContactName": "RECEIVER NAME",
        "ContactPhone": "212563080",
        "Email": ""
      },
      "CostCentre": "TEST COST CENTRE ONE",
      "Carrier": "Post Haste - AKL - 2011",
      "DeliveryInstructions": "",
      "IsSaturdayDelivery": false,
      "IsRuralDelivery": false,
      "IsPOBox": false,
      "CustomerRef": "#1029",
      "TotalCubic": 0.022,
      "TotalKg": 5.5,
      "Parts": 1,
      "IsSignatureRequired": true,
      "IsFreightForward": false,
      "ManifestedAt": null,
      "Items": [
        {
          "PartNo": 1,
          "LengthCm": 47,
          "WidthCm": 47,
          "HeightCm": 10,
          "WeightKg": 5.5,
          "PackageName": "SMALL BOX",
          "Charge_LineTotal": 9.98,
          "PickedAt": null,
          "DeliveredAt": null,
          "RatingCode": "MS"
        }
      ],
      "ConsignmentNo": "APD00020626",
      "Status": null,
      "Picked": null,
      "Delivered": null,
      "Tracking": "https:\/\/gosweetspot.com\/track\/108633-APD00020626",
      "Events": [
      	{
      		"EventDT": "2019-10-10T22:57:57.047",
      		"Code": "CR",
      		"Description": "Tracking number allocated & order ready",
      		"Location": "AUCKLAND",
      		"Part": "APD0002062601"
      	},
      	{
      		"EventDT": "2019-10-10T22:57:57.047",
      		"Code": "COUR",
      		"Description": "Picked up",
      		"Location": "PENROSE (AKL)",
      		"Part": "APD0002062601"
      	},
      	{
      		"EventDT": "2019-10-10T22:57:57.047",
      		"Code": "COURU",
      		"Description": "On courier vehicle for delivery",
      		"Location": "Glenfield Industrial Wairau Valley (AKL)",
      		"Part": "APD0002062601"
      	},
      	{
      		"EventDT": "2019-10-10T22:57:57.047",
      		"Code": "DEL",
      		"Description": "Delivered to ANDREW",
      		"Location": "Glenfield Industrial Wairau Valley (AKL)",
      		"Part": "APD0002062601"
      	}
      ],
      "ManifestNumber": "ABCD",
      "TotalCost": 9.98,
      "CreatedUtc": "2019-10-10T22:57:57.047",
      "PackingSlipNo": "#1029",
      "ManualTicket": false,
      "Consignee": "RECEIVER NAME"
    },
    {
      "OriginZone": "AKLW",
      "DestinationZone": "AKL",
      "Origin": {
        "Building": "**** TEST ********* TEST *****",
        "Address": "**** TEST ********* TEST *****",
        "Name": "TEST ACCOUNT",
        "Suburb": "MT ROSKILL",
        "Town": "AUCKLAND",
        "PostalCode": "0600",
        "Country": "NZ",
        "ContactName": "TEST",
        "ContactPhone": "123456",
        "Email": ""
      },
      "Destination": {
        "Building": "GOSWEETSPOT",
        "Address": "101 STATION ROAD EAST",
        "Name": "RECEIVER NAME",
        "Suburb": "PENROSE",
        "Town": "AUCKLAND",
        "PostalCode": "1061",
        "Country": "NZ",
        "ContactName": "RECEIVER NAME",
        "ContactPhone": "212563080",
        "Email": ""
      },
      "CostCentre": "TEST COST CENTRE ONE",
      "Carrier": "Post Haste - AKL - 2011",
      "DeliveryInstructions": "",
      "IsSaturdayDelivery": false,
      "IsRuralDelivery": false,
      "IsPOBox": false,
      "CustomerRef": "#1031",
      "TotalCubic": 0.022,
      "TotalKg": 5.5,
      "Parts": 1,
      "IsSignatureRequired": true,
      "IsFreightForward": false,
      "ManifestedAt": null,
      "Items": [
        {
          "PartNo": 1,
          "LengthCm": 47,
          "WidthCm": 47,
          "HeightCm": 10,
          "WeightKg": 5.5,
          "PackageName": "SMALL BOX",
          "Charge_LineTotal": 9.98,
          "PickedAt": null,
          "DeliveredAt": null,
          "RatingCode": "MS"
        }
      ],
      "ConsignmentNo": "APD00020627",
      "Status": null,
      "Picked": null,
      "Delivered": null,
      "Tracking": "https:\/\/gosweetspot.com\/track\/108633-APD00020627",
      "Events": [
        
      ],
      "ManifestNumber": "ABCD",
      "TotalCost": 9.98,
      "CreatedUtc": "2019-10-10T23:30:53.88",
      "PackingSlipNo": "#1031",
      "ManualTicket": false,
      "Consignee": "RECEIVER NAME"
    }
  ]
}

```
