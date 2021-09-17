# Labels

    GET api/labels

## Description
Gets the shipment labels in the requested format, png or pdf.

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Parameters
|Field|Required?|Description|
|--- |--- |--- |
|**connote**|required|Shipment consignment number to download.|
|**format**|optional|The format of the label. See below section for available formats.|
|**rotate**|optional|true or false. Specify this if the label requires rotation.|



### Available format types:

+ LABEL_PDF - label is presented on an A4 page.  </li>
+ LABEL_PNG_100X175 - label is presented as a PNG image with dimension 100mm x 175mm.
+ LABEL_PNG_100X150 - label is presented as a PNG image with dimension 100mm x 150mm.
+ LABEL_PDF_100X175 - label is presented as a PDF with dimension 100mm x 175mm.
+ LABEL_PDF_100X150 - label is presented as a PDF with dimension 100mm x 150mm.
+ LABEL_PDF_LABELOPE - label is presented as a PDF Labelope. Rotation is not supported.
+ The 100x150 sizing is presently experimental and not available across all carriers.
+ USER_CONFIGURED - label is presented as a PDF when [User's Printing Setting](https://ship.gosweetspot.com/settings) is PDF file, or a PRN file is presented if [User's Printing Setting](https://ship.gosweetspot.com/settings) is GoPrint - PRN Download.
+ GOPRINT_PRN - PRN file is presented.
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
