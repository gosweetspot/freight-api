# Pending Orders

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
mandatory parameters are marked with an astricks (*)


***

## Return format
<table>
  <tr>
    <th colspan="2">Return Value</th>
  </tr>
  <tr>
    <td>array</td>
    <td>a list of up to 1000 shipments
      <table>
        <tr>
          <td>return[] <br />struct</td>
          <td>shipment
              <table>
                <tr>
                  <td>ConsignmentNo</td>
                  <td>string</td>
                  <td>shipment consignment number</td>
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
                  <td>Events</td>
                  <td>return[] <br />struct</td>
                  <td>track and trace url for live tracking of the order

                        <table>
                          <tr>
                            <td>Part</td>
                            <td>shipment part number</td>
                          </tr>
                          <tr>
                            <td>Code</td>
                            <td>event milestone code.
                              * CR - Created
                              * PUP - Picked up from sender
                              * UPD - Courier status update provided
                              * EXP - delivery exception, or service update
                            </td>
                          </tr>
                          <tr>
                            <td>Description</td>
                            <td>Event description</td>
                          </tr>
                          <tr>
                            <td>eventDt</td>
                            <td>date/time of event/activity local to location of event</td>
                          </tr>
                          <tr>
                            <td>Location</td>
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

    GET http://api.gosweetspot.com/labels/download?format=label_png&connote=ABA0010054

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8


**Return** __shortened for example purpose__
``` json
[
  "iVBORw0KGgoAAAANSUhEUgAABUYAAAMHCAYAAAD1lY2SAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAP+lSURBVHhe7P0JtGX3ld\/3UbKk7pYlmW4pDiUPk",
  "iVBORw0KGgoAAAANSUhEUgAABUYAAAMHCAYAAAD1lY2SAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAP+lSURBVHhe7P0JtGXXnd\/3UbKk7pYlmW4pDiUPk",
  "iVBORw0KGgoAAAANSUhEUgAABUYAAAMHCAYAAAD1lY2SAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAP+lSURBVHhe7P0J9GXXld\/3UbKk7pYlmW4pDiUPk"
]

**binary blocks above have been trimmed for presentation.**

```
