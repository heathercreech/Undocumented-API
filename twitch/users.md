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
A `users/:user/follows/channels` request returns the number of channels a user follows, their links, and a great deal of information about the channels themselves.


#### Games

### Parameters
*Note: any description following by '(?)' means that the parameters function is being guessed and has not been confirmed*

| Option | Default Value | Description |
|--------|---------------|-------------|
| direction | DESC | Determines which order that channels appear based on sortby's value |
| limit | 25 | Limits the number of results returned |
| offset | 0 | Object offset for pagination. |
| sortby | login | Key that the data is sorted by. Valid values are `created_at`, `last_broadcast`, and `login` (unsure if there are more than this) |