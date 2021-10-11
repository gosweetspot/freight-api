# Stock Sizes

    GET https://api.gosweetspot.com/api/stocksizes

## Description
Get the list of available stock sizes

***

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Return format
### Root Object
- An array of objects, where each object represents a stock size available to your user.

### Stock Size
- **PackageStockId** - integer, GoSweetSpot generated an unique identifier for each Stock Size.
- **Name** - string, name of the stock size.
- **Height** - decimal, height of the stock size.
- **Length** - decimal, lengh of the stock size.
- **Width** - decimal, width of the stock size.
- **Cubic** - decimal, cubic(M3) of the stock size.
- **Weight** - decimal, weight of the stock size.
- **Type** - string, type of the stock size - Box, Carton, etc. 
- **Sort** - integer, sequence of all stock sizes on Ship UI.
- **IsTrackPak** - bool, represents if the stock size is trackable.
- **HeightAdjustable** - bool, represents if user can adjust the height of the stock size.
- **Availability** - string, represents access scope of the stock size:  
      Me_Only - only current user can use the stock size.  
      This_Site_Only - users on the site.  
      Entire_Group - users on the bussiness account.  
    
## Example
**Request**

    https://api.gosweetspot.com/api/stocksizes

**Headers**

    access_key: [access_key_for_site_account]
    
    Content-Type: application/json; charset=utf-8

**Return** __shortened for example purpose__
``` json

[
  {
        "PackageStockId": 5694,
        "Name": "AusPost 200g Satchel",
        "Height": 2.0000,
        "Length": 35.0000,
        "Width": 27.0000,
        "Cubit": 0.001890,
        "Type": "Satchel",
        "Weight": 0.2000,
        "Sort": 0,
        "IsTrackPak": true,
        "HeightAdjustable": false,
        "Availability": "Entire_Group"
    },
    {
        "PackageStockId": 6101,
        "Name": "AusPost 3KG Satchel",
        "Height": 3.0000,
        "Length": 35.0000,
        "Width": 27.0000,
        "Cubit": 0.002835,
        "Type": "Satchel",
        "Weight": 3.0000,
        "Sort": 0,
        "IsTrackPak": true,
        "HeightAdjustable": false,
        "Availability": "Entire_Group"
    },
    {
        "PackageStockId": 6073,
        "Name": "Castle Max Pack",
        "Height": 3.0000,
        "Length": 45.0000,
        "Width": 45.0000,
        "Cubit": 0.006075,
        "Type": "Satchel",
        "Weight": 3.0000,
        "Sort": 0,
        "IsTrackPak": true,
        "HeightAdjustable": false,
        "Availability": "Entire_Group"
    },
]


```
