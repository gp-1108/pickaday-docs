# Event

An Event must follows some rules in order to exists:

* No event is allowed to contains more than 14 distinct dates
* It must contain at least one day
* Its name length must be inside the range [3, 25] characters.

## Creating an Event

```javascript
const axios = require('axios');
const newEvent = await axios.post('https://pick-a-day.herokuapp.com/api/v1/event', {
  days: ["01/02/2014","02/02/2014","05/02/2014"],
  name: "My Event Name"
});
```

> The above command returns JSON structured like this in both scenarios:

```json
{
  "_id": "6215257d486c758bc7180462",
  "name": "My Event Name",
  "days": ["1/2/2014","2/2/2014","5/2/2014"]
}
```

This endpoint allows to create an Event starting from its name and the data with it associated.

### HTTP Request

`POST https://pick-a-day.herokuapp.com/api/v1/event`

### Query Payload

Parameter  | Description | Constraints
---------  | ----------- | -----------
days | It must be either an array of Strings in format ```gg/mm/aaaa``` or a single String composed by ```gg/mm/aaaa``` entries separated by commas | At least one day and no more than 14
name | A String containing the name of the event | The length of the string cannot exceed 25 characters and be less than 3 characters


### Response Payload
Parameter  | Description 
---------  | -----------
_id | A String of the event's ID
days | An arry of Strings in format ```gg/mm/aaaa``` containing all the dates of this event
name | A String containing the name of the event 

<aside class="notice">
The <code>_id</code> returned by the endpoint is very important, it will allow to search for a specific event.
</aside>

## Get a specific event

```javascript
const axios = require('axios');

const event = await axios.get('https://pick-a-day.herokuapp.com/api/v1/event/6215257d486c758bc7180462');
```

> The above command returns JSON structured like this:

```json
{
  "name": "My Event Name",
  "days": ["1/2/2014","2/2/2014","5/2/2014"],
  "partecipants": {
    "john": ["2/2/2014","5/2/2014"],
    "patrick": ["2/2/2014"],
    "peter": ["1/2/2014","5/2/2014"]
  }
}
```

This endpoint retrieves a specific event whose ID matches the one provided.

### HTTP Request

`GET https://pick-a-day.herokuapp.com/api/v1/event/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the event to retrieve


### Response Payload

Parameter  | Description 
---------  | -----------
days | An arry of Strings in format ```gg/mm/aaaa``` containing all the dates of this event
name | A String containing the name of the event 
partecipant | a map containing all of the entries ```partecipant-availability```

## Delete an Event

There is no need to delete an Event. Once the most recent available date will be passed by more than 10 days it will be automatically deleted.

<aside class="warning">
  When an Event is deleted, all of the associated partecipants are deleted too
</aside>