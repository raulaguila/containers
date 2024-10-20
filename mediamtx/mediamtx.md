<h1 style="text-align:center">Media MTX</h1>

[MediaMTX](https://github.com/bluenviron/mediamtx) docker compose example.

Command to send a video to stream server using ffmpeg

| parameter                    | description                                                                                                                                                                                 |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -re                          | It is an input parameter that instructs FFmpeg to read the same number of frames per second as the framerate of the input video. It is most used for live streaming or with a camera input. |
| -i test.mp4                  | It is the input video that we are using for the discussion                                                                                                                                  |
| -c:v libx264                 | Here we are specifying the encoder to be used for the video as H.264/AVC                                                                                                                    |
| -c:a aac                     | This is the target RTMP destination for the video. The URL is based on the configuration of the streaming server.                                                                           |
| -f flv                       | This is the target RTMP destination for the video. The URL is based on the configuration of the streaming server.                                                                           |
| rtmp://localhost/live/stream | This is the target RTMP destination for the video. The url is based on the configuration of the streaming server.                                                                           |

Running the above command on the terminal after the streaming server is configured, would look like this:

```shell
ffmpeg -re -i test.mp4 -c:v libx264 -c:a aac -f flv rtmp://localhost/live/stream
```

MediaMTX automatically converts incoming streams to hls for web access. To view the stream, access it in your browser:

```text
http://localhost:8888/live/stream/
```