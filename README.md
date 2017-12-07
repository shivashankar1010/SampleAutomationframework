# SampleAutomationframework
hmrc hybrid framework
restful-booker

A simple Node booking form for testing RESTful web services.
Requirements

    Docker 17.09.0
    Docker Compose 1.16.1

Installation

    Ensure mongo is up and running by executing mongod in your terminal
    Clone the repo
    Navigate into the restful-booker root folder
    Run npm install
    Run npm start

Or you can run this via Docker:

    Clone the repo
    Navigate into the restful-booker root folder
    Run docker-compose build
    Run docker-compose up
    APIs are exposed on http://localhost:3001

API

    GET /ping
    GET /booking
    GET /booking/{id}
    POST /booking
    POST /auth
    PUT /booking/{id}
    DELETE /booking/{id}

GET /ping
Usage

GET /ping
Response

200 OK - If application is up
GET /booking

GET /booking
GET /booking?firstname=sally&lastname=brown
GET /booking?checkin=2014-03-13&checkout=2014-05-21

Parameters

    firstname - String - The firstname of the user
    lastname - String - The lastname of the user
    checkin - Date(CCYY-MM-DD) - The day in which person(s) checks in
    checkout - Date(CCYY-MM-DD) - The day in which person(s) checks out

Response

[
  {
    "bookingid": 1
  },
  {
    "bookingid": 2
  },
  {
    "bookingid": 3
  },
  {
    "bookingid": 4
  }
]

GET /booking/{id}

GET /booking/1

Parameters

    id - String - The unique identifier of the booking

Response
Accept: application/json

{
    "firstname": "Sally",
    "lastname": "Brown",
    "totalprice": 111,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2013-02-23",
        "checkout": "2014-10-23"
    },
    "additionalneeds": "Breakfast"
}

Accept: application/xml

<booking>
    <firstname>Sally</firstname>
    <lastname>Brown</lastname>
    <totalprice>111</totalprice>
    <depositpaid>true</depositpaid>
    <bookingdates>
        <checkin>2013-02-23</checkin>
        <checkout>2014-10-23</checkout>
    </bookingdates>
    <additionalneeds>Breakfast</additionalneeds>
</booking>

POST /booking

POST /booking

Payload
Content-Type: text/xml

<booking>
    <firstname>Sally</firstname>
    <lastname>Brown</lastname>
    <totalprice>111</totalprice>
    <depositpaid>true</depositpaid>
    <additionalneeds>Breakfast</additionalneeds>
    <bookingdates>
        <checkin>2013/02/23</checkin>
        <checkout>2014/10/23</checkout>
    </bookingdates>
</booking>

Content-Type: application/json

{
  "firstname" : "Sally",
	"lastname" : "Brown",
	"totalprice" : 111,
	"depositpaid" : true,
	"additionalneeds" : "Breakfast",
	"bookingdates" : {
		"checkin" : "2013-02-23",
		"checkout" : "2014-10-23"
	}
}

Response
Accept: application/json

{
    "booking": {
        "firstname": "Sally",
        "lastname": "Brown",
        "totalprice": 111,
        "depositpaid": true,
        "additionalneeds": "Breakfast",
        "bookingdates": {
            "checkin": "2013-02-23",
            "checkout": "2014-10-23"
        }
    }
}

Accept: application/xml

<?xml version="1.0" encoding="UTF-8"?>
<created-booking>
    <booking>
        <firstname>Sally</firstname>
        <lastname>Brown</lastname>
        <totalprice>111</totalprice>
        <depositpaid>true</depositpaid>
        <additionalneeds>Breakfast</additionalneeds>
        <bookingdates>
            <checkin>2013-02-23</checkin>
            <checkout>2014-10-23</checkout>
        </bookingdates>
    </booking>
</created-booking>

POST /auth

POST /auth

Payload

{
    "username": "admin",
    "password": "password123"
}

Response

VHgTAuGPxvMsH1p

PUT /booking/{id}

PUT /booking/1

Authorisation requirements

    Cookie: token={token received from /auth}

Parameters

    id - String - The unique identifier of the booking

Payload
Content-Type: text/xml

<booking>
    <firstname>Sally</firstname>
    <lastname>Brown</lastname>
    <totalprice>111</totalprice>
    <depositpaid>true</depositpaid>
    <additionalneeds>Breakfast</additionalneeds>
    <bookingdates>
        <checkin>2013/02/23</checkin>
        <checkout>2014/10/23</checkout>
    </bookingdates>
</booking>

Content-Type: application/json

{
  "firstname" : "Sally",
	"lastname" : "Brown",
	"totalprice" : 111,
	"depositpaid" : true,
	"additionalneeds" : "Breakfast",
	"bookingdates" : {
		"checkin" : "2013-02-23",
		"checkout" : "2014-10-23"
	}
}

Response
Accept: application/json

{
    "id": "1",
    "firstname": "Sally",
    "lastname": "Brown",
    "totalprice": 111,
    "depositpaid": true,
    "additionalneeds": "Breakfast",
    "bookingdates": {
        "checkin": "2013-02-23",
        "checkout": "2014-10-23"
    }
}

Accept: application/xml

<?xml version="1.0" encoding="UTF-8"?>
<booking>
    <id>1</id>
    <firstname>Sally</firstname>
    <lastname>Brown</lastname>
    <totalprice>111</totalprice>
    <depositpaid>true</depositpaid>
    <additionalneeds>Breakfast</additionalneeds>
    <bookingdates>
        <checkin>2013-02-23</checkin>
        <checkout>2014-10-23</checkout>
    </bookingdates>
</booking>

DELETE /booking/{id}

DELETE /booking/1

Authorisation requirements

    Cookie: token={token received from /auth}

Parameters

    id - String - The unique identifier of the booking

Response

204 - On successful delete
