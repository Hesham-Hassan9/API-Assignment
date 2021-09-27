# I have used three APIs in my app?

## 1. LocationIQ:

### Description

LocationIQ offers a suite of services that provide powerful, reliable and scalable geolocation experiences. LocationIQ provides:

    * Address APIs: reverse geocoding, forward geocoding, autocomplete

    * Map APIs: Bitmap boxes, dynamic and static maps
   
    * Orientation APIs: Orientation, Distance Matrix, Map Matching, Nearest and More

### Usage

#### Requests can be sent to the following endpoints

   https://eu1.locationiq.com/v1/search.php?key=YOUR_ACCESS_TOKEN&q=SEARCH_STRING&format=json

  **Query Parameters:**

  | Name                                                       | Description                                                                                                                                                                                                                     | Required |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| key                                                        | Your API Key                                                                                                                                                                                                                    | Yes      |
| q                                                          | Free-form query string to search for. Commas are optional, but improves performance by reducing the complexity of the search. Do not combine with `structured`/`postalcode` parameters                                          | Either   |
| street<br>city<br>county<br>state<br>country<br>postalcode | Alternative query string format split into several parameters for `structured` requests. Structured requests are faster but are less robust against alternative OSM tagging schemas. Do not combine with `q=<query>` parameter. | Either   |

### Endpoints/Request URLs

#### Endpoints

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

### Authentication Key or Access Tokens

For user-facing applications such as Javascript websites or mobile applications, we recommend creating new access tokens on your user dashboard. Create a separate access token for each app, name it accordingly like "My Website" - and reissue these tokens frequently to prevent abuse. You can use access tokens in both public environments (websites and applications) and private environments (server backends).

## 2. weatherbit

### Description

Weatherbit API shows 16 days and returns forecasts each day from any factor at the planet. You need to send all parameters to Weather API as query string parameters. Obtains orders that show the every day forecast whilst every factor represents a duration of 1 day; Date, city, post and more. Supported interplay format is JSON with an API key required for authentication. Weatherbit.io is a historical weather, current weather and forecast API.

### Usage

Requests can be sent to the following endpoints

https://api.weatherbit.io/v2.0/forecast/daily

**Query Parameters:**

  | Name                                                       | Description                                                                                                                                                                                                                     | Required |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| key                                                        | Your API Key                                                                                                                                                                                                                    | Yes      |
| lang=[language]                                                          | the language used to display data of like en - [DEFAULT] English                                         | optional   |
| units | Units used to display unit of measure Temperature as M - [DEFAULT] Metric (Celcius, m/s, mm) | optional   |
| days=[integer] | return a specific number of forecast days | optional   |

### Endpoints/Request URLs

#### Endpoints

| Description                           | Required Parameters                       | Example(s)                                                                         |
| ------------------------------------- | ----------------------------------------- | ---------------------------------------------------------------------------------- |
| Get forecast by lat/lon (Recommended) | lat,lon                                   | &lat=38.123&lon=-78.543                                                            |
| Get forecast by city name             | city state(optional) country (optional) |   &city=Raleigh&country=US<br>   &city=Raleigh,NC   &city=Raleigh,North+Carolina |
| Get forecast by postal code           | postal\_code, country (optional)          | &postal\_code=27601&country=US                                                     |
| Get forecast by Station               | station                                   | *   &station=KRDU                                                                  |
| Get forecast by city id               | city\_id                                  | &city\_id=8953360                                                                  |

**Style Specification URL :**

 use the style specification URL. The pattern URL looks like this:

https://api.weatherbit.io/v2.0/forecast/daily?city=Raleigh,NC&key=API_KEY

**Response**

{  

             "data":[  
                {  
                  "valid_date":"2017-04-01",
                   "ts":1503954000,
                   "datetime":"2017-04-01",
                   "wind_gust_spd":16.7,
                   "wind_spd":6.4,
                   "wind_dir":45,
                   "wind_cdir":"NE",
                   "wind_cdir_full":"northeast",
                   "temp":25,
                   "max_temp":30,
                   "min_temp":26,
                   "high_temp":30,
                   "low_temp":24.5,
                   "app_max_temp":30.64,
                   "app_min_temp":23.64,
                   "pop":0,
                   "precip":0,
                   "snow":0,
                   "snow_depth":0,
                   "slp":1017,
                   "pres":1003.5,
                   "dewpt":17.8,
                   "rh":64.3,
                   "weather":{  
                      "icon":"c04d",
                      "code":"804",
                      "description":"Overcast clouds"
                   
                   },
                   "pod":"d",
                   "clouds_low":25,
                   "clouds_mid":100,
                   "clouds_hi":50,
                   "clouds":100,
                   "vis":10,
                   "max_dhi":178,
                   "uv":2,
                   "moon_phase":0.99,
                   "moon_phase_lunation":0.48,
                   "moonrise_ts":1530341260,
                   "moonset_ts":1530351260,
                   "sunrise_ts":1530321260,
                   "sunset_ts":1530391260
                }, ...
             ],
             "city_name":"Raleigh",
             "lon":"-78.63861",
             "timezone":"America\/New_York",
             "lat":"35.7721",
             "country_code":"US",
             "state_code":"NC"
          
          }

          
| Name           | Decriptions                                                                           |
|----------------|---------------------------------------------------------------------------------------|
| lat            | Latitude (Degrees)                                                                    |
| lon            | Longitude (Degrees)                                                                   |
| timezone       | Local IANA Timezone                                                                   |
| city_name      | Nearest city name                                                                     |
| country_code   | Country abbreviation                                                                  |
| state_code     | State abbreviation/code                                                               |
| data           | [contain all data]                                                                    |
| valid_date     | Date the forecast is valid for in format YYYY-MM-DD [Midnight to midnight local time] |
| ts             | Forecast period start unix timestamp (UTC)                                            |
| datetime       | [DEPRECATED] Forecast valid date (YYYY-MM-DD)                                         |
| wind_gust_spd  | Wind gust speed (Default m/s)                                                         |
| wind_spd       | Wind speed (Default m/s)                                                              |
| wind_dir       | Wind direction (degrees)                                                              |
| wind_cdir      | Abbreviated wind direction                                                            |
| wind_cdir_full | Verbal wind direction                                                                 |
| temp           | Average Temperature (default Celcius)                                                 |
| max_temp       | Maximum Temperature (default Celcius)                                                 |
| min_temp       | Minimum Temperature (default Celcius)                                                 |
| high_temp      | High Temperature - Calculated from 6AM to 6AM local time (default Celcius)            |
| low_temp       | Low Temperature - Calculated from 6AM to 6AM local (default Celcius)                  |
| app_max_temp   | Apparent/"Feels Like" temperature at max_temp time (default Celcius)                  |
| app_min_temp   | Apparent/"Feels Like" temperature at min_temp time (default Celcius)                  |
| weather        | [contain ico/ code/ description]                                                      |

### Authentication Key 

For user-facing applications such as Javascript websites or mobile applications, create a separate authentication key for each application, name it accordingly like "My Website" - and reissue these tokens frequently to prevent abuse. You can use access tokens in both public environments (websites and applications) and private environments (server backends).

## 3. The Movie Database

### Description

TMDb API: A useful resource for any developer who need to combine movie, TV and broadcast information in the side of posters or movie fan art. themoviedb.org is a loose database and community editor.

### Usage

Requests can be sent to the following endpoints

https://api.themoviedb.org/3/search/movie?api_key={api_key}&query=Jack+Reacher

**Query Parameters:**


| Name    | Description                       |          |
|---------|-----------------------------------|----------|
| api_key | Your access key                   | required |
| query   | to make your search to movie name | required |

### Endpoints/Request URLs

#### Endpoints

https://api.themoviedb.org/3/search/movie?api_key={api_key}&query=Jack+Reacher

#### Request

{

  "poster_path": "/IfB9hy4JH1eH6HEfIgIGORXi5h.jpg",

  "adult": false,
  
  "overview": "Jack Reacher must uncover the truth behind 
  a major government conspiracy in order to clear his name. On the run as a fugitive from the law, Reacher uncovers a potential secret from his past that could change his life forever.",
  
  "release_date": "2016-10-19",
  
  "genre_ids": [
    53,
    28,
    80,
    18,
    9648
  ],
  
  "id": 343611,
  
  "original_title": "Jack Reacher: Never Go Back",
  
  "original_language": "en",
  
  "title": "Jack Reacher: Never Go Back",
  
  "backdrop_path": "/4ynQYtSEuU5hyipcGkfD6ncwtwz.jpg",
  
  "popularity": 26.818468,
  
  "vote_count": 201,
  
  "video": false,
  
  "vote_average": 4.19

}

### Authentication Key 

For user-facing applications such as Javascript websites or mobile applications, create a separate authentication key for each application, name it accordingly like "My Website" - and reissue these tokens frequently to prevent abuse. You can use access tokens in both public environments (websites and applications) and private environments (server backends).

## References

Locationiq.com. 2021. LocationIQ - Free & Fast Geocoding, Reverse Geocoding and Maps service. [online] Available at: &lt;https://locationiq.com/docs> [Accessed 24 September 2021].

Weatherbit.io. 2021. Weatherbit | 16 Day Forecast API Documentation. [online] Available at: <https://www.weatherbit.io/api/weather-forecast-16-day> [Accessed 25 September 2021].

Developers.themoviedb.org. 2021. API Docs. [online] Available at: <https://developers.themoviedb.org/3/getting-started/search-and-query-for-details> [Accessed 25 September 2021].

# these are the links for the project: 
github links : https://github.com/Hesham-Hassan9

city explore : https://github.com/Hesham-Hassan9/city-explorer

city explore API: https://github.com/Hesham-Hassan9/city-explorer-api

netlify link: https://hesham-city-explorer.netlify.app/

Heroku link :https://city-explorer-api9.herokuapp.com/

Weather link: https://city-explorer-api9.herokuapp.com/getweather?searchQuery=London

Movies link: https://city-explorer-api9.herokuapp.com/getmovies?searchQuery=London