# ClearTrip Micro Services

1. [Local Activities](#local-activities)
    * [City List](#11-city-list)
    * [Collections List](#12-collections-list)
    * [Activity List](#13-activity-list)
    * [Activity Details](#14-activity-details)
    * [Search City](#15-search-city)
    * [Check Availability](#16-check-availability)
    * [Create Itinerary](#17-create-itinerary)
    * [Book Itinerary](#18-book-itinerary)
    * [Retrieve Trip](#19-retrieve-trip)
  
2. [Local Eatout](#local-eatout)
    * [City List](#21-city-list)
    * [Collections List](#22-collections-list)
    * [Restaurants List](#23-restaurants-list)
    * [Eatout Details](#24-eatout-details)
    * [Search City](#25-search-city)
    * [Check Availability](#26-check-availability)
    * [Create Itinerary](#27-create-itinerary)
    * [Book Itinerary](#28-book-itinerary)
    * [Retrieve Trip](#29-retrieve-trip)

--------------------------------------------------------------------------------
You can find Integration Details [Integration Doc](https://github.com/appsflyio/devkit-javautils)
--------------------------------------------------------------------------------


## Local Activities 

### 1.1 City List

#### Intent
`fetch_cities`

#### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| CITY_NAME | Name of city |

#### Response Body
```
[
"CITY_NAME": {
        "ttd": ${TTD},
        "count": ${COUNT},
        "fnb":  ${FNB}
    }...
]
 ```
### 1.2 Collections List

#### Intent
`fetch_collections`

#### Request Params Description
| KEY | DESCRIPTION |
| ---|--- |
| CITY_NAME | Name of city |

#### Payload
```
{
	"cityName":"${CITY_NAME}"   
}
```

#### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| IMAGE |Image Image link we can use by adding "http://ui.cltpstatic.com/" or "http://apistaging.cleartrip.com/" as base url|
| COUNT | Number of activities available for this collections |
| COLLECTION_NAME| Name of the collection |
| COLLECTION_ID | Collection id of the collection |
| CITY_ID | Id of the city |

#### Response Body 
```
[
 {
    "image": "${IMAGE}",
    "count": ${COUNT},
    "collectionName": "${COLLECTION_NAME}",
    "collectionId": ${COLLECTION_ID},
    "cityId": ${CITY_ID}
  }...
]
```

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the city | City is missing. |
 
### 1.3 Activity List

#### Intent
`fetch_activity`

#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| CITY_ID | City ID  |
| COLLECTION_ID | Collection ID from collection list API |    

### Payload
```
{
  	"cityId":"${CITY_ID},
  	"collectionId":"${COLLECTION_ID}"
}
```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| IMAGE|Image Image link we can use by adding "http://ui.cltpstatic.com/" or "http://apistaging.cleartrip.com/" as base url |
| PRICE | Activity price in requested currency format |
| NAME | Name of the activity |
| ACTIVITY_ID | Id of activity |
| VARIATION_ID | Id of variant |
| CITY_ID | Id of the city |
| LOCALITY | locality name of activity |

### Response Body 
```
[
   {
    "image": "${IMAGE}",
    "price": ${PRICE},
    "name": "${NAME}",
    "activityId": ${ACTIVITY_ID},
    "variationId": ${VARIATION_ID},
    "cityid": "${CITY_ID}",
    "locality": "${LOCALITY}"
  }...  
]
```

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the city | city-id is missing.|
| Please specify the collection-id | collection-id is a required field.|

### 1.4 Activity Details

#### Intent
`fetch_activity_details`

#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| CITY_ID | City ID  |
| VARIATION_ID | Selected variant id of the activity list api |  

### Payload
```
{
  	"cityId":"${CITY_ID},
  	"variationId":"${VARIATION_ID}"
}

```

### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| IS_GST_APPLICABLE | True or false (true represent GST applicable and false represent GST not applicable) |
| IMAGES | List of image for this activity or variant |
| IMAGES.IMAGE | Image for this activity or variant |
| IMAGES.ORDER_NO | No of the order |
| ACTIVITY_ID | Id of activity |
| ACTIVITY_NAME |Name of activity |
| INCLUSIONS | List of inclusions given to the activity |
| ADDRESS | Full activity address information |
| ADDRESS.COUNTRY | Country Name of the activity |
| ADDRESS.ADDRESS_TYPE | Address_type either will be activity address or pickup address of this activity |
| ADDRESS.ADDRESS2 | Secondary if activity exists in more than one place |
| ADDRESS.CITY | City of the activity |
| ADDRESS.ADDRESS1 | Primary address of the actvity |
| ADDRESS.LATITUDE | Latitude of the location of the activity  |
| ADDRESS.STATE | State of the activity  |
| ADDRESS.LONGITUDE | Longitude of the location of the activity  |
| ADDRESS.LOCALITY_NAME | locality name of activity  |
| CHILD_AGE_RESTRICTION | Minimum age of the child for entry  |
| DESCRIPTION | Full description of this activity or variant |
| SINGLE_LINE_DESCRIPTION | One line description of this activity or variant |
| RATINGS.BAD | Array of bad ratings |
| RATINGS.GOOD | Array of good ratings |
| RATINGS.AVG_RATING | Average of the overall ratings |
| RATINGS.RATINGS_COUNT | Total number of the ratings |
| RATINGS.REVIEW_COUNT | Total no of reviews |
| RATINGS.REVIEW | Array of review |
| PUBLISHED_TIME | Date and time of the activity published |
| MEETINGPOINT | Meeting point of the activity if avaliable else null |
| PICKUP_POINTS | Pickup points of the activity if avaliable else null |
| OPEN_ACTIVITY | True or false (true represent unschedule activity and false represent schedule activity) |
| DRESSCODE | Dress code for the actvity |
| RATES | List of all rate available for this activity or variant |
| RATES.CHEAPEST_RATES | This is cheapest price we will use to show on ui for adult(adt) , child(chd) and group(un
| RATES.IS_UNIT_TYPE | True or false, true represent this activity is a group activity |
| RATES.RATE_ID | Id of rates |
| RATES.CANCELLATION | List of cancellation policy available |
| RATES.CANCELLATION.CHARGE_TYPE | 1 or 2, 1 represent flat cancellation charge in given currency and 2 represent flat cancellation in %. |
| RATES.CANCELLATION.LEAD_HOUR | From 0 to given hour value |
| RATES.CANCELLATION.VALUE | Cancellation value depends on charge_type currency or percentage |
| RATES.PRICES | List of pricing available for this activity like weekday and weekends price |
| RATES.WHEN | List of time and duration|
| RATES.WHEN.DURATION | Duration of the activity |
| RATES.WHEN.IS_AVALIABLE_TODAY | True or false (true represent actvity is avaliable for current date and false represent activity is not avaliable) |
| RATES.WHEN.EXPAND|True or false (true represent actvity can be expand than the timings and false represent can not expand |
| RATES.WHEN.TIMINGS | Timings of the activity |
| RATES.INCLUSIONS | Inclusions for the activity |
| RATES.RATE_NAME | Name of the rates |
| RATES.ORDER | Order of the rates |
| RATES.ABOUT | About the rates |
| HIGHLGHTS | List of highlights for an activity |
| MIN_PRICE | Minimun price os the activity |
| VARIATION_ID | This is variant id for for this activity if avaliable else null |
| GROUP_ACTIVITY | True or false (true represent actvity is group activity  and false represent activity is not group activity)|

### Response Body 
```
{
	"isGstApplicable": ${IS_GST_APPLICABLE},
	"images": [{
      		"order_no": "${ORDER_NO}",
      		"image": "${IMAGE}"
   	}..],
	"activityId": ${ACTIVITY_ID},
  	"activityName": "${ACTIVITY_NAME}",
	"inclusions": [
        		"${INCLUSIONS}",...
		      ],
        "address": {
        	   "country": "${COUNTRY}",
       		   "address_type": "${ADDRESS_TYPE}",
        	   "address2": "${ADDRESS2},
        	   "city": "${CITY}",
        	   "address1": "${ADDRESS1}",
        	   "pin_code": "${PINCODE]",
                   "latitude": "${LATITUDE}",
                   "state": "${STATE}",
                   "longitude": "${LONGITUDE}",
        	   "city_id": ${CITY_ID},
                   "locality_name": "${LOCALITY_NAME}"
    },
    "childAgeRestriction": "${CHILD_AGE_RESTRICTION}",
    "description": "${DESCRIPTION}"
    "singleLineDescription": "${SINGLE_LINE_DESCRIPTION]",
    "ratings": {
        "bad": [],
        "review": ${REVIEW},
        "avg_rating": ${AVG_RATING},
        "ratings_count": ${RATINGS_COUNT},
        "good": [],
        "reviews_count": ${REVIEW_COUNT}
    },
     "publishedTime": "${PUBLISHED_TIME}",
    "meetingPoint": ${MEETING_POINT},
    "pickUpPoints": ${PICKUP_POINTS},
    "open_activity": ${OPEN_ACTIVITY},
    "dressCode": [
    	${DRESSCODE}...],
    "rates": [
        {
            "cheapest_rates": {
                "adt": ${ADT},
                "unit": ${UNIT},
                "chd": ${CHD}
            },
            "is_unit_type": false,
            "cancellation": [
                {
                    "charge_type": "${CHARGE_TYPE}",
                    "rate_id": ${RATE_ID},
                    "lead_hour": ${LEAD_HOUR},
                    "value": ${VALUE}
                }...,
            ],
            "rate_id": ${RATE_ID},
            "about": [${ABOUT}],
            "prices": [${PRICES}],
            "when": {
                "duration": "${DURATION}",
                "isAvailableToday": ${IS_AVALIABLE_TODAY},
                "expand": ${EXPAND},
                "timings": "${TIMINGS}"
            },
            "inclusions": [${INCLUSIONS}],
            "rate_name": "{${RATE_NAME}}",
            "order": ${ORDER}
        }
    ],
    "highlights": [${HIGHLIGHTS}...,
    ],
    "minPrice": ${MIN_PRICE},
    "variationId": ${VARIATION_ID},
    "groupActivity": ${GROUP_ACTIVITY}    
}
```

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |

| Please specify the city | city-id is missing.|
| Please specify the variant id | variant-id is a required field.|

### 1.5 Search City

#### Intent

`search_city`
#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| CITY_NAME | City string |

### Payload
```
{
	"city": "${CITY_NAME}"
}

```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| ttd | Contains True/False based on availability in the corresponding city |
| fnb | Contains True/False based on availability in the corresponding city |

### Response Body
```
[
"CITY_NAME": {
        "ttd": ${TTD},
        "count": ${COUNT},
        "fnb":  ${FNB}
    }...
]
 ```

### 1.6 Check Availability

#### Intent

`get_available_slots`

#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| RATE_ID | rateid |

### Payload
```
{
  "rateId":"${RATE_ID}"
}

```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| DATE | Avaliable dates for the activity |
| ADT_PRICE | Adult price for the activity |
| CHD_PRICE | Child price for the activty |
| MIN | Minimum count of people |
| MAX | Maximum count of people |
| TIMESLOTS | List of time slot on different date |

### Response Body
```
[
 {
        "date": "${DATE}",
        "adult_price": "${ADT_PRICE}",
        "child_price": "${CHD_PRICE}",
        "min": ${MIN_COUNT},
        "max": ${MAX_COUNT}",
        "timeSlots": [${TIMESLOTS]..]
    }...,
]
 ```
### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the rate id | rate-id is a required field.|

### 1.7 Create Itinerary

#### Intent

`create_itinerary`

#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| ITINERARY_DATA | Object with Itinerary Data |
| ITINERARYDATA.DATE | Date  |
| ITINERARYDATA.ACTIVITY_ID | Activity ID |
| ITINERARYDATA.PRICING | Pricing type |
| NO_OF_CHILDREN/ NO_OF_ADULTS / NO_OF_UNITS | No of adults / children / units |
| ITINERARYDATA.RATEID | rate_id |
| ITINERARYDATA.VARIANTID | Variant ID  |
| ITINERARYDATA.SCR | Currency of city ex -  INR (india) |
| ITINERARYDATA.SCT | City initials ex - IN (india) |

### Payload
```
{
  "itineraryData":{
  		 "date":"${DATE}",
		 "activityId":${ACTIVITY_ID},
		 "pricing":"${PRICING}",
		 "rateId":${RATEID},
		 "variantId":${VARIANTID},
		 "scr":"${SCR}",
		 "sct":"${SCT}",
		 "noOfChildren":${NO_OF_CHILDREN},
		 "noOfAdults":${NO_OF_ADULTS}
  	}
}
```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| CRC | Currency in which the activity price are display. |
| DUR_H | Activity duration in hour |
| DUR_M | Activity duration in mins |
| DUR_D | activity duration in day |
| TT | Total tax on this activity |
| ITINERARY_ID | Itinerary id of this activity |
| START_TIME | Start time of this activity |
| END_TIME | End time of this activity |
| TOT | Total price of this activity |
| DISPLAY_NAMES | Display name for this activity |


### Response Body
```
{
	bf : "${BF}",
	ItineraryId : "${ITINERARY_ID}",
	tot : "${TOT}",
	end_time : "${END_TIME}",
	start_time : "${START_TIME}",
	tt : "${TT}",
	dur_m : "${DUR_M}",
	dur_d : "${DUR_D}",
	dur_h : "${DUR_H}",
	crc : "${CRC}",
	displayNames : "${DISPLAY_NAMES}"
}
 ```

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
| USER_DETAILS | Id of the created user details |
| TITLE | User Title Ex: Mr or Ms or Mrs |
| FIRS_TNAME | User's first name |
| LAST_NAME | User's last name |
| USER_NAME | User's email. Booking confirmation will be sent to this email |
| MOBILE_NUMBER | User's mobile number. SMS Confirmation will be sent to this mobile number |
| BOOKING_REF | Any booking reference value from your end to map with our details |

#### Payload
```
{
  "user_details":{
  	 	"title" : "${TITLE}",
		"firstName": "${FIRST_NAME}",
		"lastName" : "${LAST_NAME}",
		"userName" : "${USER_NAME}",
		"mobileNumber" : "${MOBILE_NUMBER}",
		"bookingRef" : "${BOOKING_REF}"
  }
  
}
```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| trip | JSON object with all trip details |

### Response Body
```
{“success”:
 	{
	“trip_id”:“${TRIP_ID}”,
	“voucher_no”:“${VOUCHER_NO}”
	}
}
```

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Booking failed | Booking failed |

### 1.9 Retrieve Trip

#### Intent
`fetch_booking_details`

#### Request Params Description
| KEYWORD | DESCRIPTION |
| ---|--- |
| TRIP_ID | trip id from book itinerary api |

#### Payload
```
{
  	"tripid": "${TRIP_ID}"
}
```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| TRIP | JSON object with all trip details |
| TRIP.ACTIVITY | Number of the activity |
| TRIP.BOOKING_STATUS | Status of Booking. Either P or F |
| TRIP.CREATED_AT | Booking created time |
| TRIP.CURRENCY | The currency in which the prices of activites are displayed |
| TRIP.END_DATE_TIME | Activity end date and time |
| TRIP.EXPRESS_CHECKOUT | Express Checkout if avaliable else null|
| TRIP.HAS_WALLET_PROMOTION | Wallet promotion if available else null |
| TRIP.HOTEL | Number of hotel for the activity |
| TRIP.ITINERARY_ID | Itinerary Id of the actvity |
| TRIP.START_DATE_TIME | Activity start date and time |
| TRIP.TRIP_KEY | Key of the trip |
| TRIP.TRIP_NAME | Name of the trip  |
| TRIP.TRIP_REF | Reference of the trip  |
| TRIP.TRIP_TYPE | Type of the trip  |
| TRIP.CONTACT_DETAILS | List of the contact details given in previous bookin itinerary  |
| TRIP.TRAVELLERS_DETAILS | List of the Travellers  |
| TRIP.ACTIVITIES_BOOKINGS | List of the Activity Location which is already booked  |
| TRIP.ACTIVITIES_BOOKINGS.ACTIVITY_INFOS | List of activity booking status, voucher number, etc  |
| TRIP.ACTIVITIES_BOOKINGS.ACTIVITY_ORGANISER_DETAILS | List of details about organiser of the activity  |

### Response Body
```
{  "trip": {
                "activity": ${ACTIVITY},
                "amount": "${AMOUNT}",
                "booking_status": "${BOOKING_STATUS}",
                "created_at": "${CREATED_TIME}",
                "currency": "${CURRENCY}",
                "end_date_time": "${END_DATE_TIME}",
                "express_checkout": ${EXPRESS_CHECKOUT},
                "has_wallet_promotion": ${HAS_WALLET_PROMOTION},
                "hotel": ${HOTEL},
                "itinerary_id": "${ITINERARY_ID}",
                "start_date_time": "${START_DATE_TIME}",
                
                "trip_key": ${TRIP_KEY},
                "trip_name": "${TRIP_NAME}",
                "trip_ref": "${TRIP_REF}",
                "trip_type": ${TRIP_TYPE},
             
                "contact_detail": {
                    "address": "${ADDRESS}"",
                    "email": "${USER_NAME}",
                    "first_name": "${FIRST_NAME}",
                    "landline": ${LANDLINE},
                    "last_name": "${LAST_NAME}",
                    "mobile": "${MOBILE_NUMBER}",
                    "title": "${TITLE}"
                },
                "travellerDetails": {
                    "ADT": ${NO_OF_ADULTS},
                    "CHD": ${NO_OF_CHILDREN}
                },
                "gst_charged_by_supplier": true,
                "gst_charged_by_cleartrip": true,
                "is_reviewed": false,
                "activities_bookings": {
                    "address": "${ADDRESS}",
                    "children": ${NO_OF_CHILDREN},
                    "latitude": "${LATITUDE}",
                    "adults":${NO. OF ADULTS, ,
                    "activity_booking_infos": [
                        {
                            "booking_status": "${BOOKING_STATUS}",
                            "pax_info_seq_no": ${PAX_INFO_SEQ_NO},
                            "seq_no": ${SEQ_NO},
                            "voucher_number": "${VOUCHER_NUMBER}",
                            "class_schedules": [

                            ]
                        }
                    ],
                    "activity_organiser_detail": {
                        "first_name": "${FIRST_NAME}",
                        "last_name": "${LAST_NAME}",
                        "image_url": "${IMAGE}",
                        "email": "${USER_NAME}",
                        "phone": "${MOBILE_NUMBER]"
                    }
                    "inclusions": "${INCLUSIONS}",
                    "longitude": "${LONGITUDE}"
                }
            }
}
```

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Booking failed | Booking failed |

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
### 2.1 City List

#### Intent
`fetch_cities`

#### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| CITY_NAME | Name of city |

#### Response Body
```
[
"CITY_NAME": {
        "ttd": ${TTD},
        "count": ${COUNT},
        "fnb":  ${FNB}
    }...
]
 ```
### 2.2 Collections List

#### Intent
`fetch_collections`

#### Request Params Description
| KEY | DESCRIPTION |
| ---|--- |
| CITY_NAME | Name of city |

#### Payload
```
{
	"cityName":"${CITY_NAME}"   
}
```

#### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| IMAGE |Image Image link we can use by adding "http://ui.cltpstatic.com/" or "http://apistaging.cleartrip.com/" as base url|
| COUNT | Number of activities available for this collections |
| COLLECTION_NAME| Name of the collection |
| COLLECTION_ID | Collection id of the collection |
| CITY_ID | Id of the city |

#### Response Body 
```
[
 {
    "image": "${IMAGE}",
    "count": ${COUNT},
    "collectionName": "${COLLECTIONNAME}",
    "collectionId": ${COLLECTIONID},
    "cityId": ${CITY_ID}
  }...
]
```

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the city | City is missing. |
 
### 2.3 Restaurants List

#### Intent
`fetch_restaurants`

#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| CITYID | City ID  |
| COLLECTION_ID | Collection ID from collection list API |    

### Payload
```
{
  	"cityId":"${CITY_ID},
  	"collectionId":"${COLLECTION_ID}"
}
```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| CHAIN_IMAGE|Image link we can use by adding "http://ui.cltpstatic.com/" or "http://apistaging.cleartrip.com/" as base url |
| PRICE | Activity price in requested currency format |
| CHAIN_NAME | Name of the activity |
| RATING | Rating of activity |
| VARIATION_ID | Id of variant |
| CITY_ID | Id of the city |
| LOCALITY | locality name of activity |
| VARIANTS | List of Variats of activity |
| VARIANTS.IMAGE | Image of Variats of activity |
| VARIANTS.PRICE | Price of Variats of activity |
| VARIANTS.NAME | Name of Variats of activity |
| VARIANTS.CUISINE | List of cuisines in variant |
| VARIANTS.VARIATION_ID | Variant Id of the Variant.  |

### Response Body 
```
[
   {
    "chain_image": "${CHAIN_IMAGE}",
    "price": ${PRICE},
    "chainName": "${CHAIN_NAME}",
    "activityId": ${ACTIVITY_ID],
    "rating": "${RATING}",
    "cityId": "${CITY_ID}",
    "locality": "${LOCALITY}",
    "variants": [
      {
        "image": "${IMAGE}",
        "price": ${PRICE},
        "name": "${NAME}",
        "cuisine": [
          "${CUISINE]"
        ],
        "variationId": ${VARIATION_ID}
      }
    ]
  }....
]
```

### Error messages
Some error messages, you might get for an invalid search request.The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the city | city-id is missing.|
| Please specify the collection-id | collection-id is a required field.|

### 2.4 Eatout Details

#### Intent
`fetch_eatout_details`

#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| CITY_ID | City ID  |
| VARIATION_ID| Selected Variant ID from activity list api |
| ACTIVITY_ID | Selected Activity ID from activity list api  |


### Payload
```
{
  	"city_id":"181385",
  	"variationId":"58580",
  	"activityId":"903172"
}

```

### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| ISGSTAPPLICABLE | True or false (true represent GST applicable and false represent GST not applicable) |
| IMAGES | List of image for this activity or variant |
| IMAGES.IMAGE | Image for this activity or variant |
| IMAGES.ORDER_NO | No of the order |
| ACTIVITY_ID | Id of activity |
| CUISINE | Name of cuisine |
| INCLUSIONS | List of inclusions given to the activity |
| ADDRESS | Full activity address information |
| ADDRESS.COUNTRY | Country Name of the activity |
| ADDRESS.ADDRESS_TYPE | Address_type either will be activity address or pickup address of this activity |
| ADDRESS.ADDRESS2 | Secondary if activity exists in more than one place |
| ADDRESS.CITY | City of the activity |
| ADDRESS.ADDRESS1 | Primary address of the actvity |
| ADDRESS.LATITUDE | Latitude of the location of the activity  |
| ADDRESS.STATE | State of the activity  |
| ADDRESS.LONGITUDE | Longitude of the location of the activity  |
| ADDRESS.LOCALITY_NAME | locality name of activity  |
| ONE_LINE_DESCRIPTION | One line description of this activity or variant |
| DRESSCODE | Dress code for the actvity |
| INCLUSIONS | Inclusions for the activity |
| IS_VEG | True or false (true represent veg and false represent nonveg) |
| IS_NON_VEG | True or false (true represent nonveg and false represent veg) |
| MIN_PRICE | Minimun price os the activity |
| VARIATION_ID | This is variant id for for this activity if avaliable else null |
| EATOUT_NAME | Name of the Eatout |
| RATES | List of all rate available for this activity or variant |
| RATES.CHEAPEST_RATES | This is cheapest price we will use to show on ui for adult(adt) , child(chd) and group(un
| RATES.IS_UNIT_TYPE | True or false, true represent this activity is a group activity |
| RATES.RATE_ID | Id of rates |
| RATES.CANCELLATION | List of cancellation policy available |
| RATES.CANCELLATION.CHARGE_TYPE | 1 or 2, 1 represent flat cancellation charge in given currency and 2 represent flat cancellation in %. |
| RATES.CANCELLATION.LEAD_HOUR | From 0 to given hour value |
| RATES.CANCELLATION.VALUE | Cancellation value depends on charge_type currency or percentage |
| RATES.PRICES | List of pricing available for this activity like weekday and weekends price |
| RATES.WHEN | List of time and duration|
| RATES.WHEN.DURATION | Duration of the activity |
| RATES.WHEN.IS_AVALIABLE_TODAY | True or false (true represent actvity is avaliable for current date and false represent activity is not avaliable) |
| RATES.WHEN.EXPAND|True or false (true represent actvity can be expand than the timings and false represent can not expand |
| RATES.WHEN.TIMINGS | Timings of the activity |
| RATES.INCLUSIONS | Inclusions for the activity |
| RATES.RATE_NAME | Name of the rates |

### Response Body 
```
{	
    "isGstApplicable": ${IS_GST_APPLICABLE},
    "images": [
        {
            "order_no": "${ORDER_NO}",
            "image": "${IMAGE}"
        }..],
    "activityId": ${ACTIVITY_ID},
    "cuisine": [
        "${CUISINE}",...],
    "oneLineDescription": "${ONE_LINE_DESCRIPTION}",
    "inclusions": [${INCLUSIONS}],
    "isVeg": ${IS_VEG},
    "isNonVeg": ${IS_NON_VEG},
    "highlights": [${HIGHLIGHTS}...,]
    "minPrice": ${MINPRICE},
    "rates": [
        {
            "cheapest_rates": {
                "adt": ${ADT},
                "unit": ${UNIT},
                "chd": ${CHD}
            },
            "is_unit_type": false,
            "cancellation": [
                {
                    "charge_type": "${CHARGE_TYPE}",
                    "rate_id": ${RATE_ID},
                    "lead_hour": ${LEAD_HOUR},
                    "value": ${VALUE}
                }...,
            ],
            "rate_id": ${RATE_ID},
            "about": [${ABOUT}],
            "prices": [${PRICES}],
            "when": {
                "duration": "${DURATION}",
                "isAvailableToday": ${IS_AVALIABLE_TODAY},
                "expand": ${EXPAND},
                "timings": "${TIMINGS}"
            },
            "inclusions": [${INCLUSIONS}],
            "rate_name": "{${RATE_NAME}}",
       
        }
    ],
    "variationId": ${VARIATION_ID},
    "eatOutName": "${EATOUT_NAME}",
    "address": {
        "country": "${COUNTRY}",
        "address_type": "${ADDRESS_TYPE}",
        "address2": ${ADDRESS2},
        "city": "${CITY}",
        "address1": "${ADDRESS1}",
        "pin_code": "${PINCODE}",
        "latitude": "${LATITUDE}",
        "state": "${STATE}",
        "longitude": "${LONGITUDE}",
        "city_id": ${CITY_ID},
        "locality_name": "${LOCALITY_NAME}"
    },
    "ratings": {${RATINGS}}
    
}
```

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

#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| CITY_NAME | City string |

### Payload
```
{
	"city": "${CITY_NAME}"
}

```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| ttd | Contains True/False based on availability in the corresponding city |
| fnb | Contains True/False based on availability in the corresponding city |

### Response Body
```
[
"CITY_NAME": {
        "ttd": ${TTD},
        "count": ${COUNT},
        "fnb":  ${FNB}
    }...
]
 ```

### 2.6 Check Availability

#### Intent

`fetch_available_slots`

#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| RATE_ID | rateid |

### Payload
```
{
  "rateId":"${RATE_ID}"
}

```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| DATE | Avaliable dates for the activity |
| ADT_PRICE | Adult price for the activity |
| CHD_PRICE | Child price for the activty |
| MIN_QUANTITY | Minimum count of people |
| MAX_QUANTITY | Maximum count of people |

### Response Body
```
[
 {
        "date": "${DATE}",
        "adultPrice": "${ADT_PRICE}",
        "childPrice": ${CHD_PRICE},
        "minQuantity": ${MIN_QUANTITY},
	"maxQuantity": ${MAX_QUANTITY}
    }...,
]
 ```
### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Please specify the rate id | rate-id is a required field.|

### 2.7 Create Itinerary

#### Intent

`create_itinerary`

#### Request Params Description

| KEYWORD | DESCRIPTION |
| ---|--- |
| ITINERARY_DATA | Object with Itinerary Data |
| ITINERARYDATA.DATE | Date  |
| ITINERARYDATA.ACTIVITY_ID | Activity ID |
| ITINERARYDATA.PRICING | Pricing type |
| NOOFCHILDREN/ NO_OF_ADULTS / NO_OF_UNITS | NO_OF_CHILDREN / children / units |
| ITINERARYDATA.RATEID | rate_id |
| ITINERARYDATA.VARIANTID | Variant ID  |
| ITINERARYDATA.SCR | Currency of city ex -  INR (india) |
| ITINERARYDATA.SCT | City initials ex - IN (india) |

### Payload
```
{
  "itineraryData":{
  		 "date":"${DATE}",
		 "activityId":${ACTIVITY_ID},
		 "pricing":"${PRICING}",
		 "rateId":${RATE_ID},
		 "variantId":${VARIANT_ID},
		 "scr":"${SCR}",
		 "sct":"${SCT}",
		 "noOfChildren":${NO_OF_CHILDREN},
		 "noOfAdults":${NO_OF_ADULTS}
  	}
}
```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| CRC | Currency in which the activity price are display. |
| DUR_H | Activity duration in hour |
| DUR_M | Activity duration in mins |
| DUR_D | activity duration in day |
| TT | Total tax on this activity |
| ITINERARY_ID | Itinerary id of this activity |
| START_TIME | Start time of this activity |
| END_TIME | End time of this activity |
| TOT | Total price of this activity |
| DISPLAY_NAMES | Display name for this activity |


### Response Body
```
{
	bf : "${BF}",
	ItineraryId : "${ITINERARY_ID}",
	tot : "${TOT}",
	end_time : "${END_TIME}",
	start_time : "${START_TIME}",
	tt : "${TT}",
	dur_m : "${DUR_M}",
	dur_d : "${DUR_D}",
	dur_h : "${DUR_H}",
	crc : "${CRC}",
	displayNames : "${DISPLAY_NAMES}"
}
 ```

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
| USER_DETAILS | Id of the created user details |
| TITLE | User Title Ex: Mr or Ms or Mrs |
| FIRST_NAME | User's first name |
| LAST_NAME | User's last name |
| USER_NAME | User's email. Booking confirmation will be sent to this email |
| MOBILE_NUMBER | User's mobile number. SMS Confirmation will be sent to this mobile number |
| BOOKING_REF | Any booking reference value from your end to map with our details |

#### Payload
```
{
  "user_details":{
  	 	"title" : "${TITLE}",
		"firstName": "${FIRST_NAME}",
		"lastName" : "${LAST_NAME}",
		"userName" : "${USER_NAME}",
		"mobileNumber" : "${MOBILE_NUMBER}",
		"bookingRef" : "${BOOKING_REF}"
  }
  
}
```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| trip | JSON object with all trip details |

### Response Body
```
{“success”:
 	{
	“trip_id”:“${TRIP_ID}”,
	“voucher_no”:“${VOUCHER_NO}”
	}
}
```

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Booking failed | Booking failed |

### 2.9 Retrieve Trip

#### Intent
`fetch_booking_details`

#### Request Params Description
| KEYWORD | DESCRIPTION |
| ---|--- |
| TRIP_ID | trip id from book itinerary api |

#### Payload
```
{
  	"tripid": "${TRIP_ID}"
}
```
### Response Params Description
| KEY | DESCRIPTION |
| ---|--- |
| TRIP | JSON object with all trip details |
| TRIP.ACTIVITY | Number of the activity |
| TRIP.BOOKING_STATUS | Status of Booking. Either P or F |
| TRIP.CREATED_AT | Booking created time |
| TRIP.CURRENCY | The currency in which the prices of activites are displayed |
| TRIP.END_DATE_TIME | Activity end date and time |
| TRIP.EXPRESS_CHECKOUT | Express Checkout if avaliable else null|
| TRIP.HAS_WALLET_PROMOTION | Wallet promotion if available else null |
| TRIP.HOTEL | Number of hotel for the activity |
| TRIP.ITINERARY_ID | Itinerary Id of the actvity |
| TRIP.START_DATE_TIME | Activity start date and time |
| TRIP.TRIP_KEY | Key of the trip |
| TRIP.TRIP_NAME | Name of the trip  |
| TRIP.TRIP_REF | Reference of the trip  |
| TRIP.TRIP_TYPE | Type of the trip  |
| TRIP.CONTACT_DETAILS | List of the contact details given in previous bookin itinerary  |
| TRIP.TRAVELLERSDETAILS | List of the Travellers  |
| TRIP.ACTIVITIES_BOOKINGS | List of the Activity Location which is already booked  |
| TRIP.ACTIVITIES_BOOKINGS.ACTIVITY_INFOS | List of activity booking status, voucher number, etc  |
| TRIP.ACTIVITIES_BOOKINGS.ACTIVITY_ORGANISER_DETAILS | List of details about organiser of the activity  |

### Response Body
```
{  "trip": {
                "activity": ${ACTIVITY},
                "amount": "${AMOUNT}",
                "booking_status": "${BOOKING_STATUS}",
                "created_at": "${CREATED_TIME}",
                "currency": "${CURRENCY}",
                "end_date_time": "${END_DATE_TIME}",
                "express_checkout": ${EXPRESS_CHECKOUT},
                "has_wallet_promotion": ${HAS_WALLET_PROMOTION},
                "hotel": ${HOTEL},
                "itinerary_id": "${ITINERARY_ID}",
                "start_date_time": "${START_DATE_TIME}",
                
                "trip_key": ${TRIP_KEY},
                "trip_name": "${TRIP_NAME}",
                "trip_ref": "${TRIP_REF}",
                "trip_type": ${TRIP_TYPE},
             
                "contact_detail": {
                    "address": "${ADDRESS}"",
                    "email": "${USER_NAME}",
                    "first_name": "${FIRST_NAME}",
                    "landline": ${LANDLINE},
                    "last_name": "${LAST_NAME}",
                    "mobile": "${MOBILE_NUMBER}",
                    "title": "${TITLE}"
                },
                "travellerDetails": {
                    "ADT": ${NO_OF_ADULTS},
                    "CHD": ${NO_OF_CHILDREN}
                },
                "gst_charged_by_supplier": true,
                "gst_charged_by_cleartrip": true,
                "is_reviewed": false,
                "activities_bookings": {
                    "address": "${ADDRESS}",
                    "children": ${NO_OF_CHILDREN},
                    "latitude": "${LATITUDE}",
                    "adults":${NO. OF ADULTS}, ,
                    "activity_booking_infos": [
                        {
                            "booking_status": "${BOOKING_STATUS}",
                            "pax_info_seq_no": ${PAX_INFO_SEQ_NO},
                            "seq_no": ${SEQ_NO},
                            "voucher_number": "${VOUCHER_NUMBER}",
                            "class_schedules": [

                            ]
                        }
                    ],
                    "activity_organiser_detail": {
                        "first_name": "${FIRST_NAME}",
                        "last_name": "${LAST_NAME}",
                        "image_url": "${IMAGE}",
                        "email": "${USER_NAME}",
                        "phone": "${MOBILE_NUMBER]"
                    }
                    "inclusions": "${INCLUSIONS}",
                    "longitude": "${LONGITUDE}"
                }
            }
}
```

### Error messages
Some error messages, you might get for an invalid search request. The HTTP response code in this case will be 400.

| Error message | Description |
| ---|--- |
| Booking failed | Booking failed |

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
