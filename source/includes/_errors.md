# Errors

The pickday API uses most of the standard error codes. 
If any of your requests leads to an error it will be reported as such with its HTTP status code.

When a response singals an error, it will always come with a JSON response like: ```{ msg: "Meaningful explanation of what has gone wrong }```

Please, always look for the ```.msg``` property in the response, as it will be a meaningful explanation of what has gone wrong in your request.

```javascript
const axios = require('axios');
const newEvent = await axios.post('https://pick-a-day.herokuapp.com/api/v1/event', {
  days: ["01/02/2014","02/02/2014","05/02/2014"],
  name: "sa" // The even name is too short!
});
```

> The response would be 400 Bad requests and the following JSON payload:

```json
{
  "msg": "Path `name` (`sa`) is shorter than the minimum allowed length (3)."
}
```


```javascript
const axios = require('axios');
const partecipant = await axios.delete('https://pick-a-day.herokuapp.com/api/v1/partecipants', {
  name: "Charlie",
  eventId: "6215257d486c758bc7180462"
});
```

> Assuming the device from which the deletion was attempted and the one which created the partecipant where different
> The response would be 409 Conflict with the following JSON payload:

```json
{
  "msg": "Cannot delete partecipant dates from different IP"
}
```

### Response Payload

Parameter  | Description 
---------  | -----------
msg | A String containing an explanation of why the request failed