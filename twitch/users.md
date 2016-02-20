# Users
| Endpoints | Description |
|-----------|-------------|
|[GET /users/:user/follows/:type](users.md#get-usersuserfollowstype)	|Gets a list of :type that the user follows|


## `GET /users/:user/follows/:type`


### Possible :type Values
| Value | Description |
|-------|-------------|
| channels | Returns the list of channels that the user is following |
| games | Returns the list of games that the user is following |


#### Channels
A `users/:user/follows/channels` request returns the number of channels a user follows, their links, and a great deal of information about the channels themselves. This request is in the official API, however there are some differences.

- Default value for the sortby parameter is different (defaults to `login` instead of `created_at`)
- Sorting by `created_at` doesn't work
- There is a `live` status that shows if a channel is currently broadcasting
- A `stream` object that is assigned to if the channel is live


##### `stream` Object
The `stream` object contains information about a live broadcast.

#### Games
A `users/:user/follows/games` request returns the number of games a user follows, their names, and different images used on the site.

### Parameters

| Option | Default Value | Description |
|--------|---------------|-------------|
| direction | DESC | Determines which order that channels appear based on sortby's value |
| limit | 25 | Limits the number of results returned |
| offset | 0 | Object offset for pagination. |
| sortby | login | Key that the data is sorted by. Valid values are `last_broadcast`, and `login` (unsure if there are more than this) |