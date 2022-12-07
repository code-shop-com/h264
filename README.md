# H264 Streaming Module Introduction (version 2)

## News

The development of our adaptive streaming software is available at the
[(http://www.unified-streaming.com) Unified Streaming Platform] website. The
software that is available on this website (mod_h264_streaming version 2.2.7)
supports pseudo streaming for Flash. 

## News (March 2010)

Another sneak preview. We offer you a first look at
[http://smoothhd.code-shop.com Smooth Streaming for Adobe Flash 10.1]. Encode
your content once and playback on Silverlight, iPhone and Flash 10.1. More
information is available on our [http://smoothstreaming.code-shop.com Smooth
Streaming page].

## News (January 2009)

Welcome to version 2.0 of the H264 Streaming Module. Version 2.0 is a complete
rewrite. It works with a wider variety of MP4 video files and has faster
start/seek times. We have also added support for Apache and Ngingx, next to
Lighttpd.

## HTTP Pseudo Streaming

Adobe recently
[http://www.adobe.com/aboutadobe/pressroom/pressreleases/200712/120407adobemoviestar.html
announced] support for H264 video files in their Flash player. They have done a
great job and the good news is that we can have better quality video at lower
bitrates. At the same time it allows us to use free software to handle the
encoding.

## H264 Streaming Module

The H264 Streaming Module is a plugin for your existing !Apache/Lighttpd/Nginx
webserver. Its features are as follows:

### Timeshifting seek

Enable your viewers to immediately jump to any part of the video regardless of
the length of the video or whether it has all been downloaded yet.

### Virtual video clips

You have really long video clips and you don't want to re-encode them into
smaller parts? We also support 'virtual video clips', so you can specify to only
playback a part of the video or create download links to specific parts of the
video.

Virtual video clips also enables possibilities for
[http://demo.unified-streaming.com Adaptive Streaming].

An easy way for making previews available, say for example when you want to
differentiate between registered and unregistered users. Here's a little
tutorial for the different web servers on [wiki:VirtualVideoClipUrlRewrite 'url
rewriting and virtual video clips'].

### Network efficiency 

The next version will feature 'bandwidth shaping' allowing you to stream videos
and only use the bandwidth required to view the video over the network.

#### Encoding

If you are already using the widely adopted MPEG4/H264 industry standard, there
is no need to re-encode your MP4 videos, you can use your existing video files.

## Demonstration

You can watch the [http://h264.code-shop.com/demo/apache/testlist.html H264
(Pseudo) Streaming Demo]. Make sure you have the latest Flash player installed.
Grab it from [http://labs.adobe.com/technologies/flashplayer10/].

## Available Versions

Pick your webserver and continue to the download and build instructions.

  * [wiki:Mod-H264-Streaming-Apache-Version2 Apache]
  * [wiki:Mod-H264-Streaming-Lighttpd-Version2 Lighttpd]
  * [wiki:Mod-H264-Streaming-Nginx-Version2 Nginx]
  * [wiki:Mod-H264-Streaming-Internet-Information-Services-IIS-Version2 IIS 5
  * and 6] [wiki:Mod-H264-Streaming-Internet-Information-Services-IIS7-Version2
  * IIS 7] [wiki:Mod-H264-Streaming-AolServer-Version2 AOLserver]

Have a look at the [wiki:ReleaseNotes-Version2 latest release notes] to see what
has changed or have a look at the [wiki:Mod-H264-Streaming-Performance-Version2
performance figures] to give you an idea about cpu / memory usage.

## License

This version is free if you agree to the
[http://creativecommons.org/licenses/by-nc-sa/3.0/ noncommercial license].
Please mention its use on your website, in the lines of 'This website uses H264
pseudo video streaming technology by [http://h264.code-shop.com CodeShop]'.

Our commercial license is very inexpensive, see the following page to check if
you need a [wiki:Mod-H264-Streaming-License-Version2 commercial license].

## Flash players supporting H264 Streaming

  * [http://www.fastcatsoftware.com/Player/H264Streaming/demo.asp FCPlayer] by
  * Fastcat Software.  [http://www.longtailvideo.com/players/jw-flv-player/ JW
  * FLV Media Player].  [http://www.flowplayer.org/ Flowplayer]. The
  * H264Streaming Flowplayer plugin is available [FlowPlayer here].

## Encoding videos in H264

See the article [wiki:Encoding Encoding video in H264].

## Who is using the plugin?

See this [forum:7 forum] for references.

## Feedback

Feel free to email us a [mailto:h264@code-shop.com private comment] or leave a
note on our [/trac/discussion public forum].

## Thank you

A big thank you goes out to Tinic Uro and the people on the
http://www.jeroenwijering.com forum for providing the necessary reading,
articles and links.


