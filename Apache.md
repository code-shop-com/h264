Downloading and building the H264 Streaming Module for Apache (version 2)
=========================================================================

Dependencies
------------

We will be using [http://httpd.apache.org/docs/2.0/programs/apxs.html apxs2],
the APache eXtenSion tool, to build and install the module for the Apache
server.

Make sure you have apxs2 installed: {{{ sudo apt-get install
apache2-threaded-dev }}}

== Download ==

Download the source of the H264 Streaming Module for Apache.  {{{ cd ~ wget
http://h264.code-shop.com/download/apache_mod_h264_streaming-2.2.7.tar.gz tar
-zxvf apache_mod_h264_streaming-2.2.7.tar.gz }}}

== Build ==

{{{ cd ~/mod_h264_streaming-2.2.7 ./configure --with-apxs=`which apxs2` make
sudo make install }}}

== Configuration ==

Edit the configuration file (in /etc/apache/httpd.conf) so that file requests
ending in ".mp4" are handled by the h264_streaming_module.

{{{ LoadModule h264_streaming_module
/usr/lib/apache2/modules/mod_h264_streaming.so AddHandler
h264-streaming.extensions .mp4 }}}

Start Apache.  {{{ sudo /etc/init.d/apache start }}}

== Build & Configuration (CentOS 5.2) ==

CentOS users can follow these intructions for building the module instead. It
uses apxs (instead of apxs2) and httpd (instead of apache).

{{{ sudo yum install httpd-devel sudo yum install httpd mod_ssl

cd ~/mod_h264_streaming-2.2.5 ./configure make sudo make install

sudo vi /etc/httpd/conf/httpd.conf Add the line 'AddHandler
h264-streaming.extensions .mp4' after the line 'LoadModule h264_streaming_module
/usr/lib/httpd/modules/mod_h264_streaming.so' sudo /etc/init.d/httpd start }}}

== License ==

This version is free if you agree to the
[http://creativecommons.org/licenses/by-nc-sa/3.0/ noncommercial license].
Please mention its use on your website, in the lines of 'This website uses H264
pseudo video streaming technology by [http://h264.code-shop.com CodeShop]'.

Our commercial license is very inexpensive, see the following page to check if
you need a [wiki:Mod-H264-Streaming-License-Version2 commercial license].

== Testing ==

Continue to the [wiki:Mod-H264-Streaming-Testing-Version2 testing] page to
verify your setup.

== Demo ==

See [http://h264-demo.code-shop.com/demo/apache/testlist.html] for a demo
running Apache.



