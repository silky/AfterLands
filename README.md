AfterLands

## API

#### Get all rooms near the passed location

`GET /getallnear/:lat,:lon`

Result: List of rooms.

    {
        "response": "ok",
        "rooms": [
            {
                "name": "Hello world",
                "active": true,
                "mood": "",
                "_id": "53d455a8c027df9e7e1ea25c",
                "songs": [],
                "__v": 0,
                "location": {
                    "lat": 37.79713,
                    "lon": -122.40464
                },
                "created_at": "2014-07-27T01:28:08.828Z",
                "distance": 92.28804970634626
            }
        ]
    }

#### Make a new room

`POST /make`

Required params:

`room_name`: name of the room
`lat`, `lon`: location of the room

#### Add a song to a room

`POST /addsong`

Required params:

`song`: Rdio song object
`room_id`: Object ID of the room as in Mongo

#### Search for songs

`GET /search?query=XXXXXXX`

Returns a list of Rdio songs

#### Get details of a room

`GET /room/:room_id`

Returns the whole room object

## Sockets Messages

### Client to Server

#### Join user to a room: `joinRoom`

Pass `room_id`.

Emits `userChanged` with the new `room.num_people` to all users in this room

#### Add a vote for a song in a room

Emit `vote` with:

- `song_key`: Each Rdio song has a `key`.
- `room_id` and `vote` (+1 or -1)

Does not return anything. Emits a `voteChange` message to all client in this room. Also sends the `song_key` and `vote`.
