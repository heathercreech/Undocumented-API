#Accessing Livestream Video
As far as I could tell, there is no API for directly retrieving a livestreams video. The process actually involves quite a few GET requests. 


| Call | Description |
|------|-------------|
| `/api/channels/:channel/access_token` | Gets the signature and token string for a specific channel |
| `usher.twitch.tv/api/channel/hls/:channel.m3u8` | Retrieves a manifest file containing links to video streams of a certain quality |


##Access Tokens
An access token is used to access a specific streams quality manifest. The token consists of three values: a signature, a boolean to determine if mobile is restricted, and a value named token that contains json detailing ids, expiration dates, and various restrictions.

| Variable | Description |
|----------|-------------|
| mobile_restricted | Determines if mobile users can view the stream |
| sig | Some kind of signature, required for requesting the quality manifest |
| token | Details the channel, the expiration date, and several restrictions|

##Quality Manifest
A quality manifest is a `.m3u8` file that contains links to many more manifest files, each of which contain data corresponding to a certain video quality setting (i.e. "low", "medium", and "high"). 

###`usher.twitch.tv/api/channel/hls/:channel.m3u8`


###Processing m3u8 Files


##Video Manifest