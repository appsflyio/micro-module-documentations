# ClearTrip Micro Services

1. [Local Activities](#local-activities)

    * [Book Itenerary](#11-book-itenerary)
  
2. [Local Eatout](#local-activities)
  
    * [Book Itenerary](#11-book-itenerary-1)

--------------------------------------------------------------------------------

## Local Activities 
microapp_handle : `com.cleartrip.microservices.local.activities`
### 1.1 City List

#### Intent
`city_list`

City list api will list all the available cities and there product type availability in that city. The search request is a simple HTTP GET request. The sample request described below should be sent along with the URL, and the user’s API key in the HTTP headers. A successful response will always return the HTTP status code 200. (Note that a status code of 200 doesn’t necessarily mean that the search result will be returned; but a successful search will always return a status code of 200).

### Response Body Example
```
"gadag": {
        "ttd": true,
        "count": 6,
        "fnb": true
    },
 ```
### Response Body 
| KEY | DESCRIPTION |
| ---|--- |
| ttd | Contains True/False based on availability in the corresponding city |
| fnb | Contains True/False based on availability in the corresponding city |

If the search was successful, the response body returns an JSON along with the HTTP status code 200. If any error is encountered during the search, the response body contains an JSON with the root element error_code. See the schema and sample search result JSON for more details.

### 1.1 Book Itenerary

#### Intent
`book_itinerary`

#### Request Params Description
| KEYWORD | DESCRIPTION |
| ---|--- |
| ITENERARY_ID | Id of the created itenerary |
| TITLE | User Title Ex: Mr or Ms or Mrs |
| FIRST_NAME | User's first name |
| LAST_NAME | User's last name |
| EMAIL | User's email. Booking confirmation will be sent to this email |
| MOBILE_NO | User's mobile number. SMS Confirmation will be sent to this mobile number |

#### Payload
```
{
  "itineraryid":"${ITENERARY_ID}",
  "user_details":{
    "title" : "${TITLE}",
    "firstName": "${FIRST_NAME}",
    "lastName" : "${LAST_NAME}",
    "email" : "${EMAIL}",
    "mobileNumber" : "${MOBILE_NO}"
  }
}
```

### 1.1 Book Itenerary

#### Intent
`book_itinerary`

#### Request Params Description
| KEYWORD | DESCRIPTION |
| ---|--- |
| ITENERARY_ID | Id of the created itenerary |
| TITLE | User Title Ex: Mr or Ms or Mrs |
| FIRST_NAME | User's first name |
| LAST_NAME | User's last name |
| EMAIL | User's email. Booking confirmation will be sent to this email |
| MOBILE_NO | User's mobile number. SMS Confirmation will be sent to this mobile number |

#### Payload
```
{
  "itineraryid":"${ITENERARY_ID}",
  "user_details":{
    "title" : "${TITLE}",
    "firstName": "${FIRST_NAME}",
    "lastName" : "${LAST_NAME}",
    "email" : "${EMAIL}",
    "mobileNumber" : "${MOBILE_NO}"
  }
}
```

--------------------------------------------------------------------------------

## Local eatout 
microapp_handle : `com.cleartrip.microservices.local.eatouts`

### 1.1 Book Itenerary

#### Intent
`book_itinerary`

#### Params Description
| KEYWORD | DESCRIPTION |
| ---|--- |
| ITENERARY_ID | Id of the created itenerary |
| TITLE | User Title Ex: Mr or Ms or Mrs |
| FIRST_NAME | User's first name |
| LAST_NAME | User's last name |
| EMAIL | User's email. Booking confirmation will be sent to this email |
| MOBILE_NO | User's mobile number. SMS Confirmation will be sent to this mobile number |

#### Payload
```
{
  "itineraryid":"${ITENERARY_ID}",
  "user_details":{
    "title" : "${TITLE}",
    "firstName": "${FIRST_NAME}",
    "lastName" : "${LAST_NAME}",
    "email" : "${EMAIL}",
    "mobileNumber" : "${MOBILE_NO}"
  }
}
```
