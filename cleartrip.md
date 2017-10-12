# ClearTrip Micro Services

1. [Local Activities](#local-activities)

    * [City List](#11-book-itenerary)
    * [Collections List](#11-book-itenerary)
    * [Activity List](#11-book-itenerary)
    * [Activity Details](#11-book-itenerary)
    * [Search City](#11-book-itenerary)
    * [Check Availability](#11-book-itenerary)
    * [Create Itinerary](#11-book-itenerary)
    * [Book Itinerary](#11-book-itenerary)
  
2. [Local Eatout](#local-activities)
  
    * [City List](#11-book-itenerary)
    * [Restaurants List](#11-book-itenerary)
    * [Eatouts List](#11-book-itenerary)
    * [Eatout Details](#11-book-itenerary)
    * [Search City](#11-book-itenerary)
    * [Check Availability](#11-book-itenerary)
    * [Create Itinerary](#11-book-itenerary)
    * [Book Itinerary](#11-book-itenerary)

--------------------------------------------------------------------------------

## Local Activities 

microapp_handle : `com.cleartrip.microservices.local.activities`
### 1.1 City List

#### Intent
`city_list`

City list api will list all the available cities and there product type availability in that city. The search request is a simple HTTP GET request. The sample request described below should be sent along with the URL, and the user’s API key in the HTTP headers. A successful response will always return the HTTP status code 200. (Note that a status code of 200 doesn’t necessarily mean that the search result will be returned; but a successful search will always return a status code of 200).

### Response Body
```
"bangalore": {
        "ttd": true,
        "count": 1,
        "fnb": true
    },
 ```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| ttd | Contains True/False based on availability in the corresponding city |
| fnb | Contains True/False based on availability in the corresponding city |

If the search was successful, the response body returns an JSON along with the HTTP status code 200. If any error is encountered during the search, the response body contains an JSON with the root element error_code. See the schema and sample search result JSON for more details.


### 1.2 Collections List

#### Intent
`collections_list_ttd`

Provides the Cleartrip Collection Listing for a City. The search request is a simple HTTP GET request. The query parameters described below should be sent along with the search URL, and the user’s API key in the HTTP headers. A successful response will always return the HTTP status code 200. (Note that a status code of 200 doesn’t necessarily mean that the search result will be returned; but a successful search will always return a status code of 200).
City list api also take tags as optional params and return the data related to tags, otherwise 400 for requested api.
 
### Payload
```
{
  "intent":"collections_list_ttd",
  "data":{
  	"cityName":"bangalore"   
  }
}
```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| cityName | Name of city |

### Response Body 
```
{
scr : "INR",
collections[],
city{},
categories[],
sid : "5b434caa-5446-43fa-ab39-4b34c6a75e64"
}
```

### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| currency | The currency in which the prices of activities are displayed  |
| collections | List of collections available on this city and it's details |
| collections.count | Number of activities available for this collections |
| collections.rank | Sequence order to show on ui |
| collections.id | Collection id of the collection |
| collections.categories | List of categories id which this collection belong |
| collections.name | Name of the collection |
| collections.desc | Description of this collection |
| collection.image | Image Image link we can use by adding "http://ui.cltpstatic.com/" or "http://apistaging.cleartrip.com/" as base url|
| city | City name and city id for further use |
| city.name | Name of the city |
| city.id | Id of the city |
| categories | List of all categories for these collections |
| categories.name | Name of the categories |
| categories.rank | Sequence order of list of categories |
| categories.id | Id of categories |

If the search was successful, the response body returns an JSON along with the HTTP status code 200. If any error is encountered during the search, the response body contains an JSON with the root element error_code. See the schema and sample search result JSON for more details.

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the city | City is missing. |
 
### 1.3 Activity List

#### Intent
`activity_list`

The collection info request takes the collection Id and city Id as input and provides the brief activities information which are part of that collections, along with the thumbnail and wide-angle image URL in response.
Note: Some of the activities might overlap in different collections
Example: Wonderla activity might get listed as part of 'Theme Parks' as well as 'Water Sprots' collections.
Collection info api also take tags as optional params and return the data related to tags, otherwise 400 for requested api.

### Payload
```
{
  "intent":"activity_list",
  "data":{
  	"city_id":"32550",
  	"id":"25270"
    
  }
}
```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| city_id | City ID  |
| id | Collection ID from collection list API |

### Response Body 
```
{
result[],
activities_near_you{},
scr : "INR",
explore_collections{},
web_url : "/local/gadag/art-craft-in-gadag-collection-1560-1",
details{},
collection{}
sid : "068740f3-741f-4c48-a179-5ea6671aae77"
}
```

### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| currency | The currency in which the prices of activities are displayed  |
| result | Show list of variant or activities on this collections|
| result.image| Image Image link we can use by adding "http://ui.cltpstatic.com/" or "http://apistaging.cleartrip.com/" as base url |
| result.address | Full activity address information |
| result.address.address_type | Address_type either will be activity address or pickup address of this activity |
| result.address.locality_name | locality name of activity |
| result.price | Activity price in requested currency format |
| result.name | Name of the activity |
| result.activity_id | Id of activity|
| result.id | Id of variant |
| result.timings | Activity or variant start time |
| result.published_time | When this activity or variant published in datetime format |
| extras |extras value will present fnb product type only. |
| extras.localities | list of localities which are all mapped to results.address.locality_name value |
| extras.tag | all different tag type value |
| collection | Show collection information in details |
| details | This details will be present if we have only one variant or activity in a collections |

If the search was successful, the response body returns an JSON along with the HTTP status code 200. If any error is encountered during the search, the response body contains an JSON with the root element error_code. See the schema and sample search result JSON for more details.

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the city | city-id is missing.|
| Please specify the collection-id | collection-id is a required field.|

### 1.4 Activity Details

#### Intent
`activity_details_ttd`

The activity details info request takes the result’s id and city id as input and provides the detailed activity information along with the thumbnail and wide-angle image URL in response. 
Note :For FNB details you need to pass activity-id from result's list as mandatory parameter to get the details. If needs to get categories for this activity we need to just pass categories=true in request parameters.


### Payload
```
{
  "intent":"activity_details_ttd",
  "data":{
  	"city_id":"32550",
  	"id":"42774"
  }
}
```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| city_id | City ID  |
| id |  Selected Activity ID from activity list api |

### Response Body 
```
{
scr : "INR",
web_url : "/local/gadag/11-39-stack-2-activityy-in-gadag-75742-1",
details{},
sid : "b9effb20-981f-4e7e-b46d-d992bd7f1daa"
}
```

### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| currency | The currency in which the prices of activities are displayed  |
| details | Show complete details of this activity or variant |
| details.activity_name| Name of the activity |
| details.published_time | Name of the variant |
| details.variant_name | Address_type either will be activity address or pickup address of this activity |
| details.images | List of image for this activity or variant |
| details.images.img |Image link we can use by adding "http://ui.cltpstatic.com/" or "http://apistaging.cleartrip.com/" as base url and append this image link. |
| details.address | Full activity address information |
| details.address.address_type | Address_type either will be activity address or pickup address of this activity |
| details.open_activity | True or false (true represent unschedule activity and false represent schedule activity) |
| details.rates | List of all rate available for this activity or variant |
| details.rates.cheapest | This is cheapest price we will use to show on ui for adult(adt) , child(chd) and group(unit)|
| details.rates.is_unit_type | True or false, true represent this activity is a group activity |
| details.rates.rate_id | Id of rates |
| details.rates.cancellation | List of cancellation policy available |
| details.rates.cancellation.charge_type | 1 or 2, 1 represent flat cancellation charge in given currency and 2 represent flat cancellation in %. |
| details.rates.cancellation.lead_hour | From 0 to given hour value |
| details.rates.cancellation.value | Cancellation value depends on charge_type currency or percentage |
| details.rates.prices | List of pricing available for this activity like weekday and weekends price |
| details.description | Full description of this activity or variant |
| details.trust_marker | Booking details on last few hours |
| details.one_line_description| One line description of this activity or variant |
| details.recommended_traveller_type | List of all suitable traveller type. E.g Couple, Kids, Solo, Group etc |
| details.highlights | List of highlights for an activity |
| details.variation_id | This is variant id for for this activity |


If the search was successful, the response body returns an JSON along with the HTTP status code 200. If any error is encountered during the search, the response body contains an JSON with the root element error_code. See the schema and sample search result JSON for more details.

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |

| Please specify the city | city-id is missing.|
| Please specify the variant id | variant-id is a required field.|

### 1.5 Search City

#### Intent

`search_city`

This API is used to search for a required city

### Payload
```
{
  "intent":"search_city",
  "data":{
  	"city":""
    
  }
}

```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| city | City string |

### Response Body
```
"bangalore": {
        "ttd": true,
        "count": 1,
        "fnb": true
    },
 ```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| ttd | Contains True/False based on availability in the corresponding city |
| fnb | Contains True/False based on availability in the corresponding city |


If the search was successful, the response body returns an JSON along with the HTTP status code 200. If any error is encountered during the search, the response body contains an JSON with the root element error_code. See the schema and sample search result JSON for more details.

### 1.6 Check Availability

#### Intent

`availability_check_ttd`

The availability request takes the rate id as input and provides the details of activity availability information with date, time slot and availability count.

### Payload
```
{
  "intent":"availability_check_ttd",
  "data":{
  		"rate_id":"83219",
  		"scr":"INR",
  		"sct":"IN"
  }
}

```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| rate_id | rateid |
| scr | Currency of city ex -  INR (india) |
| sct | City initials ex - IN (india) |

### Response Body
```
{
type : "S"
crc : "INR"
inv[]
}
 ```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| currency | The currency in which the prices of activities are displayed. |
| type | "S" or "O" Schedule (S) or Open or Schedule(O) activity inventory |
| cf | convenience fee details |
| inv | List of inventory are available to book with date respective |
| inv.time_slot_inventory | List of time slot on different date |
| inv.time_slot_inventory.min| Minimum count required |
| inv.time_slot_inventory.max | Maximum count available to book |
| inv.time_slot_inventory.adult_price | On this time slot adult price |
| inv.time_slot_inventory.child_price | On this time slot adult price |
| inv.time_slot_inventory.unit_price| On this time slot group or unit price |
| inv.time_slot_inventory.status | RATE_UNAVAILABLE("U"), AVAILABLE("A"), EARLY("E"), LATE("L"), BLACK_OUT("B"), SOLD_OUT("S"), INVALID_TIME_SLOT("TS") possible status code |
| ts | Time slot value on different day or date, ts value will present only for open activity with time slot, and pick time slot value from ts_key value from inv.time_slot_inventory.ts_key |

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |

| Please specify the rate id | rate-id is a required field.|

### 1.7 Create Itinerary

#### Intent

`create_itinerary`

The user sends an itinerary request to create an itinerary on the cleartrip servers. All the relevant booking details are collected from the user. This Create itinerary request will be different for different case like schedule, unschedule, individual, group. Please find the possible case sample request to create itinerary. Once an itinerary has been created, an itinerary-id is assigned. An itinerary is available only for an hour after it has been created. At the end of one hour, an itinerary is expired and it is not possible to fetch the details (unless the itinerary was booked, and at this point it becomes a trip, and its details can be fetched using the retrieve trip service).

### Payload
```
{
  "intent":"create_itinerary",
  "data":{
  	"categoryId":"ttd",
  	"itinerary_data":{
  		 "date": "10/11/2017",
    	"activity_id": "807322",
    	"pricing": "INDIVIDUAL",
    	"adults": "1",
    	"rate_id": "43157",
    	"variantion_id": "4274",
    	"scr": "INR",
    	"sct": "IN"
  	}
  }
}

```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |

| itinerary_data | Object with Itinerary Data |
| date | Date  |
| date | Currency of city ex -  INR (india) |
| activity_id | Activity ID |
| pricing | Pricing type |
| adults/ children / units | No of adults / children / units |
| rate_id | rate_id |
| variantion_id | Variant ID  |
| scr | Currency of city ex -  INR (india) |
| sct | City initials ex - IN (india) |

### Response Body
```
{
bf : "2"
ItineraryId : "1565e1678d-0fed-4028-ab32-4bc78b05e17e"
tot : "2"
end_time : "2017-10-13T02:00"
start_time : "2017-10-13T01:00"
tt : "0"
dur_m : "0"
dur_d : "0"
dur_h : "1"
crc : "INR"
displayNames : "11.39 stack 2 activityy"
}
 ```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| crc | Currency in which the activity price are display. |
| dur_h | Activity duration in hour |
| dur_m | Activity duration in mins |
| dur_d | activity duration in day |
| tt | Total tax on this activity |
| itineraryId | Itinerary id of this activity |
| start_time | Start time of this activity |
| end_time | End time of this activity |
| tot | Total price of this activity |
| displayNames | Display name for this activity |


### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the date | Date is required |
| Please specify the activity id | Missing activity id |
| Please specify the pricing | Missing pricing |
| Please specify the rate id | Missing rate id |
| Please specify the variant id | Missing variant id |


### 1.8 Book Itinerary

#### Intent
`confirm_booking`

#### Request Params Description
| KEYWORD | DESCRIPTION |
| ---|--- |
| itineraryid | Id of the created itenerary |
| user_details | Id of the created user details |
| title | User Title Ex: Mr or Ms or Mrs |
| firstName | User's first name |
| lastName | User's last name |
| userName | User's email. Booking confirmation will be sent to this email |
| mobileNumber | User's mobile number. SMS Confirmation will be sent to this mobile number |
| bookingRef | Any booking reference value from your end to map with our details |

#### Payload
```
{
  "intent":"confirm_booking",
  "data":{
  	"itineraryid":"157d88fc41-4253-4517-847a-f30e8f7c956a",
  	"user_details":{
  	 	"title" : "Mr",
		"firstName": "Ashiq",
		"lastName" : "Ali",
		"userName" : "karthik@appsfly.io",
		"mobileNumber" : "961916308",
		"bookingRef" : "Appsfly123"
  	}
  }
}
```
### Response Params Description
{
   "success": {
       "trip_id": "Q1700990001",
       "vaucher_no": "CAMP-168161"
   }
}

| KEY | DESCRIPTION |
| ---|--- |
| success | This tag will contain trip id and voucher number for that successfull booking |

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the itinerary id |  Itinerary id is a required field. |

### Status / Error Codes

Status Codes 
All status codes are standard HTTP status codes. The below ones are used in this API.

2XX - Denotes successful transaction with the server.
4XX - Error occurred on the client side
5XX - Error occurred on the server side

 
| Status Code | Description|
| ---|--- |
| 200 | OK |
| 201 | Created |
| 202 | Accepted (Request accepted, and queued for execution) |
| 400 | Bad request |
| 401 | Authentication failure |
| 403 | Forbidden |
| 404 | Resource not found |
| 405 | Method Not Allowed |
| 409 | Conflict |
| 412 | Precondition Failed |
| 413 | Request Entity Too Large |
| 500 | Internal Server Error |
| 501 | Not Implemented |
| 503 | Service Unavailable |


--------------------------------------------------------------------------------

## Local eatout 

microapp_handle : `com.cleartrip.microservices.local.eatouts`

### 2.1 City List

#### Intent
`city_list`

City list api will list all the available cities and there product type availability in that city. The search request is a simple HTTP GET request. The sample request described below should be sent along with the URL, and the user’s API key in the HTTP headers. A successful response will always return the HTTP status code 200. (Note that a status code of 200 doesn’t necessarily mean that the search result will be returned; but a successful search will always return a status code of 200).

### Response Body
```
"bangalore": {
        "ttd": true,
        "count": 1,
        "fnb": true
    },
 ```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| ttd | Contains True/False based on availability in the corresponding city |
| fnb | Contains True/False based on availability in the corresponding city |

If the search was successful, the response body returns an JSON along with the HTTP status code 200. If any error is encountered during the search, the response body contains an JSON with the root element error_code. See the schema and sample search result JSON for more details.


### 2.2 Restaurants List

#### Intent
`restaurants_list_ttd`

Provides the Cleartrip Restaurant Listing for a City. The search request is a simple HTTP GET request. The query parameters described below should be sent along with the search URL, and the user’s API key in the HTTP headers. A successful response will always return the HTTP status code 200. (Note that a status code of 200 doesn’t necessarily mean that the search result will be returned; but a successful search will always return a status code of 200).
City list api also take tags as optional params and return the data related to tags, otherwise 400 for requested api.
 
### Payload
```
{
  "intent":"restaurants_list_fnb",
  "data":{
  	"cityName":"bangalore"
  }
}

```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| cityName | Name of city |

### Response Body 
```
{
scr : "INR"
collections[],
city{},
chains[],
categories : null,
sid : "90fcba7f-4a32-4abd-8f11-88815e4b88af",
time_slot{}
}
```

### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| currency | The currency in which the prices of activities are displayed  |
| collections | List of collections available on this city and it's details |
| collections.count | Number of activities available for this collections |
| collections.rank | Sequence order to show on ui |
| collections.id | Collection id of the collection |
| collections.categories | List of categories id which this collection belong |
| collections.name | Name of the collection |
| collections.desc | Description of this collection |
| collection.image | Image Image link we can use by adding "http://ui.cltpstatic.com/" or "http://apistaging.cleartrip.com/" as base url|
| city | City name and city id for further use |
| city.name | Name of the city |
| city.id | Id of the city |
| categories | List of all categories for these collections |
| categories.name | Name of the categories |
| categories.rank | Sequence order of list of categories |
| categories.id | Id of categories |

If the search was successful, the response body returns an JSON along with the HTTP status code 200. If any error is encountered during the search, the response body contains an JSON with the root element error_code. See the schema and sample search result JSON for more details.

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the city | City is missing. |
 
### 2.3 Eatouts List

#### Intent
`eatout_list`

The collection info request takes the collection Id and city Id as input and provides the brief activities information which are part of that collections, along with the thumbnail and wide-angle image URL in response.
Note: Some of the activities might overlap in different collections
Example: Wonderla activity might get listed as part of 'Theme Parks' as well as 'Water Sprots' collections.
Collection info api also take tags as optional params and return the data related to tags, otherwise 400 for requested api.


### Payload
```
{
  "intent":"eatout_list",
  "data":{
  	"city_id":"32550",
  	"id":"25270" 
  }
}
 

```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| city_id | City ID  |
| id | Collection ID from collection list API |

### Response Body 
```
{
result[],
scr : "INR"
web_url : "/local/bangalore/20-discount-vouchers-in-bangalore-collection-25270-2"
extras{},
collection{},
sid : "fb04df53-e96d-4300-aac8-cc6710f653cd"
}
```

### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| currency | The currency in which the prices of activities are displayed  |
| result | Show list of variant or activities on this collections|
| result.image| Image Image link we can use by adding "http://ui.cltpstatic.com/" or "http://apistaging.cleartrip.com/" as base url |
| result.address | Full activity address information |
| result.address.address_type | Address_type either will be activity address or pickup address of this activity |
| result.address.locality_name | locality name of activity |
| result.price | Activity price in requested currency format |
| result.name | Name of the activity |
| result.activity_id | Id of activity|
| result.id | Id of variant |
| result.timings | Activity or variant start time |
| result.published_time | When this activity or variant published in datetime format |
| extras |extras value will present fnb product type only. |
| extras.localities | list of localities which are all mapped to results.address.locality_name value |
| extras.tag | all different tag type value |
| collection | Show collection information in details |
| details | This details will be present if we have only one variant or activity in a collections |

If the search was successful, the response body returns an JSON along with the HTTP status code 200. If any error is encountered during the search, the response body contains an JSON with the root element error_code. See the schema and sample search result JSON for more details.

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the city | city-id is missing.|
| Please specify the collection-id | collection-id is a required field.|

### 2.4 Eatout Details

#### Intent
`eatout_details_ttd`

The activity details info request takes the result’s id and city id as input and provides the detailed activity information along with the thumbnail and wide-angle image URL in response. 
Note :For FNB details you need to pass activity-id from result's list as mandatory parameter to get the details. If needs to get categories for this activity we need to just pass categories=true in request parameters.


### Payload
```
{
  "intent":"eatout_details_fnb",
  "data":{
  	"city_id":"32550",
  	"id":"71864",
  	"activity_id":"813588"
  }
}

```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| city_id | City ID  |
| id | Selected Variant ID from activity list api |
| activity_id | Selected Activity ID from activity list api  |

### Response Body 
```
{
scr : "INR",
web_url : "/local/bangalore/bakasur-20-discount-in-bangalore-71864-2",
details{},
sid : "5f8aa59f-0a4f-4983-b623-2871013907f5",
}
```

### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| currency | The currency in which the prices of activities are displayed  |
| details | Show complete details of this activity or variant |
| details.activity_name| Name of the activity |
| details.published_time | Name of the variant |
| details.variant_name | Address_type either will be activity address or pickup address of this activity |
| details.images | List of image for this activity or variant |
| details.images.img |Image link we can use by adding "http://ui.cltpstatic.com/" or "http://apistaging.cleartrip.com/" as base url and append this image link. |
| details.address | Full activity address information |
| details.address.address_type | Address_type either will be activity address or pickup address of this activity |
| details.open_activity | True or false (true represent unschedule activity and false represent schedule activity) |
| details.rates | List of all rate available for this activity or variant |
| details.rates.cheapest | This is cheapest price we will use to show on ui for adult(adt) , child(chd) and group(unit)|
| details.rates.is_unit_type | True or false, true represent this activity is a group activity |
| details.rates.rate_id | Id of rates |
| details.rates.cancellation | List of cancellation policy available |
| details.rates.cancellation.charge_type | 1 or 2, 1 represent flat cancellation charge in given currency and 2 represent flat cancellation in %. |
| details.rates.cancellation.lead_hour | From 0 to given hour value |
| details.rates.cancellation.value | Cancellation value depends on charge_type currency or percentage |
| details.rates.prices | List of pricing available for this activity like weekday and weekends price |
| details.description | Full description of this activity or variant |
| details.trust_marker | Booking details on last few hours |
| details.one_line_description| One line description of this activity or variant |
| details.recommended_traveller_type | List of all suitable traveller type. E.g Couple, Kids, Solo, Group etc |
| details.highlights | List of highlights for an activity |
| details.variation_id | This is variant id for for this activity |
| details.ratings | Complete information of ratings & reviews for an activity |
| details.group_activity | True or False, true represent it's group(UNIT) and false means INDIVIDUAL activity|
| details.meeting_point | Meeting point address details if available |
| details.pick_up_points | Pickup point address details if available |


If the search was successful, the response body returns an JSON along with the HTTP status code 200. If any error is encountered during the search, the response body contains an JSON with the root element error_code. See the schema and sample search result JSON for more details.

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the city | city-id is missing.|
| Please specify the variant id | variant-id is a required field.|
| Please specify the activity id | activity-id is a required field.|


### 2.5 Search City

#### Intent

`search_city`

This API is used to search for a required city

### Payload
```
{
  "intent":"search_city",
  "data":{
  	"city":""
    
  }
}

```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| city | City string |

### Response Body
```
"bangalore": {
        "ttd": true,
        "count": 1,
        "fnb": true
    },
 ```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| ttd | Contains True/False based on availability in the corresponding city |
| fnb | Contains True/False based on availability in the corresponding city |


If the search was successful, the response body returns an JSON along with the HTTP status code 200. If any error is encountered during the search, the response body contains an JSON with the root element error_code. See the schema and sample search result JSON for more details.

### 2.6 Check Availability

#### Intent

`availability_check_fnb`

The availability request takes the rate id as input and provides the details of activity availability information with date, time slot and availability count.

### Payload
```
{
  "intent":"availability_check_fnb",
  "data":{
  		"rate_id":"83219",
  		"scr":"INR",
  		"sct":"IN"
  }
}

```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| rate_id | rateid |
| scr | Currency of city ex -  INR (india) |
| sct | City initials ex - IN (india) |

### Response Body
```
{
type : "S"
crc : "INR"
inv[]
}
 ```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| currency | The currency in which the prices of activities are displayed. |
| type | "S" or "O" Schedule (S) or Open or Schedule(O) activity inventory |
| cf | convenience fee details |
| inv | List of inventory are available to book with date respective |
| inv.time_slot_inventory | List of time slot on different date |
| inv.time_slot_inventory.min| Minimum count required |
| inv.time_slot_inventory.max | Maximum count available to book |
| inv.time_slot_inventory.adult_price | On this time slot adult price |
| inv.time_slot_inventory.child_price | On this time slot adult price |
| inv.time_slot_inventory.unit_price| On this time slot group or unit price |
| inv.time_slot_inventory.status | RATE_UNAVAILABLE("U"), AVAILABLE("A"), EARLY("E"), LATE("L"), BLACK_OUT("B"), SOLD_OUT("S"), INVALID_TIME_SLOT("TS") possible status code |
| ts | Time slot value on different day or date, ts value will present only for open activity with time slot, and pick time slot value from ts_key value from inv.time_slot_inventory.ts_key |

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.
| Error message | Description |
| ---|--- |

| Please specify the rate id | rate-id is a required field.|

### 2.7 Create Itinerary

#### Intent

`create_itinerary`

The user sends an itinerary request to create an itinerary on the cleartrip servers. All the relevant booking details are collected from the user. This Create itinerary request will be different for different case like schedule, unschedule, individual, group. Please find the possible case sample request to create itinerary. Once an itinerary has been created, an itinerary-id is assigned. An itinerary is available only for an hour after it has been created. At the end of one hour, an itinerary is expired and it is not possible to fetch the details (unless the itinerary was booked, and at this point it becomes a trip, and its details can be fetched using the retrieve trip service).

### Payload
```
{
  "intent":"create_itinerary",
  "data":{
  	"categoryId":"ttd",
  	"itinerary_data":{
  		 "date": "10/11/2017",
    	"activity_id": "807322",
    	"pricing": "INDIVIDUAL",
    	"adults": "1",
    	"rate_id": "43157",
    	"variantion_id": "4274",
    	"scr": "INR",
    	"sct": "IN"
  	}
  }
}

```
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |

| itinerary_data | Object with Itinerary Data |
| date | Date  |
| date | Currency of city ex -  INR (india) |
| activity_id | Activity ID |
| pricing | Pricing type |
| adults/ children / units | No of adults / children / units |
| rate_id | rate_id |
| variantion_id | Variant ID  |
| scr | Currency of city ex -  INR (india) |
| sct | City initials ex - IN (india) |

### Response Body
```
{
bf : "2"
ItineraryId : "1565e1678d-0fed-4028-ab32-4bc78b05e17e"
tot : "2"
end_time : "2017-10-13T02:00"
start_time : "2017-10-13T01:00"
tt : "0"
dur_m : "0"
dur_d : "0"
dur_h : "1"
crc : "INR"
displayNames : "11.39 stack 2 activityy"
}
 ```
### Response Params Description

| KEY | DESCRIPTION |
| ---|--- |
| crc | Currency in which the activity price are display. |
| dur_h | Activity duration in hour |
| dur_m | Activity duration in mins |
| dur_d | activity duration in day |
| tt | Total tax on this activity |
| itineraryId | Itinerary id of this activity |
| start_time | Start time of this activity |
| end_time | End time of this activity |
| tot | Total price of this activity |
| displayNames | Display name for this activity |


### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the date | Date is required |
| Please specify the activity id | Missing activity id |
| Please specify the pricing | Missing pricing |
| Please specify the rate id | Missing rate id |
| Please specify the variant id | Missing variant id |

### 2.8 Book Itinerary

#### Intent
`confirm_booking`

#### Request Params Description
| KEYWORD | DESCRIPTION |
| ---|--- |
| itineraryid | Id of the created itenerary |
| user_details | Id of the created user details |
| title | User Title Ex: Mr or Ms or Mrs |
| firstName | User's first name |
| lastName | User's last name |
| userName | User's email. Booking confirmation will be sent to this email |
| mobileNumber | User's mobile number. SMS Confirmation will be sent to this mobile number |
| bookingRef | Any booking reference value from your end to map with our details |

#### Payload
```
{
  "intent":"confirm_booking",
  "data":{
  	"itineraryid":"157d88fc41-4253-4517-847a-f30e8f7c956a",
  	"user_details":{
  	 	"title" : "Mr",
		"firstName": "Ashiq",
		"lastName" : "Ali",
		"userName" : "karthik@appsfly.io",
		"mobileNumber" : "961916308",
		"bookingRef" : "Appsfly123"
  	}
  }
}
```
### Response Params Description
{
   "success": {
       "trip_id": "Q1700990001",
       "vaucher_no": "CAMP-168161"
   }
}

| KEY | DESCRIPTION |
| ---|--- |
| success | This tag will contain trip id and voucher number for that successfull booking |

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the itinerary id |  Itinerary id is a required field. |

### Status / Error Codes

Status Codes 
All status codes are standard HTTP status codes. The below ones are used in this API.

2XX - Denotes successful transaction with the server.
4XX - Error occurred on the client side
5XX - Error occurred on the server side

 
| Status Code | Description|
| ---|--- |
| 200 | OK |
| 201 | Created |
| 202 | Accepted (Request accepted, and queued for execution) |
| 400 | Bad request |
| 401 | Authentication failure |
| 403 | Forbidden |
| 404 | Resource not found |
| 405 | Method Not Allowed |
| 409 | Conflict |
| 412 | Precondition Failed |
| 413 | Request Entity Too Large |
| 500 | Internal Server Error |
| 501 | Not Implemented |
| 503 | Service Unavailable |
