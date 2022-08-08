# Setting up an ip camera stream

RTSP (Real Time Streaming Protocole) uses port 554.

Each vendor have their own url to access the camera feed.

Using VLC, you can use " Media > Open Network Stream... "

For my setup this URL works:

```
rtsp://<IP_ADDR_OF_CAMERA>/user=<USERNAME>_password=<PASSWORD>_channel=0_stream=0.sdp?real_stream
```

Once you have the stream, you can live view it, or setup a ZoneMinder server.

https://www.howtoforge.com/video_surveillance_zoneminder_ubuntu

https://zoneminder.readthedocs.io/en/stable/installationguide/ubuntu.html

https://zoneminder.readthedocs.io/en/stable/installationguide/index.html

This solution works great, but lots to tweak to avoid false positive events
