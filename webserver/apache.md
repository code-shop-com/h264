# Downloading and building the H264 Streaming Module for Apache (version 2)

We will be using [apxs2](http://httpd.apache.org/docs/2.0/programs/apxs.html),
the APache eXtenSion tool, to build and install the module for the Apache
server.

Make sure you have apxs2 installed: 

```
sudo apt-get install apache2-threaded-dev
```

## Download

Download the source of the H264 Streaming Module for Apache.  

```
cd ~ 
wget https://github.com/code-shop-com/h264/blob/main/download/apache_mod_h264_streaming-2.2.7.tar.gz
tar -zxvf apache_mod_h264_streaming-2.2.7.tar.gz 
```

## Build

```
cd ~/mod_h264_streaming-2.2.7 
./configure --with-apxs=`which apxs2` 
make
sudo make install
````

## Configuration

Edit the configuration file (in /etc/apache/httpd.conf) so that file requests
ending in ".mp4" are handled by the h264_streaming_module.

```
LoadModule h264_streaming_modulei /usr/lib/apache2/modules/mod_h264_streaming.so
AddHandler h264-streaming.extensions .mp4
```

Start Apache.  

```
sudo /etc/init.d/apache start
```

## Build & Configuration (CentOS 5.2)

CentOS users can follow these intructions for building the module instead. It
uses apxs (instead of apxs2) and httpd (instead of apache).

```
sudo yum install httpd-devel 
sudo yum install httpd mod_ssl

cd ~/mod_h264_streaming-2.2.5 
./configure 
make 
sudo make install

echo 'LoadModule h264_streaming_module /usr/lib/httpd/modules/mod_h264_streaming.so' >> /etc/httpd/conf/httpd.conf
echo 'AddHandler h264-streaming.extensions .mp4' >> /etc/httpd/conf/httpd.conf

sudo /etc/init.d/httpd start
```

## License

See the [license](../license.md) section.

## Testing

Continue to the [testing](testing.md) page to verify your setup.

