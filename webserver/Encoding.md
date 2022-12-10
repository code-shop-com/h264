# How to encode video in H264 format

## Ffmpeg/x264 (profile High, level 3.0) (latest versions of x264)

We have successfully been using ffmpeg/libx264 with two pass encoding using the
following commands:

```
infile ="video.avi" 
tmpfile="video_tmp.mp4" 
outfile="video.mp4"
options="-vcodec libx264 -b 512k -flags +loop+mv4 -cmp 256 \ 
         -partitions +parti4x4+parti8x8+partp4x4+partp8x8+partb8x8 \
         -me_method hex -subq 7 -trellis1 -refs 5 -bf 3 \
         -flags2 +bpyramid+wpred+mixed_refs+dct8x8 -coder 1 -me_range 16 \
         -g 250 -keyint_min 25 -sc_threshold 40 -i_qfactor 0.71 -qmin 10 \ 
         -qmax 51 -qdiff 4"

ffmpeg -y -i "$infile" -an -pass 1 -threads 2 $options "$tmpfile"

ffmpeg -y -i "$infile" -acodec libfaac -ar 44100 -ab 96k -pass 2 -threads 2 $options "$tmpfile"

qt-faststart "$tmpfile" "$outfile"
```

The last line 'qt-faststart' is optional. It doesn't hurt though and it even may
save a little time on the server which is hosting the movie files.

Thanks to S0ma for the updated options.

## Ffmpeg/x264 (profile High, level 3.0) (older versions)

Replace the options above with:

```
options="-vcodec libx264 -b 512k -bf 3 -subq 6 -cmp 256 -refs 5 -qmin 10 \
         -qmax 51 -qdiff 4 -coder 1 -loop 1 -me hex -me_range 16 -trellis 1 \ 
         -flags +mv4 -flags2 +bpyramid+wpred+mixed_refs+brdo+8x8dct \
         -partitions parti4x4+parti8x8+partp4x4+partp8x8+partb8x8 -g 250 \ 
         -keyint_min 25 -sc_threshold 40 -i_qfactor 0.71"
```

## Ffmpeg/x264 (profile Baseline, level 3.0) (iPhone)

Replace the options above with:

```
options="-vcodec libx264 -b 512k -flags +loop+mv4 -cmp 256 \ 
         -partitions +parti4x4+parti8x8+partp4x4+partp8x8+partb8x8 \ 
         -me_method hex -subq 7 -trellis 1 -refs 5 -bf 0 \ 
         -flags2 +mixed_refs -coder 0 -me_range 16 \ 
         -g 250 -keyint_min 25 -sc_threshold 40 -i_qfactor 0.71 -qmin 10 \ 
         -qmax 51 -qdiff 4""
```

## Mencoder & mp4creator

The following PHP script was contributed (thanks!):

```
system("mencoder ". $file_input ." -o ". $file_output_raw ." -ovc x264 -x264encopts
       bitrate=300:threads=auto:subq=6:partitions=all:8x8dct:me=umh:frameref=5:bframes=3:b_pyramid:weight_b
       -vf bmovl=0:0:mylogo.fifo,scale=". $nw .":". $nh .",harddup -oac faac -faacopts br=56:mpeg=4:object=2 
       -srate 44100 -ofps 24000/1001");

system("mplayer ". $file_output_raw. " -dumpaudio -dumpfile ". $file_output_aac .""); 
system("mplayer ". $file_output_raw. " -dumpvideo -dumpfile ".  $file_output_h264 ."");

system("mp4creator -create=". $file_output_aac. " ". $file_output ."");
system("mp4creator -create=". $file_output_h264. " -rate=23.976 ". $file_output ."");

system("mp4creator -hint=1 ". $file_output .""); system("mp4creator -hint=2 ".  $file_output .""); 
system("mp4creator -optimize ". $file_output .""); }}}
```

## Telestream Episode Engine Pro 5

Files transcoded by a [http://www.telestream.net/products/episode_engine.htm
Telestream Episode Engine Pro 5] are reported to work. The files are H264/AAC in
an MP4 container. They are compatible with both Flash and iPod.

## Encoding H264 on Tiger

Here is a little wisdom snippet from challefredde:

I'm using different tools but mostly this combination: On Mac OS X 10.4 Tiger:

- Perian plugin installed (watch almost all videos in Quicktime)
- Mpeg Streamclip from Squared 5
- [Quicktime codec](http://www.macupdate.com/info.php/id/20273/x264-quicktime-codec)
  Encodes better h264 videos than Quicktime's built-in.
- QTFastStart

Video: 900 kbit/s, Audio: AAC, stereo 96 kbit/s, Res: 640x360 (widescreen)

The video plays fine on iPod's.

