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
To retrieve a quality manifest, the above call must be made with a few query parameters (the access token data from earlier).

| Parameter | Description |
|-----------|-------------|
| sig | (Required) The signature from the access token |
| token | (Required) The token variable from the access token |
| p | 6-digit random integer, no idea what this is used for |
| allow_spectre | No idea what this is |
| player | No idea. Valid values: `twitchweb`(possibly more) |
| allow_source | Determines if the manifest file will contain a link to "source" quality |
| allow_audio_only | Determines if the manifest file will contain a link to "audio_only" quality |


###Processing Manifest Files

Below is an example of a quality manifest file.
```
#EXTM3U
#EXT-X-TWITCH-INFO:NODE="video-edge-80f084.ord02",MANIFEST-NODE="video-edge-80f084.ord02",SERVER-TIME="1456790945.85",USER-IP="147.133.207.237",CLUSTER="ord02",MANIFEST-CLUSTER="ord02"
#EXT-X-MEDIA:TYPE=VIDEO,GROUP-ID="high",NAME="High",AUTOSELECT=YES,DEFAULT=YES
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=1760000,RESOLUTION=1280x720,CODECS="avc1.66.31,mp4a.40.2",VIDEO="high"
http://video-edge-80f084.ord02.hls.ttvnw.net/hls-8c7be4/lobosjr_19903039840_409766749/high/py-index-live.m3u8?token=id=2607615118474079899,bid=19903039840,exp=1456877345,node=video-edge-80f084-1.ord02.hls.justin.tv,nname=video-edge-80f084.ord02,fmt=high&sig=301187cdc1f0597bfe5e66ea3a00c3d157f31823
#EXT-X-MEDIA:TYPE=VIDEO,GROUP-ID="medium",NAME="Medium",AUTOSELECT=YES,DEFAULT=YES
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=928000,RESOLUTION=852x480,CODECS="avc1.66.31,mp4a.40.2",VIDEO="medium"
http://video-edge-80f084.ord02.hls.ttvnw.net/hls-8c7be4/lobosjr_19903039840_409766749/medium/py-index-live.m3u8?token=id=2607615118474079899,bid=19903039840,exp=1456877345,node=video-edge-80f084-1.ord02.hls.justin.tv,nname=video-edge-80f084.ord02,fmt=medium&sig=e932def1ce0b85ac27d441741290485782747d84
#EXT-X-MEDIA:TYPE=VIDEO,GROUP-ID="low",NAME="Low",AUTOSELECT=YES,DEFAULT=YES
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=596000,RESOLUTION=640x360,CODECS="avc1.66.31,mp4a.40.2",VIDEO="low"
http://video-edge-80f084.ord02.hls.ttvnw.net/hls-8c7be4/lobosjr_19903039840_409766749/low/py-index-live.m3u8?token=id=2607615118474079899,bid=19903039840,exp=1456877345,node=video-edge-80f084-1.ord02.hls.justin.tv,nname=video-edge-80f084.ord02,fmt=low&sig=fab722b0945b934859b8c6cb4f07b5b6efddeaab
#EXT-X-MEDIA:TYPE=VIDEO,GROUP-ID="mobile",NAME="Mobile",AUTOSELECT=YES,DEFAULT=YES
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=164000,RESOLUTION=400x226,CODECS="avc1.66.31,mp4a.40.2",VIDEO="mobile"
http://video-edge-80f084.ord02.hls.ttvnw.net/hls-8c7be4/lobosjr_19903039840_409766749/mobile/py-index-live.m3u8?token=id=2607615118474079899,bid=19903039840,exp=1456877345,node=video-edge-80f084-1.ord02.hls.justin.tv,nname=video-edge-80f084.ord02,fmt=mobile&sig=ed44bb0c152320e58aff1d4c88b9cb0ebd508305
#EXT-X-MEDIA:TYPE=VIDEO,GROUP-ID="audio_only",NAME="Audio Only",AUTOSELECT=NO,DEFAULT=NO
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=128000,CODECS="mp4a.40.2",VIDEO="audio_only"
http://video-edge-80f084.ord02.hls.ttvnw.net/hls-8c7be4/lobosjr_19903039840_409766749/audio_only/py-index-live.m3u8?token=id=2607615118474079899,bid=19903039840,exp=1456877345,node=video-edge-80f084-1.ord02.hls.justin.tv,nname=video-edge-80f084.ord02,fmt=audio_only&sig=6a50478bb993e32b5aa35b3f55cc13c7ae339ad1
```

##Video Manifest