# Downloading and building the H264 Streaming Module for Nginx (version 2)

## Dependencies

For more information on downloading and installing Nginx, please read the
official [getting started](http://wiki.codemongers.com/NginxGettingStarted)
instructions.

We will be using version 0.7.9 of Nginx.

```
cd ~ 
wget http://www.nginx.eu/download/sources/nginx-0.7.9.tar.gz tar 
zxvf nginx-0.7.9.tar.gz
```

## Download

Download the source of the H264 Streaming Module for Nginx.  

```
cd ~ 
wget https://github.com/code-shop-com/h264/blob/main/download/nginx_mod_h264_streaming-2.2.7.tar.gz
tar -zxvf nginx_mod_h264_streaming-2.2.7.tar.gz
```

## Build

Run configure in the Nginx directory with the following additions to the
commandline.  

```
cd ~/nginx-0.7.9 
./configure --add-module=$HOME/nginx_mod_h264_streaming-2.2.7 --sbin-path=/usr/local/sbin --with-debug 
```

Make and install Nginx.  

```
make 
sudo make install
```

## Configuration

Edit the configuration file (in /usr/local/nginx/conf/nginx.conf) so that file
requests ending in ".mp4" are handled by the 'mp4' command. Add the following
lines (around line 43). 

```
location ~ \.mp4$ { mp4; }
```

Start Nginx.  

```
sudo /usr/local/sbin/nginx
```

## License

See the [license](../license.md) section.

## Testing

Continue to the [testing](testing.md) page to verify your setup.


