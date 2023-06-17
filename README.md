#

                   Nudge API Documentation

1- Overview

Nudge API is a JSON-based API. All requests are made to endpoints beginning: https://api/v1/app

All requests must be secure, i.e. https, not http.

2- Resources

The API is RESTful and arranged around resources. All requests must be made using https.
Typically, the first request you make should be to post a nudge for an event.

2.1 Post Nudge

Create a Nudge for an Event.

API Endpoint: /nudge

A request to create a nudge for an event looks like this:
POST https://api/v1/app/nudge

Payload:
title, event,date,time,description,image,icon,invitation

Object Data Model of A Nudge

Field
Type
Description
title
String
Title of the Nudge
event
String
Event for which the Nudge is created
date
Date
Date of Nudge
time
String
Time at which Nudge is to be sent
description
String
Description of the Nudge
image
file
Cover photo of the nudge
icon
file
Icon for display when nudge is minimized
invitation
String
One-line invitation

Example Request:

POST api/v1/app/nudges
Host: api.medium.com
Content-Type: application/json
Accept: application/json
Accept-Charset: utf-8

body
{
"title": "Team Meeting",
"event": "Integration of FrontEnd with BackEnd",
"date": "2023-06-30",
“Time”: “23:58:00 IST”
“description”:”A Team Meeting to discuss how the integration is to be carried out, its intricacies and details.”,
"imageUrl":“https://cdn-images-1.aloha.com/fit/0*ae1jbP_od0W6E.jpeg",
“iconUrl”:“https://cdn-images-1.aloha.com/fit/0*ae1jbP_od0W6E.jpeg”,
“invitation”:” Don’t miss out on this wonderful opportunity”
}

Possible Errors

Error Code
Description
400 Bad Request
Informed Parameters in the Request

500 Internal Server Error
An unexpected error occurred on the server.

2.2 Fetch Nudges

2.2.1 Fetch All Nudges

Returns a full list of nudges in the database. This includes all nudges created for all types of events.

API Endpoint: /nudge

A request to fetch a list of all nudges created for all events looks like this:
GET https://api/v1/app/nudge

The response is a list of Nudges objects. An empty array is returned if no nudges have been registered. The response array is wrapped in a data envelope.

Example response:

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
"data": [
{
"id": "b969ac62a46b",
"title": "Team Meeting",
"event": "Integration of FrontEnd with BackEnd",
"date": "2023-06-30",
“Time”:”13:00:00 IST”,
“description”:”A Team Meeting to discuss how the integration is to be carried out, its intricacies and details.”,
"imageUrl":“https://cdn-images-1.aloha.com/fit/0*ae1jbP_od0W6E.jpeg",
“iconUrl”:“https://cdn-images-1.aloha.com/fit/0*ae1jbP_od0W6E.jpeg”,
“invitation”:”Don’t miss out on this wonderful opportunity”
},
]
}

Possible Errors

Error Code
Description
404 Not Found
Resource doesn’t exist or incorrect URL or endpoint

2.2.2 Fetch Nudges for an Event

Returns the list of nudges created for a particular event.

API Endpoint: /nudge?event=eventName

A request to fetch a list of all nudges created for a particular event looks like this:

GET https://api/v1/app/nudge?event=eventName

The response is a list of Nudges created for an event by the name {eventName}. An empty array is returned if no nudges have been registered for that particular event. The response array is wrapped in a data envelope.

Example Response:

Same as Fetch All Nudges (2.2.1)

Possible Errors

Error Code
Description
404 Not Found
Resource doesn’t exist or incorrect URL or endpoint

2.2.3 Fetch a Particular Nudge

Returns the nudge requested by id.

API Endpoint: /nudge/:id

A request to fetch a single nudge created for a particular event looks like this:
GET https://api/v1/app/nudge/:id

The response is a single JSON object with id equal to id in request parameter. An error is returned if no nudge is registered by that id.

Example response:

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

    {
     "id": "b969ac62a46b",
      "title": "Team Meeting",
      "event": "Integration of FrontEnd with BackEnd",
      "date": "2023-06-30",
      “Time”:”13:00:00 IST”,
      “description”:”A Team Meeting to discuss how the integration is to be carried out, its intricacies and details.”,
       "imageUrl":“https://cdn-images-1.aloha.com/fit/0*ae1jbP_od0W6E.jpeg",
      “iconUrl”:“https://cdn-images-1.aloha.com/fit/0*ae1jbP_od0W6E.jpeg”,

“invitation”:”Don’t miss out on this wonderful opportunity”
},

    }

Possible Errors

Error Code
Description
404 Not Found
Resource doesn’t exist or incorrect URL or endpoint

2.3 Update Nudge Details

Updates the details of a particular nudge referenced by its id.

API Endpoint: /nudge/:id

A request to update a single nudge created for a particular event looks like this:
PUT https://api/v1/app/nudge/:id

Payload
Same as payload of Add Nudge (2.1)

Object Data Model
Same as object data model of Add Nudge (2.1)

Example Request
Same as request of Add Nudge (2.1)

2.4 Delete Nudge

Deletes a particular nudge referenced by its id.

API Endpoint: /nudge/:id

A request to delete a single nudge for an event looks like this:
DELETE https://api/v1/app/nudge/:id

The response is a single JSON object with a message key. An error is returned if no nudge is registered by that id.

Example Response:

{
“message”: “ Nudge with id: 64eb45673a has been deleted”
}

Possible Errors

Error Code
Description
400 Bad Request
Incorrect Parameter
