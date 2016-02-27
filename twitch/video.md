#Accessing Livestream Video
As far as I could tell, there is no API for directly retrieving a livestreams video. The process actually involves quite a few GET requests. 


| Call | Description |
|------|-------------|
| /api/channels/:channel/access_token | Gets the signature and token string for a specific channel |
| usher.twitch.tv/api/channel/hls/:channel.m3u8| Retrieves a manifest file containing links to video streams of a certain quality |


##Access Tokens


##Quality Manifest


###Processing m3u8 Files


##Video Manifest