# Shipments

    GET https://api.gosweetspot.com/api/shipments

## Description
Get status updates for shipments

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

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
                                                        <li>CR - Created</li>
                                                        <li>PUP - Picked up from sender</li>
                                                        <li>UPD - Courier status update provided</li>
                                                        <li>EXP - delivery exception, or service update</li>
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

    GET http://api.gosweetspot.com/api/shipments?lastupdateminutc=2015-08-13%2008:15:13&page=1&shipments=ABC0001,ABC0002,ABC20303

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8


**Return** __shortened for example purpose__
``` json
{
	"Page": 1,
	"PageSize": 3,
	"Pages": 1,
	"Results": [
		{
			"ConsignmentNo": "SSPOT015389",
			"Status": "Delivered to ANDREW",
			"Picked": "2015-05-29T15:37:45",
			"Delivered": "2015-06-02T10:23:20",
			"Tracking": "http://gosweetspot.com/track/4180-SSPOT015389",
			"Events": [
				{
					"EventDT": "2015-05-29T14:34:32.927",
					"Code": "CR",
					"Description": "Tracking number allocated & order ready",
					"Location": "AUCKLAND",
					"Part": "SSPOT01538901"
				},
				{
					"EventDT": "2015-05-29T15:37:45",
					"Code": "COUR",
					"Description": "Picked up",
					"Location": "PENROSE (AKL)",
					"Part": "SSPOT01538901"
				},
				{
					"EventDT": "2015-06-02T08:46:32",
					"Code": "COURU",
					"Description": "On courier vehicle for delivery",
					"Location": "Glenfield Industrial Wairau Valley (AKL)",
					"Part": "SSPOT01538901"
				},
				{
					"EventDT": "2015-06-02T10:23:20",
					"Code": "DEL",
					"Description": "Delivered to ANDREW",
					"Location": "Glenfield Industrial Wairau Valley (AKL)",
					"Part": "SSPOT01538901"
				}
			],
			"TotalCost": 8.90,
			"CreatedUtc": "2015-05-30T02:34:32.927",
			"PackingSlipNo": "SSORDER10133",
			"ManualTicket": false,
			"Consignee": "BOB SMITH LTD"
		},
		{
			"ConsignmentNo": "SSPOT015387",
			"Status": "Delivered to FRONT DOOR",
			"Picked": "2015-05-29T15:37:45",
			"Delivered": "2015-06-02T06:27:13",
			"Tracking": "http://gosweetspot.com/track/4180-SSPOT015387",
			"Events": [
				{
					"EventDT": "2015-05-29T14:33:46.46",
					"Code": "CR",
					"Description": "Tracking number allocated & order ready",
					"Location": "AUCKLAND",
					"Part": "SSPOT01538701"
				},
				{
					"EventDT": "2015-05-29T15:37:45",
					"Code": "COUR",
					"Description": "Picked up",
					"Location": "PENROSE (AKL)",
					"Part": "SSPOT01538701"
				},
				{
					"EventDT": "2015-06-02T05:40:41",
					"Code": "COURU",
					"Description": "On courier vehicle for delivery",
					"Location": "KELSTON/GLEN EDEN/GLENDENE/HENDERSON (AKL)",
					"Part": "SSPOT01538701"
				},
				{
					"EventDT": "2015-06-02T06:27:13",
					"Code": "DEL",
					"Description": "Delivered to FRONT DOOR",
					"Location": "KELSTON/GLEN EDEN/GLENDENE/HENDERSON (AKL)",
					"Part": "SSPOT01538701"
				}
			],
			"TotalCost": 8.95,
			"CreatedUtc": "2015-05-30T02:33:46.46",
			"PackingSlipNo": "SSORDER10135",
			"ManualTicket": false,
			"Consignee": "TOM HARDY LIMITED"
		},
		{
			"ConsignmentNo": "SSPOT015392",
			"Status": "Delivered to 25 HARKNESS",
			"Picked": "2015-06-04T16:08:39",
			"Delivered": "2015-06-05T08:07:00",
			"Tracking": "http://gosweetspot.com/track/4180-SSPOT015392",
			"Events": [
				{
					"EventDT": "2015-06-02T11:57:21.63",
					"Code": "CR",
					"Description": "Tracking number allocated & order ready",
					"Location": "AUCKLAND",
					"Part": "SSPOT01539201"
				},
				{
					"EventDT": "2015-06-04T16:08:39",
					"Code": "COUR",
					"Description": "Picked up",
					"Location": "PENROSE (AKL)",
					"Part": "SSPOT01539201"
				},
				{
					"EventDT": "2015-06-05T06:57:55",
					"Code": "COURU",
					"Description": "On courier vehicle for delivery",
					"Location": "AVONHEAD/ILAM/UPPER RICCARTON (CHC)",
					"Part": "SSPOT01539201"
				},
				{
					"EventDT": "2015-06-05T08:07:23",
					"Code": "DEL",
					"Description": "Delivered to 25 HARKNESS",
					"Location": "AVONHEAD/ILAM/UPPER RICCARTON (CHC)",
					"Part": "SSPOT01539201"
				}
			],
			"TotalCost": 17.56,
			"CreatedUtc": "2015-06-02T23:57:21.63",
			"PackingSlipNo": "SSORDER10154",
			"ManualTicket": false,
			"Consignee": "THE FOX SHED"
		}
	]
}

```
