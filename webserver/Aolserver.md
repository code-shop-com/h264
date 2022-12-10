# Downloading and building the H264 Streaming Module for AolServer (version 2)

## Dependencies

Please read the official [AOLserver](http://www.aolserver.com/) site for more
information on downloading and install AOLserver and Tcl.

## Download

Download the source of the H264 Streaming Module for AOLserver.  {{{ cd ~ wget
http://h264.code-shop.com/download/aolserver_mod_h264_streaming-2.2.7.tar.gz tar
-zxvf aolserver_mod_h264_streaming-2.2.7.tar.gz }}}

## Build

Edit the 'NSHOME' variable in the provided 'Makefile' to point to your installed
AOLserver.

Make and install the module.  ` make make install `

## Configuration

Edit your AOLserver configuration file ('nsd.tcl') and add the module:

{{{ ns_section "ns/server/server1/modules" ns_param mod_h264_streaming
mod_h264_streaming.so }}}

Start AOLserver: ` bin/nsd -ft nsd.tcl `

## Usage

test.tcl {{{ set file_url "trailer2.mp4" set handle [h264open $file_url
"start=20&end=30"] set length [h264length $handle] ns_startcontent ns_write
"HTTP/1.0 200 OK Content-Type: video/mp4 Content-Length: $length \n" while {1} {
if {[h264eof $handle]} { break } set buf [h264read $handle] ns_write $buf }
h264close $handle }}}

The streaming module also implements FLV streaming for convenience. Note that
for FLV streaming the start parameter is given in bytes. The module checks the
incoming URL for the '.flv' extension, if your FLV video files don't have an
extension then you can force it by adding 'input=flv' to the query parameter.
E.g: {{{ set file_url "trailer2" set handle [h264open $file_url
"start=43751640&input=flv"] }}}

## License

This version is free if you agree to the
[noncommercial license](http://creativecommons.org/licenses/by-nc-sa/3.0/).
Please mention its use on your website, in the lines of 'This website uses H264
pseudo video streaming technology by [CodeShop](http://h264.code-shop.com)'.

Our commercial license is very inexpensive, see the following page to check if
you need a [commercial license](/wiki:Mod-H264-Streaming-License-Version2/).

## Testing

Continue to the [testing](/wiki:Mod-H264-Streaming-Testing-Version2/) page to
verify your setup.

