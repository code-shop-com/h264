# Testing the H264 Streaming Module (version 2)

## Dependencies 

For testing purposes we recommend a tool like WGET, or Curl.

## Download a complete movie 

Upload an MP4 video to the document root of your website and download the full
file. make sure you change the URL to your own domain.

```
wget -O test.mp4 "http://h264-demo.example.com/trailer.mp4"
```

## Specify a start time 

Specify a start time:

```
wget -O test.mp4 "http://h264-demo.code-shop.com/trailer.mp4?start=45.5"
```

This saves a file (test.mp4) on your local disk that will have the first 45.5
seconds removed from the original (trailer2.mp4) video. You can use your
favorite player to see if worked okay.

## Query parameters

| parameter name | value | notes | 
| --- | --- | --- | --- |
| start | start time of video clip (in seconds)| defaults to start of clip |
| end | end time of video clip (in seconds) | defaults to end of clip|
| client | FLASH|| when the client is specified as FLASH meta data will not be 
compressed and only 1 video and audio stream is returned |

Note that the start and end times are always aligned to the nearest keyframe.
The more keyframes you have in your video the more accurate it will be. In
FFMPEG you can set the number of keyframes with the 'Set group of pictures size'
(-g gop_size) option.

## Virtual video clips 

As you can see it is easy to create 'virtual video clips'. Let's say that you
have a *very* long video that you do not want to re-encode into smaller parts,
you can easily specify them using the start and end times.

So there is only one full clip stored, but parts of it can be made available,
like so:

| The full clip | http://h264-demo.example.com/demo/trailer.mp4?start=0] |
| The first minute | http://h264-demo.example.com/trailer.mp4?start=0&end=60 |
| The last two minutes | http://h264-demo.example.com/trailer.mp4?start=404 |

