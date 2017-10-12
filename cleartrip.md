# ClearTrip Micro Services

1. Local Activities

    * Book Itenerary
  
2. Local Eatout
  
    * Booking Itenerary


## Local Activities

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
