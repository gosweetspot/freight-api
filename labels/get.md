# Labels

    GET api/labels

## Description
Gets the shipment labels in the requested format, png or pdf.

***

## Requires authentication
* A valid access Key must be provided in **access_key** request header.

***

## Parameters
<table>
      <tr>
        <th>Field</th>
        <th>Required?</th>
        <th>Description</th>
      </tr>
        <tr>
            <td valign="top">**format**</td>
            <td valign="top">optional</td>
            <td>
              available formats are as below. If not supplied, the default is LABEL_PNG_100X175  

              <ul>
                <li>LABEL_PDF - label is presented on an A4 page  </li>
                <li>LABEL_PNG_100X175 - label is presented as a PNG image with dimension 100mm x 175mm</li>
                <li>LABEL_PNG_100X150 - label is presented as a PNG image with dimension 100mm x 150mm</li>
                <li>LABEL_PDF_100X175 - label is presented as a PDF with dimension 100mm x 175mm</li>
                <li>LABEL_PDF_100X150 - label is presented as a PDF with dimension 100mm x 150mm </li>
                <li>The 100x150 sizing is presently experimental and not available across all carriers.</li>
              </ul>
            </td>
        </tr>
        <tr>
          <td>**rotate**</td>
          <td>optional</td>
          <td>if the label orientation requires 180 degree rotation</td>
        </tr>
        <tr>
          <td>**connote**</td>
          <td>required</td>
          <td>shipment consignment number to download</td>
        </tr>
</table>

***

## Return format
An array of base64 encoded binary:

In the case of multi part shipments, the PNG format will return a binary block per part.
In the case of PDF, all parts are returned on a single multi page pdf.
***

## Example
**Request**

    GET http://api.gosweetspot.com/api/labels?format=label_png&connote=ABA0010054

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
