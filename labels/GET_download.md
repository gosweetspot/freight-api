[![](../obsolete-banner.png)](https://api-docs.gosweetspot.com/)

# Label

    GET download

## Description
Gets the shipment labels in the requested format.

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Parameters
- **format** - optional - available formats are as below. If not supplied, the default is LABEL_PNG_100X175  
      LABEL_PDF - label is presented on an A4 page  
      LABEL_PNG_100X175 - label is presented as a PNG image with dimension 100mm x 175mm  
      LABEL_PNG_100X150 - label is presented as a PNG image with dimension 100mm x 150mm  
      LABEL_PDF_100X175 - label is presented as a PDF with dimension 100mm x 175mm  
      LABEL_PDF_100X150 - label is presented as a PDF with dimension 100mm x 150mm  

      The 100x150 sizing is presently experimental and not available across all carriers.  
- **rotate** - optional - if the label orientation requires 180 degree rotation
- **connote** - shipment consignment number to download

***

## Return format
An array of base64 encoded binary:

In the case of multi part shipments, the PNG format will return a binary block per part.
In the case of PDF, all parts are returned on a single multi page pdf.
***

## Example
**Request**

    GET https://api.gosweetspot.com/labels/download?format=label_png&connote=ABA0010054

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
