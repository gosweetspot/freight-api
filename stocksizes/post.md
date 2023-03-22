[![](../obsolete-banner.png)](https://api-docs.gosweetspot.com/)

# Create/Update Stock Size

    POST api/stocksizes

## Description
This method is used to create new stock sizes or update an existing stock size.

## Requires authentication
* A valid access key must be provided in `access_key` request header.
* If the user with the access_key has access to multiple sites in the account, a `site_id` HTTP header with the site id is also required.

***

## Parameters

The body of the message should be sent as an JSON array.

- **PackageStockId** - integer, GoSweetSpot generated an unique identifier for each Stock Size. we try to find and update the existing record first, if there is no matching record, we will create a stock size instead. For creating stock size, you can set this field to null. 
- **Name** - string, name of the stock size.
- **Height** - decimal, height of the stock size.
- **Length** - decimal, lengh of the stock size.
- **Width** - decimal, width of the stock size.
- **Weight** - decimal, weight of the stock size.
- **Type** - string, type of the stock size - Box, Carton, etc. 
- **Sort** - integer, sequence of all stock sizes on Ship UI.
- **Availability** - string, represents access scope of the stock size:  
      Me_Only - only current user can use the stock size.  
      This_Site_Only - users on the site.  
      Entire_Group - users on the bussiness account.  

## Example 1 - Create stock zies

**Request**

    http://api.gosweetspot.com/api/stocksizes

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8



*Body*
``` json
{
    "Name": "Test",
    "Height": 11,
    "Length": 12,
    "Width": 13,
    "Type": "BOX",
    "Weight": 5.0,
    "Sort": 1,
    "Availability": "This_Site_Only"
}
```


**Response**
``` json
{
    "PackageStockId": 159880,
    "Name": "Test",
    "Height": 11.0,
    "Length": 12.0,
    "Width": 13.0,
    "Cubic": 0.002,
    "Type": "BOX",
    "Weight": 5.0,
    "Sort": 1,
    "IsTrackPak": false,
    "HeightAdjustable": true,
    "Availability": "This_Site_Only"
}

```


## Example 2 - Update an existing stock size

**Request**

    POST http://api.gosweetspot.com/api/stocksizes

*Headers*

    access_key: [access_key_for_site_account]
    Content-Type: application/json; charset=utf-8

*Body*
``` json
{
    "PackageStockId": 159880,
    "Name": "Test",
    "Height": 90,
    "Length": 90,
    "Width": 70,
    "Type": "Carton",
    "Weight": 15.0,
    "Sort": 200,
    "Availability": "Me_Only"
}
```


**Response**
``` json
{
    "PackageStockId": 159880,
    "Name": "Test",
    "Height": 90.0,
    "Length": 90.0,
    "Width": 70.0,
    "Cubic": 0.001716,
    "Type": "Carton",
    "Weight": 15.0,
    "Sort": 200,
    "IsTrackPak": false,
    "HeightAdjustable": false,
    "Availability": "Me_Only"
}
```