# Release notes (version 2)

[back](http://h264.code-shop.com/trac/wiki/)[[PageOutline]]

----

## Newer versions (version 2.3.x and onwards)

The latest release notes can be found on our [Unified-Streaming](http://www.unified-streaming.com/index.php/support/release-notes/) page.


## 2010-01 (development version)

  -

## 2010-01 (Version 2.2.7)

  - lowered apache requirement to version 2.0.55.
  - added read_ahead configuration for Nginx version >= 0.8.18 (read_ahead).
  - ignore esds atoms in hint tracks. this makes videos with hint tracks playable again.
  - fixed 405 Not Allowed errors for Nginx/Debian (include order, make sure nginx headers are included first before including stdint.h).
  - fixed CPU hogging.
  - added query parameter 'input=flv' to specify the file type when the '.flv' extension is missing from the filename.

## 2009-12 (Version 2.2.6)

  - esds atom for video is allowed.
  - Fixed stsz atom with default sample size.
  - esds atom for mp3 may have no decoder specific info descriptor.
  - Fixed planetdv report (end parameter near end of file was always sending moov_size too much data).
  - Fixed memory overrun in writing moov_data (for very specific movie files).

## 2009-10 (Version 2.2.4)

  - IIS7: Fixed App Pool crash for Unsupported Media Type files.

## 2009-08 (Version 2.2.1)

  - Fixed order of unknown atoms.

## 2009-07 (version 2.2.0)

## 2009-05 (development version, not available yet)

  - Added 'vbegin' and 'vend' parameters to specify beginning and ending of Virtual Video clips. They are similar to the 'start' and 'end' parameters, but avoid the name clash. Note that the 'start' and 'end' parameters are relative to 'vbegin' and 'vend'.
  - IIS: Added Connection: Keep-Alive

## 2009-04 (development version, not available yet)

  - Fixed error handling for the case where top level atoms have an invalid size.
  - Apache: added APR version check for apr_brigade_insert_file (1.1.0) availability (CentOS 4.7)
  - Lighttpd 1.4.18: Added BW shaping, Last-Modified and ETag response headers, and fallthru for range requests.
  - Lighttpd 1.5.0: Fixed buffer-seconds when the key is specified in a specific context (not the global one).

## 2009-04 (version 2.1rc2) available in SVN for testing

If you want to build the latest version (version 2.1 release candidate 2), just replace '/tags/mod_h264_streaming-2.0' with '/tags/mod_h264_streaming-2.1rc2' in the two SVN export commands of the build instructions.

For example, replace the SVN export commands for [Apache](/wiki:Mod-H264-Streaming-Apache-Version2/) with the following two lines. The rest of the instructions are the same.

{{{
svn export http://h264.code-shop.com/svn/h264/tags/mod_h264_streaming-2.1rc2/apache apache_http_h264_streaming
svn export --force http://h264.code-shop.com/svn/h264/tags/mod_h264_streaming-2.1rc2/mp4split apache_http_h264_streaming
}}}

  - Lighttpd 1.5.0: Fixed first 'buffer burst' in BW traffic shaping.
  - Lighttpd 1.5.0: Better BW shaping after seek (the size of the original metadata was taken into account, instead of the new metadata).
  - Fixed stts/ctts writing for ['variable frame rate'](http://h264.code-shop.com/trac/discussion/1/36) videos.
  - Added [Adaptive streaming](http://h264.code-shop.com/demo/adaptive_streaming/video.html) demo.
  - Added 'adaptive=1' query parameter for sending metadata only.
  - Added [IIS module](/wiki:Mod-H264-Streaming-Internet-Information-Services-IIS-Version2/).
  - Fixed round off error in start/end time to sample conversion and removed floating point time calculations.
  - Apache: Added ETag header.
  - Nginx: Added Last-Modified header.
  - Apache/Nginx: Added support for range requests with start/end parameters (for streaming virtual video clips in vlc/quicktime/iphone).
  - Lighttpd 1.5.0: Added ETag header.
  - Apache2/Lighttpd 1.5.0: Added Last-Modified header.
  - Apache2/Nginx: Videos now play on iPhone and VLC Media Player.

## 2009-03 (version 2.1rc)

  - MP4: Fixed pts time scale overflow
  - MP4: Fixed ctts atom overflow
  - Lighttpd: Added bandwidth traffic shaping. No matter where you seek in the video, the first N seconds are always send at maximum speed (thus minimizing seek delay) and at the same time this limits the traffic as only N seconds of the video is buffered (greatly saving bandwidth). A little similar to what RTMP streaming offers. Supports any bit rate, variable bitrate, etc... it automatically adjusts the speed every second.
  - Flash: Added h264streaming FlowPlayer plugin.
  - FreeBSD: added include sys/types.h for off_t
  - Debian: added _LARGEFILE_SOURCE (for fseeko) to nginx config
  - 64bit: changed all %llu/%lld printf format specifiers to PRIu64/PRId64
  - 64bit: changed last ftell to ftello

## 2009-01 (version 2.0)

  - Added versions for Apache2 and Nginx.
  - MP4/Moov now fully parses and creates the headers. This gives an average saving of 50% of the meta data, improving seek/load times.
  - Added support for reading of extended boxes and 64 bit chunk offsets.
  - Added client check, so for flash clients only one video and one audio stream is returned. Other tracks, like hint tracks, are filtered out as they are not needed.
  - For clients that are not flash (e.g. quicktime player, iphone, vlc) the headers are compressed.
  - Fixed 64 bit overflows in stts that occured in video files with very large time scales.

## Wishlist / TODO

  - Support subtitle tracks
  - Support range requests with start/end parameters (for streaming virtual video clips in vlc/quicktime/iphone) for Lighttpd and IIS.
  - Add bandwidth shaping for Apache, Nginx and IIS.
  - Make range requests configurable. You may want to disable it to avoid use of download accelerators.



