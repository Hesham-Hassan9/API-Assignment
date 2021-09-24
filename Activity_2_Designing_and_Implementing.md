I have used three API in my app?

# 1. LocationIQ:

## Description

LocationIQ offers a suite of services that provide powerful, reliable and scalable geolocation experiences. LocationIQ provides:

    * Address APIs: reverse geocoding, forward geocoding, autocomplete

    * Map APIs: Bitmap boxes, dynamic and static maps
   
    * Orientation APIs: Orientation, Distance Matrix, Map Matching, Nearest and More

## Usage

### Requests can be sent to the following endpoints

   https://eu1.locationiq.com/v1/search.php?key=YOUR_ACCESS_TOKEN&q=SEARCH_STRING&format=json

  **Query Parameters:**

  | Name                                                       | Description                                                                                                                                                                                                                     | Required |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| key                                                        | Your API Key                                                                                                                                                                                                                    | Yes      |
| q                                                          | Free-form query string to search for. Commas are optional, but improves performance by reducing the complexity of the search. Do not combine with `structured`/`postalcode` parameters                                          | Either   |
| street<br>city<br>county<br>state<br>country<br>postalcode | Alternative query string format split into several parameters for `structured` requests. Structured requests are faster but are less robust against alternative OSM tagging schemas. Do not combine with `q=<query>` parameter. | Either   |

## Endpoints/Request URLs

### Endpoints

Depending on the Maps SDK you decide to use, you'll need to use either the style specification URL or the box URLs.

**Style Specification URL :**

For Mapbox-GL SDKs, use the style specification URL. The pattern URL looks like this:

https://tiles.locationiq.com/v3/&lt;theme>/&lt type>.json?key=&lt;access_token>

**Parameters**

| Name          | Description                                                                                                                                                                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| theme         | `streets`, `earth`, `hybrid`. Complete list of available themes [here](https://locationiq.com/docs-html/index.html?shell#list_of_available_themes).                                                                                                          |
| type          | `vector`,`raster`. `vector` renders the map on the client-side and is faster, has crisper text and consume less bandwidth. `raster` by nature is slower and consumes more bandwidth as images are rendered on the server-side and transferred to the client. |
| access\_token | Your LocationIQ public access token. We recommend that you generate a new `access token` on your User Dashboard and add HTTP Referrer Restrictions to avoid abuse.                                                                                           |

**Response**

| Name          | Description                                                                                                                                                                                                                                                                               |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| place\_id     | An internal identifier for this result in the LocationIQ database. This value may vary across our servers, and change often, so do not use this as an identifier for caching or storage.                                                                                                  |
| licence       | The Licence and attribution requirements                                                                                                                                                                                                                                                  |
| osm\_type     | The type of this result. One of `node`,`way` or `relation`.                                                                                                                                                                                                                               |
| osm\_id       | The corresponding OSM ID of this result.                                                                                                                                                                                                                                                  |
| boundingbox   | Array of bounding box coordinates where this result is located. The order is as below:<br>\- min lat / bottom-left Latitude<br>\- max lat / top-right Latitude<br>\- min lon / bottom-left Longitude<br>\- max lon / top-right Longitude                                                  |
| lat           | The Latitude of this result                                                                                                                                                                                                                                                               |
| lon           | The Longitude of this result                                                                                                                                                                                                                                                              |
| display\_name | The display name of this result, with complete address                                                                                                                                                                                                                                    |
| importance    | Calculated importance of this result compared to the search query the user has provided. Ranges between 0 and 1. Type: float                                                                                                                                                              |
| icon          | The URL of an icon representing this result, if applicable.                                                                                                                                                                                                                               |
| address       | The address breakdown into individual components. Returned when `addressdetails=1` is set in the request. Important components include (but not limited to) country, postcode, state, county, city, town. [Read more.](https://locationiq.com/docs-html/index.html?shell#address-details) |
| extratags     | The dictionary with additional useful tags like website or maxspeed. Returned when `extratags=1` is set in the request.                                                                                                                                                                   |
| namedetails   | The dictionary with full list of available names including ref etc. Returned when `namedetails=1` is set in the request.                                                                                                                                                                  |
| geojson       | Output geometry of results in geojson format. Returned when `polygon_geojson=1` is set in the request.                                                                                                                                                                                    |
| geokml        | Output geometry of results in kml format. Returned when `polygon_kml=1` is set in the request.                                                                                                                                                                                            |
| svg           | Output geometry of results in svg format. Returned when `polygon_svg=1` is set in the request.                                                                                                                                                                                            |
| geotext       | Output geometry of results as a WKT. Returned when `polygon_text=1` is set in the request.                                                                                                                                                                                                |

## Authentication Key or Access Tokens

For user-facing applications such as Javascript websites or mobile applications, we recommend creating new access tokens on your user dashboard. Create a separate access token for each app, name it accordingly like "My Website" - and reissue these tokens frequently to prevent abuse. You can use access tokens in both public environments (websites and applications) and private environments (server backends).


### References

Locationiq.com. 2021. LocationIQ - Free & Fast Geocoding, Reverse Geocoding and Maps service. [online] Available at: &lt;https://locationiq.com/docs> [Accessed 24 September 2021].
