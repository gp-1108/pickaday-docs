# Partecipant

A Partecipant in order to exist must meet some requirements:

* A Partecipant must always be associated to an already existing event
* Given a specific name, at most one Partecipant per event is allowed to use that name
* A Partecipant name length must fall in this range: [3, 15]
* Once created, the partecipant's name cannot be changed
* A Partecipant must be available at least in onde day, if not it will be deleted from the event
* All of the available dates of the Partecipant must be valid dates (contained in the corresponding event)
* Given a specific device, this device can add/edit only one partecipant per event

<aside class="notice">
Once a Partecipant is created, it will be linked to the device'IP which created the Partecipant in the first place.
From now on, only this specific device will be allowed to modify this partecipant (edit or delete).
</aside>

## Adding a Partecipant

```javascript
const axios = require('axios');
const partecipant = await axios.post('https://pick-a-day.herokuapp.com/api/v1/partecipants', {
  available: ["02/02/2014","05/02/2014"],
  name: "John",
  eventId: "6215257d486c758bc7180462"
});
```

```javascript
const axios = require('axios');
const partecipant = await axios.post('https://pick-a-day.herokuapp.com/api/v1/partecipants', {
  available: "02/02/2014,05/02/2014",
  name: "John",
  eventId: "6215257d486c758bc7180462"
});
```

> The above commands returns an empty object in JSON:

```json
{}
```

This endpoint allows to create an Partecipant in a specific event.

### HTTP Request

`POST https://pick-a-day.herokuapp.com/api/v1/partecipants`

### Query Payload

Parameter  | Description | Constraints
---------  | ----------- | -----------
available | It must be either an array of Strings in format ```gg/mm/aaaa``` or a single String composed by ```gg/mm/aaaa``` entries separated by commas | At least one day and no more than 14, also it must be present in the corresponding event dates
name | A String containing the name of the partecipant | The length of the string cannot exceed 15 characters and be less than 3 characters. Given a specific event, no partecipants can share the same name
eventId | A String with the ID of the event | It must be a valid ID of an already existing event


## Editing a partecipant

```javascript
const axios = require('axios');
const partecipant = await axios.patch('https://pick-a-day.herokuapp.com/api/v1/partecipants', {
  available: ["05/02/2014"],
  name: "Peter",
  eventId: "6215257d486c758bc7180462"
});
```

```javascript
const axios = require('axios');
const partecipant = await axios.patch('https://pick-a-day.herokuapp.com/api/v1/partecipants', {
  available: "05/02/2014",
  name: "Peter",
  eventId: "6215257d486c758bc7180462"
});
```

> The above commands returns an empty object in JSON:

```json
{}
```

This endpoint allows to edit a partecipant available dates.
 
Please keep in mind that only a **matching IP address** allows for editing of a specified partecipant. If one tries to edit a partecipant from another device/IP it will not be allowed.

### HTTP Request

`PATCH https://pick-a-day.herokuapp.com/api/v1/partecipants`

### Query Payload

Parameter  | Description | Constraints
---------  | ----------- | -----------
available | It must be either an array of Strings in format ```gg/mm/aaaa``` or a single String composed by ```gg/mm/aaaa``` entries separated by commas | At least one day and no more than 14, also it must be present in the corresponding event dates
name | A String containing the name of the partecipant | It must be an already existing partecipant's name in the event
eventId | A String with the ID of the event | It must be a valid ID of an already existing event


<aside class="warning">
The combination of Event-Partecipant's name identifies the partecipants. It is therefore not allowed to modify the name of the partecipant after its creation.
The name in the payload serves for identifying purpose, not editing.
</aside>


## Delete a Partecipant

```javascript
const axios = require('axios');
const partecipant = await axios.delete('https://pick-a-day.herokuapp.com/api/v1/partecipants', {
  name: "John",
  eventId: "6215257d486c758bc7180462"
});
```

```javascript
const axios = require('axios');
const partecipant = await axios.delete('https://pick-a-day.herokuapp.com/api/v1/partecipants', {
  name: "John",
  eventId: "6215257d486c758bc7180462"
});
```

> The above commands returns an empty object in JSON:

```json
{}
```

This endpoint allows to delete a partecipant from a specific event.
 
Please keep in mind that only a **matching IP address** allows for deletion of a specified partecipant. If one tries to delete a partecipant from another device/IP it will not be allowed.

### HTTP Request

`DELETE https://pick-a-day.herokuapp.com/api/v1/partecipants`

### Query Payload

Parameter  | Description | Constraints
---------  | ----------- | -----------
name | A String containing the name of the partecipant | It must be an already existing partecipant's name in the event
eventId | A String with the ID of the event | It must be a valid ID of an already existing event