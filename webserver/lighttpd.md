# Downloading and building the H264 Streaming Module for Lighttpd (version 2)

## Dependencies

To make sure you have all dependencies (configuration files, startup scripts)
installed it's best to first install Lighttpd via 'apt-get'.

```
sudo apt-get install lighttpd
```

## Download Lighttpd 1.4.18

Download the source of Lighttpd and the H264 Streaming Module.

```
cd ~ 
wget https://github.com/code-shop-com/h264/blob/main/download/lighttpd-1.4.18_mod_h264_streaming-2.2.9.tar.gz
tar -zxvf lighttpd-1.4.18_mod_h264_streaming-2.2.9.tar.gz
```

## Download Lighttpd 1.4.19 & 1.4.20 (and other 1.4.x)

Follow the instructions for 'Download Lighttpd 1.4.18' first. Then continue with
the following steps.

Download a source distribution (e.g. [version 1.4.28](http://download.lighttpd.net/lighttpd/releases-1.4.x/lighttpd-1.4.28.tar.gz)
build and install your version of Lighttpd (from the official
site) as you would do normally.

The following instructions are basically a copy of the Lighttpd's page of
[How to add a Lighttpd plugin](http://trac.lighttpd.net/trac/wiki/HowToWriteALighttpdPlugin)

### Prerequisites 
Make sure you have automake 1.9 (required by autogen.sh), autoconf 2.59 and 
libtool 1.5.x.

### Files
Copy the module's files from the 1.4.18 source distribution to
your source distribution (lighttpd-1.4.x). 

```
cp lighttpd-1.4.18/src/mod_h264_streaming.c lighttpd-1.4.x/src/ 
cp lighttpd-1.4.18/src/mod_streaming_export.h lighttpd-1.4.x/src/ 
... see below for a list of all the files to copy ...  
cp lighttpd-1.4.18/src/output_mp4.* lighttpd-1.4.x/src/
```

### Makefile
First you add the following to the lighttpd-1.4.x/src/Makefile.am file: 

```
lib_LTLIBRARIES += mod_h264_streaming.la 
mod_h264_streaming_la_SOURCES = mod_h264_streaming.c \
                                mod_streaming_export.h \
                                moov.c moov.h \
                                mp4_io.c mp4_io.h \
                                mp4_reader.c mp4_reader.h \
                                mp4_writer.c mp4_writer.h \
                                mp4_process.c mp4_process.h \
                                output_bucket.c output_bucket.h \
                                output_mp4.c output_mp4.h
mod_h264_streaming_la_CFLAGS = $(AM_CFLAGS) -DBUILDING_H264_STREAMING
mod_h264_streaming_la_LDFLAGS = -module -export-dynamic -avoid-version -no-undefined 
mod_h264_streaming_la_LIBADD = $(common_libadd)
```

*(for example, just after 'mod_flv_streaming')*

Then, you type this: 

```
./autogen.sh 
./configure --enable-maintainer-mode --prefix=${HOME}/test/lighttpd-1.4.x
```

in the lighttpd-1.4.x directory. The 'enable-maintainer-mode will trigger a
rebuild of all makefiles by autoconf ...

Note: You may not see the plugin listed in the 'Plugins: enabled:' list. No
reason to worry.

After this you are all set and should type 'make && make install' - the exe+libs
will be installed in ${HOME}/test/lighttpd-1.4.x.

## Download Lighttpd 1.5.0

```
cd ~ 
wget https://github.com/code-shop-com/h264/blob/main/download/lighttpd-1.5.0_mod_h264_streaming-2.2.7.tar.gz
tar -zxvf lighttpd-1.5.0_mod_h264_streaming-2.2.9.tar.gz 
```

## Build

Run configure in the Lighttpd directory. 

```
cd ~/lighttpd-1.4.18 
./configure
```

Make and install Lighttpd.  ` make sudo make install `

## Configuration

Edit the configuration file (in /etc/lighttpd/lighttpd.conf) so that file
requests ending in ".mp4" are handled by the mod_h264_streaming module.

```
server.modules = ( ..., "mod_h264_streaming", ...) 
h264-streaming.extensions = ( ".mp4" )
```

Make sure that DAEMON in your startup script (/etc/init.d/lighttpd) is set to
point to the locally build version.

```
DAEMON=/usr/local/sbin/lighttpd
```

Start Lighttpd 

```
sudo /etc/init.d/lighttpd start
```

## Advanced configuration

Two other modules that you may consider using are mod_expire and
mod_secdownload. The order of the modules in your configuration is important. If
you are using mod_secdownload to prevent hotlinking of your mp4 files make sure
that it is included before the mod_h264_streaming in the module list.

```
server.modules = ( "mod_expire", "mod_secdownload", "mod_h264_streaming", etc...  }
```

Bandwidth shaping is enabled by setting the h264-streaming.buffer-seconds
option.

```
# Files ending in .mp4 and .f4v are served by the module
h264-streaming.extensions = ( ".mp4", ".f4v" )
# The number of seconds after which the bandwidth is shaped (defaults to
# 0=disable)
h264-streaming.buffer-seconds = 10 
```

Also add an Expires/Cache-Control header for your video files, so video files
can be cached by webbrowsers or a CDN provider.

```
# Add Expires/Cache-Control header
$HTTP["url"] =~ "\.(mp4|f4v)$" { expire.url = ( "" => "access 8 hours" ) }
```

Use mod_secdownload to prevent hotlinking.

```
secdownload.secret          = "secret" 
secdownload.document-root   = "/var/www/video/" 
secdownload.uri-prefix      = "/video/" 
secdownload.timeout         = 3600
```

## License

See the [license](../license.md) section.

## Testing

Continue to the [testing](testing.md) page to verify your setup.

