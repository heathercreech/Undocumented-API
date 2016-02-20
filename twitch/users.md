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

