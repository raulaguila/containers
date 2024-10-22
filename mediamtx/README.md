<h1 style="text-align:center">Media MTX</h1>

_[MediaMTX](https://github.com/bluenviron/mediamtx)_ is a ready-to-use and zero-dependency real-time media server and
media proxy that allows to publish, read, proxy, record and playback video and audio streams. It has been conceived as
a "media router" that routes media streams from one end to the other.

# Starting

Starting the container:

```shell
docker compose up -d --build
```

# Testing

### Encoding

Using FFmpeg to encode and send data to the server. Following is the FFmpeg command to encode and transfer the video to
the server.

| parameter                    | description                                                                                                                                                                                 |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -stream_loop -1              | It i to stream the video on loop                                                                                                                                                            | 
| -re                          | It is an input parameter that instructs FFmpeg to read the same number of frames per second as the framerate of the input video. It is most used for live streaming or with a camera input. |
| -i test.mp4                  | It is the input video that we are using for the discussion                                                                                                                                  |
| -c:v libx264                 | Here we are specifying the encoder to be used for the video as H.264/AVC                                                                                                                    |
| -c:a aac                     | This is the target RTMP destination for the video. The URL is based on the configuration of the streaming server.                                                                           |
| -f flv                       | This is the target RTMP destination for the video. The URL is based on the configuration of the streaming server.                                                                           |
| rtmp://localhost/live/stream | This is the target RTMP destination for the video. The url is based on the configuration of the streaming server.                                                                           |

Running the above command on the terminal after the streaming server is configured, would look like this:

```shell
ffmpeg -stream_loop -1 -re -i test.mp4 -c:v libx264 -c:a aac -f flv rtmp://localhost/live/stream
```

FFmpeg auto generate a video to stream:

```shell
ffmpeg -r 100 -f lavfi -i testsrc -vf scale=1920:1080 -vcodec libx264 -profile:v baseline -pix_fmt yuv420p -f flv rtmp://localhost/live/stream
```

### Consuming

MediaMTX is configured to automatically convert incoming streams to HLS protocol for web access.

To view the stream, access it in your browser:

```text
http://localhost:8888/live/stream/
```

Or you can consume it using any other software that consumes the RTMP protocol, such as VLC, OBS...
