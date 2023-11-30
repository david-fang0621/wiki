# Commands

Commands used in the course "FFmpeg - The Complete Guide" by Syed Andaleeb Roomy.
( https://www.udemy.com/course/ffmpeg-the-complete-guide/?referralCode=1B0CDEEB984838103727 )

## Inspecting with ffprobe

ffprobe seagull.mp4
ffprobe -v error seagull.mp4 -show_format
ffprobe -v error seagull.mp4 -show_format -show_streams
ffprobe -v error seagull.mp4 -show_format -show_streams -print_format json
ffprobe -v error seagull.mp4 -show_streams -select_streams v
ffprobe -v error seagull.mp4 -show_streams -select_streams v -show_entries stream=codec_name
ffprobe -v error seagull.mp4 -select_streams v -show_entries stream=codec_name
ffprobe -v error seagull.mp4 -select_streams v -show_entries stream=codec_name -print_format default=noprint_wrappers=1:nokey=1
ffprobe -v error seagull.mp4 -show_entries format=format_long_name -print_format default=noprint_wrappers=1:nokey=1
ffprobe -v error https://test-videos.co.uk/vids/bigbuckbunny/mp4/h264/1080/Big_Buck_Bunny_1080_10s_10MB.mp4 -show_format -show_streams -print_format json

## Playing with ffplay

ffplay -v error bullfinch.mp4
ffplay -v error bullfinch.mp4 -x 600 -y 600
ffplay -v error bullfinch.mp4 -x 600 -y 600 -noborder
ffplay -v error bullfinch.mp4 -y 600 -noborder
ffplay -v error bullfinch.mp4 -y 600 -noborder -top 0 -left 0
ffplay -v error bullfinch.mp4 -y 600 -noborder -fs
ffplay -v error bullfinch.mp4 -y 600 -noborder -an
ffplay -v error bullfinch.mp4 -y 600 -noborder -vn
ffplay -v error bullfinch.mp4 -y 600 -noborder -vn -showmode waves
ffplay -v error bullfinch.mp4 -y 600 -noborder -loop 0
ffplay -v error birds-forest.ogg -showmode waves
ffplay -v error kingfisher.jpg
ffplay -v error https://test-videos.co.uk/vids/bigbuckbunny/mp4/h264/720/Big_Buck_Bunny_720_10s_1MB.mp4 -noborder -y 600

_Section 4_

## Inputs and Outputs

ffmpeg -protocols
ffmpeg -devices
ffmpeg -formats

## Stream Selection

ffprobe multitrack.mp4 -v error -show_format -show_streams -print_format json
ffmpeg -v error -y -i multitrack.mp4 -to 1 multitrack-1s.mp4
ffprobe multitrack-1s.mp4 -v error -show_format -show_streams -print_format json
ffmpeg -v error -y -i multitrack.mp4 -to 1 -map 0 multitrack-1s.mp4
ffprobe multitrack-1s.mp4 -v error -show_format -show_streams -print_format json
ffmpeg -v error -y -i multitrack.mp4 -to 1 -map 0:v multitrack-1s.mp4
ffprobe multitrack-1s.mp4 -v error -show_format -show_streams -print_format json
ffmpeg -v error -y -i multitrack.mp4 -to 1 -map 0:0 multitrack-1s.mp4
ffprobe multitrack-1s.mp4 -v error -show_format -show_streams -print_format json
ffmpeg -v error -y -i multitrack.mp4 -to 1 -map 0:a multitrack-1s.mp4
ffprobe multitrack-1s.mp4 -v error -show_format -show_streams -print_format json
ffmpeg -v error -y -i multitrack.mp4 -to 1 -map 0:a:0 multitrack-1s.mp4
ffprobe multitrack-1s.mp4 -v error -show_format -show_streams -print_format json
ffmpeg -v error -y -i multitrack.mp4 -i second-input.mp4 -to 1 -map 1:v:0 -map 0:a:1 multitrack-1s.mp4
ffprobe multitrack-1s.mp4 -v error -show_format -show_streams -print_format json

## Filter Graphs

ffmpeg -v error -y -i bullfinch.mp4 -vf "split[bg][ol];[bg]scale=width=1920:height=1080,format=gray[bg_out];[ol]scale=-1:480,hflip[ol_out];[bg_out][ol_out]overlay=x=W-w:y=(H-h)/2" ol.mp4
ffplay -v error ol.mp4
ffmpeg -y -i four_channel_stream.wav -af "asplit=2[voice][bg];[voice]volume=volume=2,pan=mono|c0=c0+c1[voice_out];[bg]volume=volume=0.5,pan=mono|c0=c2+c3[bg_out];[voice_out][bg_out]amerge=inputs=2" audio_out.wav
ffmpeg -v error -y -i bullfinch.mp4 -i ffmpeg-logo.png -filter_complex "[1:v]scale=-1:200[small_logo];[0:v][small_logo]overlay=x=W-w-50:y=H-h-50,split=2[sd_in][hd_in];[sd_in]scale=-2:480[sd];[hd_in]scale=-2:1080[hd];[0:a]pan=stereo|FL=c0+c2|FR=c1+c3[stereo_mix]" -map "[sd]" sd.mp4 -map "[hd]" hd.mp4 -map "[stereo_mix]" stereo_mix.mp3

_Section 5_

## Encoding Basics

ffprobe -v error bullfinch.mov -select_streams v -show_entries stream=codec_name -print_format default=noprint_wrappers=1
ffmpeg -v error -y -i bullfinch.mov transcoded.mxf
ffprobe -v error transcoded.mxf -select_streams v -show_entries stream=codec_name -print_format default=noprint_wrappers=1
ffmpeg -v error -y -i bullfinch.mov transcoded.mp4
ffprobe -v error transcoded.mp4 -select_streams v -show_entries stream=codec_name -print_format default=noprint_wrappers=1
ffmpeg -v error -y -i bullfinch.mov -vcodec libx264 transcoded.mxf
ffprobe -v error transcoded.mxf -select_streams v -show_entries stream=codec_name -print_format default=noprint_wrappers=1
ffmpeg -encoders
ffmpeg -v error -y -i bullfinch.mov -vcodec libvpx-vp9 transcoded.mxf
ffmpeg -v error -y -i bullfinch.mov -vcodec libvpx-vp9 transcoded.mp4
ffprobe -v error transcoded.mp4 -select_streams v -show_entries stream=codec_name -print_format default=noprint_wrappers=1
ffprobe -v error transcoded.mp4 -select_streams a -show_entries stream=codec_name -print_format default=noprint_wrappers=1
ffmpeg -v error -y -i bullfinch.mov -vcodec libvpx-vp9 -acodec libmp3lame transcoded.mp4
ffprobe -v error transcoded.mp4 -select_streams a -show_entries stream=codec_name -print_format default=noprint_wrappers=1

## H.264 / AVC

ffprobe -v error bullfinch.mov -select_streams v -show_entries stream=codec_name,bit_rate -print_format default=noprint_wrappers=1
ffmpeg -v error -y -i bullfinch.mov -vcodec libx264 transcoded.mp4
ffprobe -v error transcoded.mp4 -select_streams v -show_entries stream=codec_name,bit_rate -print_format default=noprint_wrappers=1
ffplay -v error -an transcoded.mp4
ffmpeg -v error -y -i bullfinch.mov -vcodec libx264 -crf 10 transcoded.mp4
ffprobe -v error transcoded.mp4 -select_streams v -show_entries stream=codec_name,bit_rate -print_format default=noprint_wrappers=1
ffplay -v error -an transcoded.mp4
ffmpeg -v error -y -i bullfinch.mov -vcodec libx264 -crf 45 transcoded.mp4
ffprobe -v error transcoded.mp4 -select_streams v -show_entries stream=codec_name,bit_rate -print_format default=noprint_wrappers=1
ffplay -v error -an transcoded.mp4
ffmpeg -v error -y -i bullfinch.mov -vcodec libx264 -b:v 2M transcoded.mp4
ffprobe -v error transcoded.mp4 -select_streams v -show_entries stream=codec_name,bit_rate -print_format default=noprint_wrappers=1
ffmpeg -v error -y -i bullfinch.mov -vcodec libx264 -b:v 2M -pass 1 -f null /dev/null
ffmpeg -v error -y -i bullfinch.mov -vcodec libx264 -b:v 2M -pass 2 transcoded.mp4
ffprobe -v error transcoded.mp4 -select_streams v -show_entries stream=codec_name,bit_rate -print_format default=noprint_wrappers=1
time ffmpeg -v error -y -i bullfinch.mov -vcodec libx264 transcoded.mp4
du -sh transcoded.mp4
time ffmpeg -v error -y -i bullfinch.mov -vcodec libx264 -preset ultrafast transcoded.mp4
du -sh transcoded.mp4
time ffmpeg -v error -y -i bullfinch.mov -vcodec libx264 -preset slow transcoded.mp4
du -sh transcoded.mp4

_Section 6_

## Trimming

ffmpeg -y -v error -i nature.mp4 -ss 00:03:55.000 -to 240.0 squirrel.mp4
ffmpeg -y -v error -i nature.mp4 -ss 00:03:55.000 -t 5 squirrel2.mp4

## Merging

vim list.txt
file 'bullfinch-5s.mp4'
file 'seagull-5s.mp4'
file 'squirrel.mp4'
ffmpeg -y -v error -f concat -i list.txt merged.mp4

## Generating Thumbnails

ffmpeg -v error -i bullfinch.mp4 -vframes 1 bullfinch-poster-frame.jpg
ffprobe bullfinch-poster-frame.jpg -v error -select_streams v -show_entries stream=width,height
ffmpeg -v error -i bullfinch.mp4 -vframes 1 -vf scale=320:180 bullfinch-thumbnail.jpg
ffprobe bullfinch-thumbnail.jpg -v error -select_streams v -show_entries stream=width,height
ffmpeg -v error -i bullfinch.mp4 -ss 5 -vframes 1 -vf scale=320:180 bullfinch-thumbnail-at-5s.jpg
ffmpeg -v error -i bullfinch.mp4 -vf fps=1,scale=320:180 bullfinch-thumbnail-%02d.jpg
ls

## Scaling

ffplay -v error cow_4k.mp4 -an
ffprobe cow_4k.mp4 -v error -select_streams v -show_entries stream=width,height
ffmpeg -v error -y -i cow_4k.mp4 -vf scale=1280:720 cow_720p.mp4
ffprobe cow_720p.mp4 -v error -select_streams v -show_entries stream=width,height
ffplay -v error cow_720p.mp4 -an
ffmpeg -v error -y -i cow_4k.mp4 -vf scale=640:480 cow_480p.mp4
ffplay -v error cow_480p.mp4 -an
ffmpeg -v error -y -i cow_4k.mp4 -vf scale=-1:480 cow_480_aspect_preserved.mp4
ffmpeg -v error -y -i cow_4k.mp4 -vf scale=-2:480 cow_480_aspect_preserved.mp4
ffprobe -v error cow_480_aspect_preserved.mp4 -v error -select_streams v -show_entries stream=width,height
ffplay -v error cow_480_aspect_preserved.mp4 -an
ffmpeg -v error -y -i cow_4k.mp4 -vf scale=640:480:force_original_aspect_ratio=decrease cow_480_aspect_forced.mp4
ffprobe -v error cow_480_aspect_forced.mp4 -v error -select_streams v -show_entries stream=width,height
ffmpeg -v error -y -i cow_4k.mp4 -vf "scale=640:480:force_original_aspect_ratio=decrease,pad=640:480:(ow-iw)/2:(oh-ih)/2" cow_480_aspect_forced_and_padded.mp4
ffplay -v error cow_480_aspect_forced_and_padded.mp4 -an

## Overlay

ffplay bullfinch.mp4 -v error -an -top 0 -y 875
ffmpeg -v error -y -i bullfinch.mp4 -i ffmpeg-logo.png -filter_complex "overlay" out.mp4 && ffplay out.mp4 -v error -an -top 0 -y 875
ffmpeg -v error -y -i bullfinch.mp4 -i ffmpeg-logo.png -filter_complex "overlay=x=main_w-overlay_w-50:y=50" out.mp4 && ffplay out.mp4 -v error -an -top 0 -y 875
ffmpeg -v error -y -i bullfinch.mp4 -i ffmpeg-logo.png -filter_complex "[1:v]colorchannelmixer=aa=0.4[transparent_logo];[0:v][transparent_logo]overlay=x=main_w-overlay_w-50:y=50" out.mp4 && ffplay out.mp4 -v error -an -top 0 -y 875
ffmpeg -v error -y -i bullfinch.mp4 -i ffmpeg-logo.png -filter_complex "[1:v]scale=-1:100[smaller_logo];[0:v][smaller_logo]overlay=x=main_w-overlay_w-50:y=50" out.mp4 && ffplay out.mp4 -v error -an -top 0 -y 875
ffmpeg -v error -y -i bullfinch.mp4 -i ffmpeg-logo.png -i tux.png -filter_complex "[1:v]scale=-1:100[smaller_logo];[0:v][smaller_logo]overlay=x=main_w-overlay_w-50:y=50[after_one_logo];[after_one_logo][2:v]overlay=W-w-50:H-h-50" out.mp4 && ffplay out.mp4 -v error -an -top 0 -y 875
ffmpeg -v error -y -i bullfinch.mp4 -i ffmpeg-logo.png -i squirrel.mp4 -filter_complex "[1:v]scale=-1:100[smaller_logo];[0:v][smaller_logo]overlay=x=main_w-overlay_w-50:y=50[after_one_logo];[2:v]scale=-1:400[smaller_squirrel];[after_one_logo][smaller_squirrel]overlay=W-w-50:H-h-50" out.mp4 && ffplay out.mp4 -v error -an -top 0 -y 875

## Drawing Text or Timecode

ffplay bullfinch.mp4 -v error -an -top 240 -y 835
ffplay bullfinch.mp4 -v error -an -top 240 -y 835 -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=Birds"
ffplay bullfinch.mp4 -v error -an -top 240 -y 835 -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=Birds:fontsize=48:x=100:y=100"
ffplay bullfinch.mp4 -v error -an -top 240 -y 835 -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=Birds:fontsize=h/2:x=(w-text_w)/2:y=(h-text_h)/2"
ffplay bullfinch.mp4 -v error -an -top 240 -y 835 -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=Birds:fontsize=h/2:x=(w-text_w)/2:y=(h-text_h)/2:fontcolor=green"
ffplay bullfinch.mp4 -v error -an -top 240 -y 835 -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=Birds:fontsize=h/2:x=(w-text_w)/2:y=(h-text_h)/2:fontcolor=#000000AA"
ffplay bullfinch.mp4 -v error -an -top 240 -y 835 -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=Birds:fontsize=h/2:x=(w-text_w)/2:y=(h-text_h)/2:fontcolor=#000000AA:enable='between(t,1,3)'"
ffplay bullfinch.mp4 -v error -an -top 240 -y 835 -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=Birds:fontsize=h/2:x=(w-text_w)/2:y=(h-t\*200):fontcolor=#000000AA"
ffplay bullfinch.mp4 -v error -an -top 240 -y 835 -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=:fontsize=60:x=(w-text_w)/2:y=(h-100):fontcolor=#000000:timecode='10\:00\:00\:00':rate=30000/1001"
ffplay bullfinch.mp4 -v error -an -top 240 -y 835 -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=:fontsize=60:x=(w-text_w)/2:y=(h-100):fontcolor=#000000:timecode='10\:00\:00\:00':rate=30000/1001:box=1:boxborderw=15:boxcolor=#ffffff44"

_Section 7_

## Separating Channels

ffprobe -v error two-stereo-tracks.m4a -select_streams a -show_entries stream=index,codec_name,channels -print_format json
ffmpeg -y -v error -i two-stereo-tracks.m4a -filter_complex "amerge=inputs=2" four-channels-one-stream.m4a
ffprobe -v error four-channels-one-stream.m4a -select_streams a -show_entries stream=index,codec_name,channels -print_format json
ffmpeg -y -v error -i two-stereo-tracks.m4a -filter_complex "amerge=inputs=2,asplit=4[all0][all1][all2][all3];[all0]pan=mono|c0=c0[ch0];[all1]pan=mono|c0=c1[ch1];[all2]pan=mono|c0=c2[ch2];[all3]pan=mono|c0=c3[ch3]" -map "[ch0]" ch0.m4a -map "[ch1]" ch1.m4a -map "[ch2]" ch2.m4a -map "[ch3]" ch3.m4a
ffprobe -v error ch0.m4a -select_streams a -show_entries stream=index,codec_name,channels -print_format json

## Mixing Channels

ffprobe -v error ch0.m4a -select_streams a -show_entries stream=index,codec_name,channels -print_format json
ffmpeg -v error -y -i ch0.m4a -i ch1.m4a -i ch2.m4a -i ch3.m4a -filter_complex "amerge=inputs=4" one-stream-four-channels.m4a
ffprobe -v error one-stream-four-channels.m4a -select_streams a -show_entries stream=index,codec_name,channels -print_format json
ffmpeg -v error -y -i ch0.m4a -i ch1.m4a -i ch2.m4a -i ch3.m4a -filter_complex "amix=inputs=4" one-stream-one-channel.m4a
ffprobe -v error one-stream-one-channel.m4a -select_streams a -show_entries stream=index,codec_name,channels -print_format json
ffmpeg -v error -y -i ch0.m4a -i ch1.m4a -i ch2.m4a -i ch3.m4a -filter_complex "amerge=inputs=4,pan=mono|c0=c0+c1+c2+c3" pan-mono.m4a
ffprobe -v error pan-mono.m4a -select_streams a -show_entries stream=index,codec_name,channels -print_format json
ffmpeg -v error -y -i ch0.m4a -i ch1.m4a -i ch2.m4a -i ch3.m4a -filter_complex "amerge=inputs=4,pan=mono|c0=0.5*c0+2*c1+0.5*c2+2*c3" pan-mono-weighted.m4a
ffmpeg -v error -y -i ch0.m4a -i ch1.m4a -i ch2.m4a -i ch3.m4a -filter_complex "amerge=inputs=4,pan=stereo|FL=c0+c2|FR=c1+c3" pan-stereo.m4a
ffprobe -v error pan-stereo.m4a -select_streams a -show_entries stream=index,codec_name,channels -print_format json

_Section 8_

## Introduction to Streaming

The following files have been used in the lecture. The files are all derived from nature.mp4.

- - File: unstreamable.mp4

Description: Same as nature.mp4. Non-fast-started.

Apache httpd.conf configuration for this file:
<Files "unstreamable.mp4">

# Non-fast-started

RequestHeader unset Range
</Files>

- - File: unseekable.mp4

Description: Can be generated from nature.mp4 by fast-starting it with the following command -
ffmpeg -y -i nature.mp4 -movflags +faststart -c copy unseekable.mp4

Apache httpd.conf configuration for this file:
<Files "unseekable.mp4">

## Fast-started

## RequestHeader unset Range

Header unset "Accept-Ranges"
Header always set "Accept-Ranges" "none"
</Files>

File: pseudo-seekable.mp4

Description: Can be generated from nature.mp4 by fast-starting it with the following command -
ffmpeg -y -i nature.mp4 -movflags +faststart -c copy pseudo-seekable.mp4

Apache httpd.conf configuration for this file:
<Files "pseudo-seekable.mp4">

## Fast-started

RequestHeader unset Range
</Files>

- - File: random-seekable.mp4

Description: Can be generated from nature.mp4 by fast-starting it with the following command -
ffmpeg -y -i nature.mp4 -movflags +faststart -c copy random-seekable.mp4

Apache httpd.conf configuration for this file:
<Files "random-seekable.mp4">

## Fast-started

## No extra configuration needed

</Files>

- - File: adaptive.m3u8 (and related files)

Description: Can be generated from nature.mp4 with the following command -
ffmpeg.exe -y -i nature.mp4 -filter_complex "[0:v]split=3[720_in][480_in][240_in];[720_in]scale=-2:720[720_out];[480_in]scale=-2:480[480_out];[240_in]scale=-2:240[240_out]" -map "[720_out]" -map "[480_out]" -map "[240_out]" -map 0:a -map 0:a -map 0:a -b:v:0 3500k -maxrate:v:0 3500k -bufsize:v:0 3500k -b:v:1 1690k -maxrate:v:1 1690k -bufsize:v:1 1690k -b:v:2 326k -maxrate:v:2 326k -bufsize:v:2 326k -b:a:0 128k -b:a:1 128k -b:a:2 128k -x264-params "keyint=60:min-keyint=60:scenecut=0" -var_stream_map "v:0,a:0,name:720p-4M v:1,a:1,name:480p-2M v:2,a:2,name:240p-500k" -hls_list_size 0 -hls_time 2 -hls_segment_filename adaptive-%v-%03d.ts -master_pl_name adaptive.m3u8 adaptive-%v.m3u8

Apache httpd.conf configuration for this file:
<Files "adaptive.m3u8">

## No extra configuration needed

## </Files>

## Streaming Protocols

ffplay -v quiet -y 200 "<the-http-url>"

ffmpeg -v quiet -i "<the-http-url>" -vf "scale=-2:200,drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=RTMP:fontsize=30:x=10:y=20:fontcolor=#000000:box=1:boxborderw=5:boxcolor=#ff888888" -vcodec libx264 -f flv rtmp://localhost:1935/live/rtmpdemo

ffplay -v quiet rtmp://localhost:1935/live/rtmpdemo

ffmpeg -v quiet -i rtmp://localhost:1935/live/rtmpdemo -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=SRT:fontsize=30:x=10:y=60:fontcolor=#000000:box=1:boxborderw=5:boxcolor=#ff888888" -vcodec libx264 -f mpegts srt://localhost:1935?streamid=input/live/srtdemo

ffplay -v quiet srt://localhost:1935?streamid=output/live/srtdemo

ffmpeg -v quiet -i srt://localhost:1935?streamid=output/live/srtdemo -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=HTTP:fontsize=30:x=10:y=100:fontcolor=#000000:box=1:boxborderw=5:boxcolor=#ff888888" -vcodec libx264 -f dash -method PUT http://localhost/live/httpdemo.mpd

ffplay -v quiet http://localhost/live/httpdemo.mpd

- -

If you want to follow the demo, you need RTMP and SRT servers in addition to an HTTP server running locally. If you have Docker installed, you can easily use the following commands to quickly get an RTMP and an SRT server up and running.
docker run -d -p 1935:1935 tiangolo/nginx-rtmp
docker run -d -p 1935:1935/udp ravenium/srt-live-server

I used a local Apache server (from XAMPP stack) for HTTP and had to add this extra configuration to httpd.conf in order make it possible to upload the DASH files produced above to http://localhost/live/httpdemo.mpd:
<Directory "E:/xampp/htdocs/live">
Options Indexes FollowSymLinks Includes ExecCGI
AllowOverride All
Require all granted

<Limit GET HEAD POST PUT DELETE OPTIONS>
Require all granted
</Limit>

Dav On
</Directory>

## Progressive Download

The following files have been used in the lecture. The files are all derived from nature.mp4.

- - File: seekable-no-fast-started-no.mp4

Description: Same as nature.mp4. Non-fast-started.

Apache httpd.conf configuration for this file:
<Files "seekable-no-fast-started-no.mp4">
RequestHeader unset Range
Header set "Accept-Ranges" "none"
</Files>

- - File: seekable-no-fast-started-yes.mp4

Description: Can be generated from nature.mp4 by fast-starting it with the following command -
ffmpeg -y -i nature.mp4 -movflags +faststart -c copy seekable-no-fast-started-yes.mp4

Apache httpd.conf configuration for this file:
<Files "seekable-no-fast-started-yes.mp4">
RequestHeader unset Range
Header set "Accept-Ranges" "none"
</Files>

- - File: seekable-yes-fast-started-no.mp4

Description: Same as nature.mp4. Non-fast-started.

Apache httpd.conf configuration for this file:
<Files "seekable-yes-fast-started-no.mp4">

## No extra configuration needed

</Files>

- - File: seekable-yes-fast-started-yes.mp4

Description: Can be generated from nature.mp4 by fast-starting it with the following command -
ffmpeg -y -i nature.mp4 -movflags +faststart -c copy seekable-yes-fast-started-yes.mp4

Apache httpd.conf configuration for this file:
<Files "seekable-yes-fast-started-yes.mp4">

## No extra configuration needed

</Files>

- -

ffmpeg -f lavfi -i testsrc=duration=5 test.mp4
ffmpeg -v trace -i test.mp4
ffmpeg -v trace -i test.mp4 2>&1 | grep -e type:\'mdat\' -e type:\'moov\'
ffmpeg -i test.mp4 -movflags +faststart -c copy test-fast-started.mp4
ffmpeg -v trace -i test-fast-started.mp4 2>&1 | grep -e type:\'mdat\' -e type:\'moov\'
ffmpeg -y -f lavfi -i testsrc=duration=5 -movflags +faststart test-2.mp4
ffmpeg -v trace -i test-2.mp4 2>&1 | grep -e type:\'mdat\' -e type:\'moov\'

## Adaptive Streaming

ffprobe -v error seekable-yes-fast-started-yes.mp4 -print_format default=noprint_wrappers=1:nokey=1 -show_entries format=bit_rate

- - File: adaptive.m3u8 (and related files)

Description: Can be generated from nature.mp4 with the following command -
ffmpeg.exe -y -i nature.mp4 -filter_complex "[0:v]split=3[720_in][480_in][240_in];[720_in]scale=-2:720[720_out];[480_in]scale=-2:480[480_out];[240_in]scale=-2:240[240_out]" -map "[720_out]" -map "[480_out]" -map "[240_out]" -map 0:a -map 0:a -map 0:a -b:v:0 3500k -maxrate:v:0 3500k -bufsize:v:0 3500k -b:v:1 1690k -maxrate:v:1 1690k -bufsize:v:1 1690k -b:v:2 326k -maxrate:v:2 326k -bufsize:v:2 326k -b:a:0 128k -b:a:1 128k -b:a:2 128k -x264-params "keyint=60:min-keyint=60:scenecut=0" -var_stream_map "v:0,a:0,name:720p-4M v:1,a:1,name:480p-2M v:2,a:2,name:240p-500k" -hls_list_size 0 -hls_time 2 -hls_segment_filename adaptive-%v-%03d.ts -master_pl_name adaptive.m3u8 adaptive-%v.m3u8

## HLS & DASH with FFmpeg

HLS, TS, A+V:
ffmpeg.exe -y -i ../nature.mp4 -to 10 \
-filter_complex "[0:v]fps=30,split=3[720_in][480_in][240_in];[720_in]scale=-2:720[720_out];[480_in]scale=-2:480[480_out];[240_in]scale=-2:240[240_out]" \
-map "[720_out]" -map "[480_out]" -map "[240_out]" -map 0:a -map 0:a -map 0:a \
-b:v:0 3500k -maxrate:v:0 3500k -bufsize:v:0 3500k \
-b:v:1 1690k -maxrate:v:1 1690k -bufsize:v:1 1690k \
-b:v:2 326k -maxrate:v:2 326k -bufsize:v:2 326k \
-b:a:0 128k \
-b:a:1 96k \
-b:a:2 64k \
-x264-params "keyint=60:min-keyint=60:scenecut=0" \
-var_stream_map "v:0,a:0,name:720p-4M v:1,a:1,name:480p-2M v:2,a:2,name:240p-500k" \
-hls_time 2 \
-hls_list_size 0 \
-hls_segment_filename adaptive-%v-%03d.ts \
-master_pl_name adaptive.m3u8 \
adaptive-%v.m3u8

HLS, TS:
ffmpeg.exe -y -i ../nature.mp4 -to 10 \
-filter_complex "[0:v]fps=30,split=3[720_in][480_in][240_in];[720_in]scale=-2:720[720_out];[480_in]scale=-2:480[480_out];[240_in]scale=-2:240[240_out]" \
-map "[720_out]" -map "[480_out]" -map "[240_out]" -map 0:a \
-b:v:0 3500k -maxrate:v:0 3500k -bufsize:v:0 3500k \
-b:v:1 1690k -maxrate:v:1 1690k -bufsize:v:1 1690k \
-b:v:2 326k -maxrate:v:2 326k -bufsize:v:2 326k \
-b:a:0 128k \
-x264-params "keyint=60:min-keyint=60:scenecut=0" \
-var_stream_map "a:0,agroup:a128,name:audio-128k v:0,agroup:a128,name:720p-4M v:1,agroup:a128,name:480p-2M v:2,agroup:a128,name:240p-500k" \
-hls_time 2 \
-hls_list_size 0 \
-hls_segment_filename adaptive-%v-%03d.ts \
-master_pl_name adaptive.m3u8 \
adaptive-%v.m3u8

HLS, fMP4:
ffmpeg.exe -y -i ../nature.mp4 -to 10 \
-filter_complex "[0:v]fps=30,split=3[720_in][480_in][240_in];[720_in]scale=-2:720[720_out];[480_in]scale=-2:480[480_out];[240_in]scale=-2:240[240_out]" \
-map "[720_out]" -map "[480_out]" -map "[240_out]" -map 0:a \
-b:v:0 3500k -maxrate:v:0 3500k -bufsize:v:0 3500k \
-b:v:1 1690k -maxrate:v:1 1690k -bufsize:v:1 1690k \
-b:v:2 326k -maxrate:v:2 326k -bufsize:v:2 326k \
-b:a:0 128k \
-x264-params "keyint=60:min-keyint=60:scenecut=0" \
-var_stream_map "a:0,agroup:a128,name:audio-128k v:0,agroup:a128,name:720p-4M v:1,agroup:a128,name:480p-2M v:2,agroup:a128,name:240p-500k" \
-hls_segment_type fmp4 \
-hls_time 2 \
-hls_list_size 0 \
-hls_fmp4_init_filename adaptive-%v-init.m4s \
-hls_segment_filename adaptive-%v-%03d.m4s \
-master_pl_name adaptive.m3u8 \
adaptive-%v.m3u8

DASH, fMP4:
ffmpeg.exe -y -i ../nature.mp4 -to 10 \
-filter_complex "[0:v]fps=30,split=3[720_in][480_in][240_in];[720_in]scale=-2:720[720_out];[480_in]scale=-2:480[480_out];[240_in]scale=-2:240[240_out]" \
-map "[720_out]" -map "[480_out]" -map "[240_out]" -map 0:a \
-b:v:0 3500k -maxrate:v:0 3500k -bufsize:v:0 3500k \
-b:v:1 1690k -maxrate:v:1 1690k -bufsize:v:1 1690k \
-b:v:2 326k -maxrate:v:2 326k -bufsize:v:2 326k \
-b:a:0 128k \
-x264-params "keyint=60:min-keyint=60:scenecut=0" \
-seg_duration 2 \
adaptive.mpd

HLS+DASH, fMP4:
ffmpeg.exe -y -i ../nature.mp4 -to 10 \
-filter_complex "[0:v]fps=30,split=3[720_in][480_in][240_in];[720_in]scale=-2:720[720_out];[480_in]scale=-2:480[480_out];[240_in]scale=-2:240[240_out]" \
-map "[720_out]" -map "[480_out]" -map "[240_out]" -map 0:a \
-b:v:0 3500k -maxrate:v:0 3500k -bufsize:v:0 3500k \
-b:v:1 1690k -maxrate:v:1 1690k -bufsize:v:1 1690k \
-b:v:2 326k -maxrate:v:2 326k -bufsize:v:2 326k \
-b:a:0 128k \
-x264-params "keyint=60:min-keyint=60:scenecut=0" \
-hls_playlist 1 \
-hls_master_name adaptive.m3u8 \
-seg_duration 2 \
adaptive.mpd

- -

If you have any questions, comments, or improvement suggestions about the course or its contents, please feel free to contact me through private messages or email ( [andaleebcse@gmail.com](mailto:andaleebcse@gmail.com) ).

Syed Andaleeb Roomy
https://www.udemy.com/course/ffmpeg-the-complete-guide/?referralCode=1B0CDEEB984838103727

# Video Editting Using FFMpeg

1. Add text to video using ffmpeg

```
ffmpeg -i sample.mp4 -vf drawtext="fontfile=path: fontsize=20:fontcolor=red:x=10:y=10:text='HELLO'" output.mp4

```

1. Add logo to video using ffmpeg

```
ffmpeg -i sample.mp4 -i player_180x240.png -filter_complex "overlay=(w-t*60):10" output.mp4

ffmpeg -i sample.mp4 -i player.png -filter_complex "[v0][v1]blend=all_mode=overlay:all_opacity=0.7,format=yuv420p[v]" output.mp4

```

1. Image resize

```
ffmpeg -i player.png -vf scale=180:240 player_180x240.png

```

1. fade in/out effects

```

```

1. Apply interval into an overlay text

```
ffmpeg -i sample.mp4 -vf "drawtext=fontsize=40:fontcolor=yellow:x=(w-text_w)/2:y=h-60*t:text='HELLO':enable='between(t,2,3)'" -c:v libx264 -t 10 output.mp4

```

1. rect shape

```
ffmpeg -y -i sample.mp4 -vf "drawbox=x=10:y=10:w=100:h=100:color=white@0.5:t=fill" output.mp4

```

1. Extract frame from timestamp

ffmpeg -i 1.mp4 -vf "[in]
drawtext=fontfile=./font.ttf: text='First Line': fontcolor=red: fontsize=40: x=(w-text_w)/2: y=if(lt(t\,3)\,(-h+((3*h-200)t/6))\,(h-200)/2):enable='between(t,2.9,50)',
drawtext=fontfile=./font.ttf: text='Second Line': fontcolor=yellow: fontsize=30: x=if(lt(t\,4)\,(-w+((3w-tw)t/8))\,(w-tw)/2): y=(h-100)/2:enable='between(t,3.5,50)',
drawtext=fontfile=./font.ttf: text='Third Line': fontcolor=blue: fontsize=50: x=if(lt(t\,5)\,(2w-((3*w+tw)*t/10))\,(w-tw)/2): y=h/2:enable='between(t,4.5,50)',
drawtext=fontfile=./font.ttf:
text='Fourth Line':
fontcolor=white:
fontsize=80:
x=(w-text_w)/2:
y=if(lt(t\,6)\,(2*h-((3*h-100)*t/12))\,(h+100)/2):
enable='between(t,5.5,50)'
[out]" out.mp4

ffmpeg -i 1.mp4 -vf "[in]drawtext=fontfile=./font.ttf:text='FRIESE':fontcolor=white:fontsize=150:x=(w-text_w)/2:y=if(lt(t\,1)\,(20*h-((3*h-100)*t/1.2))\,(h+100)/2):enable='between(t,0.5,3)',drawtext=fontfile=./font.ttf:text='HANS CHRISTIAN':fontcolor=white:fontsize=150:x=(w-text_w)/2:y=if(lt(t\,1)\,(20*h-((3*h-400)*t/1.2))\,(h+400)/2):enable='between(t,1,3)',drawtext=fontfile=./font.ttf:text='FRIESE':fontcolor=#6D3100:fontsize=150:x=(w-text_w)/2:y=(h+100)/2:enable='between(t,2.5,5)',drawtext=fontfile=./font.ttf:text='HANS CHRISTIAN':fontcolor=#6D3100:fontsize=150:x=(w-text_w)/2:y=(h+400)/2:enable='between(t,2.5,5)'[out]" out.mp4

ffmpeg -i 2.mp4 -i player.png -filter_complex "[0:v][1:v] overlay=if(lt(t\,14)\,(w-t\*50),0):h/2:enable='between(t,5,14)'" -pix_fmt yuv420p -c:a copy output.mp4

Remove audio from Video

```
ffmpeg -i input.mp4 -c copy -an output.mp4

```

Convert AVI to mp4

```
ffmpeg -i input.avi -strict -2 output.mp4

```

ffprobe -v error 1.mp4
ffprobe -v error 1.mp4 -show_format
ffprobe -v error 1.mp4 -show_format -show_streams
ffprobe -v error 1.mp4 -show_format -show_streams -print_format json
ffprobe -v error 1.mp4 -show_streams -select_streams v
ffprobe -v error 1.mp4 -show_streams -select_streams v -show_entries stream=codec_name
ffprobe -v error 1.mp4 -show_streams -select_streams v -show_entries stream=codec_name -print_format default=noprint_wrappers=1
ffprobe -v error 1.mp4 -show_streams -select_streams v -show_entries stream=codec_name:nokey=1

ffprobe -v error 1.mp4 -show_streams format=format_long_name -print_format default=noprint_wrappers=1:nokey=1

### ffplay

ffplay -v error bullfinch.mp4 -7 600 -noborder
ffplay -v error bullfinch.mp4 -7 600 -noborder -fs -an
ffplay -v error bullfinch.mp4 -7 600 -noborder -fs -vn
ffplay -v error bullfinch.mp4 -7 600 -noborder -fs -showmode waves
ffplay -v error bullfinch.mp4 -7 600 -noborder -loop 0
F: Full screen
M: mute
0~9: Volumn
S: step next
-> forward 10s
<- back 10s
ESC: quit

### Media Concepts

### Image:

1. Pixel

- Smallest representation of a point in 2D space
- Building block of an image
- Has a color - represented in RGB or YUV
- Can have transparency information( alpha )

1. Resolution

- Represents quality
- Denoted as width \* height
- Examples: HD (1920*1080), UHD (3840*2160), 4K (4096\*2160)

1. Aspect Ratio

### Audio

- Smallest digital representation of a sound
- Building block of an audio
- Can be stored as 8/16/24/32 bit value (bit depth)
- More bits => higher quality audio

1. Audio frequency

- How many sampels per second
- Examples: 44.1kHz, 48kHz
- Higher frequency => higher quaility

1. Audio Channels

- Represents a single sequence of samples
- Channels of the same audio track are meant to be played together
- Channels can be organized in "channel layouts"
- Examples: Mono (single), Stereo (two channels), 5.1, 7.1

1. Audio Tracks

- Organize different sounds that relate to the same timeline

### Video

- Sequence of images
- Has time duration
- Each image is called a frame

1. FPS (video Frame rate)

- Frames per second
- Examples: 23.98, 24, 25, 29.70, 30, 50, 59.94, 60

1. Video Compression

- works by removing redundant information
- Spatial redundancy - within a frame
- Temporal redundancy - across frames

### Codes

What's a codec?

- Encoding and decoding
- Can mean a format or specification, or software library/plugin
  Video Codes: H.264, H.265, VP9, Prores, DNxHD
  Audio COdes: PCM, AAC, Mp3

### Containers

What's a container?

- Package/wrapper for the media essence
- File format
- How the media data is organized inside a file
- Examples: MP4, MXF (broadcast), QT/MOV (Broadcast), MKV, WAV, M4A

### Transcoding

1. What is transcoding?

- From one codec to another
- Example: Prores to H.264

1. Transmuxing

- From one container to another
- Example: MXF to MP4

1. Thumbnail generation

- Preview image
- Search hit
- Hover-scrubbing
- Poster frame

1. Frame rate conversion (25 FPS => 30 FPS)

- Support different TV standards (PAL/NTSC)
- Higher FPS: preserve slow motion quality for editing
- Lower FPS: playback/streaming

1. Bitrate conversion
2. Change GOP size
3. Overlay (logo, Watermark, Graphics)
4. Subtitles / Captions
5. Timecode
6. Convert video resolution
7. Audio volume adjustment
8. Audio mixing
9. Audio extraction
10. Audio resampling
11. Apply effects (Flip, Cropping, Color adjustment, Noise)

### FFmpeg

### FFmpeg Architecture

- Basic Process
  Input -> FFmpeg -> Output
- Transcoding
  Input -> Unpack -> Uncompress -> Compress -> Pack -> Output 1. Unpack means Demux 2. Uncompress -> Decode 3. Compress -> Encode 4. Pack -> Mux
- Transcoding and Filters
  ![[Pasted image 20220404193014.png]]
  ![[Pasted image 20220404193407.png]]

### Inputs and Outputs

```
ffmpeg -i <input-protocal>:<input-identifier>
	.... <filters and other options> ....
- f <output device or format>
<output-protocol>:<output-identifier>

ffmpeg -protocols
ffmpeg -devices
ffmpeg -formats

```

- Files
  ![[Pasted image 20220404193913.png]]
- Network
  ![[Pasted image 20220404194007.png]]
- Pipes, stdin, stdout
  ![[Pasted image 20220404194047.png]]
- Generated Inputs
  ![[Pasted image 20220404194229.png]]
- Screen capture
  ![[Pasted image 20220404194259.png]]
- Webcam capture
  ![[Pasted image 20220404194557.png]]
- Microphone capture
  ![[Pasted image 20220404194647.png]]

### Stream selection

### Video manipulation

# Stream Protocols

1. RTMP (Real-time Messaging Protocol)

- Based on TCP
- Low-latency
- Developed by Macromedia (acquired by Adobe)
- Adobe Flash player
- Not being updated anymore, so doesn't support the recent codes
- Requires extra browser plugin
- Requires RTMP server (Ingest protocol)

1. HTTP

- Based on TCP
- Unlikely to be blocked anywhere
- No separate streaming server required
- HTML5 video
- MSE (Media source extensions)
- HLS, MPEG-DASH
- JavaScript players
- No extra browser plugin needed
- No separate server required (Distribution purpose)

1. SRT (Secure Reliable Transport)

- Based on UDP
- Faster than RTMP
- Reliable on unpredictable networks
- Almost no adoption
- UDP not supported in browsers

1. FFmpeg

ffplay -v quiet -y 200 "<the-http-url>"

ffmpeg -v quiet -i "<the-http-url>" -vf "scale=-2:200,drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=RTMP:fontsize=30:x=10:y=20:fontcolor=#000000:box=1:boxborderw=5:boxcolor=#ff888888" -vcodec libx264 -f flv rtmp://localhost:1935/live/rtmpdemo

ffplay -v quiet rtmp://localhost:1935/live/rtmpdemo

ffmpeg -v quiet -i rtmp://localhost:1935/live/rtmpdemo -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=SRT:fontsize=30:x=10:y=60:fontcolor=#000000:box=1:boxborderw=5:boxcolor=#ff888888" -vcodec libx264 -f mpegts srt://localhost:1935?streamid=input/live/srtdemo

ffplay -v quiet srt://localhost:1935?streamid=output/live/srtdemo

ffmpeg -v quiet -i srt://localhost:1935?streamid=output/live/srtdemo -vf "drawtext=fontfile='c\:/Windows/Fonts/courbd.ttf':text=HTTP:fontsize=30:x=10:y=100:fontcolor=#000000:box=1:boxborderw=5:boxcolor=#ff888888" -vcodec libx264 -f dash -method PUT http://localhost/live/httpdemo.mpd

ffplay -v quiet http://localhost/live/httpdemo.mpd

```

If you want to follow the demo, you need RTMP and SRT servers in addition to an HTTP server running locally. If you have Docker installed, you can easily use the following commands to quickly get an RTMP and an SRT server up and running.

```

docker run -d -p 1935:1935 tiangolo/nginx-rtmp
docker run -d -p 1935:1935/udp ravenium/srt-live-server

```

I used a local Apache server (from XAMPP stack) for HTTP and had to add this extra configuration to httpd.conf in order make it possible to upload the DASH files produced above to <http://localhost/live/httpdemo.mpd:>

```

<Directory "E:/xampp/htdocs/live">
Options Indexes FollowSymLinks Includes ExecCGI
AllowOverride All
Require all granted

<Limit GET HEAD POST PUT DELETE OPTIONS>
Require all granted
</Limit>

Dav On
</Directory>

```

# Progressive Download
1. Single file media
- Container format: MP4, WebM, Ogg
- Playback
What's the file format? Do I know how to parse the file? -> Is it audio or video or both? -> What's the video width and height? -> Codecs -> If I have to seek to the 123rd second, where in this file can I find the media data for that particular time?
- The index
Lookup table -> where to find meida data of a time or frame -> Difficult for the encoder to know the contents of the index beforehand -> That's why it's usually written at the end
2. Structure of MP4 (How to find the index)
- Includes Similar to Apple Quicktime File Format (QT/MOV)
- Hierarchical
- Atom / Box
- Structure : ftyp | mdat | moov
fast started: ftyp | moov | mdat
3. Progressive Download
```

The following files have been used in the lecture. The files are all derived from nature.mp4.

1. File: seekable-no-fast-started-no.mp4
   Description: Same as nature.mp4. Non-fast-started.
   Apache httpd.conf configuration for this file:

```
<Files "seekable-no-fast-started-no.mp4">
  RequestHeader unset Range
  Header set "Accept-Ranges" "none"
</Files>

```

1. File: seekable-no-fast-started-yes.mp4
   Description: Can be generated from nature.mp4 by fast-starting it with the following command -

```
ffmpeg -y -i nature.mp4 -movflags +faststart -c copy seekable-no-fast-started-yes.mp4

```

Apache httpd.conf configuration for this file:

```
<Files "seekable-no-fast-started-yes.mp4">
  RequestHeader unset Range
  Header set "Accept-Ranges" "none"
</Files>

```

1. File: seekable-yes-fast-started-no.mp4
   Description: Same as nature.mp4. Non-fast-started.
   Apache httpd.conf configuration for this file:

```
<Files "seekable-yes-fast-started-no.mp4">
  ## No extra configuration needed
</Files>

```

1. File: seekable-yes-fast-started-yes.mp4
   Description: Can be generated from nature.mp4 by fast-starting it with the following command -

```
ffmpeg -y -i nature.mp4 -movflags +faststart -c copy seekable-yes-fast-started-yes.mp4

```

Apache httpd.conf configuration for this file:

```
<Files "seekable-yes-fast-started-yes.mp4">
  ## No extra configuration needed
</Files>

```

FFmpeg

```
ffmpeg -f lavfi -i testsrc=duration=5 test.mp4
ffmpeg -v trace -i test.mp4
ffmpeg -v trace -i test.mp4 2>&1 | grep -e type:\\'mdat\\' -e type:\\'moov\\'
ffmpeg -i test.mp4 -movflags +faststart -c copy test-fast-started.mp4
ffmpeg -v trace -i test-fast-started.mp4 2>&1 | grep -e type:\\'mdat\\' -e type:\\'moov\\'
ffmpeg -y -f lavfi -i testsrc=duration=5 -movflags +faststart test-2.mp4
ffmpeg -v trace -i test-2.mp4 2>&1 | grep -e type:\\'mdat\\' -e type:\\'moov\\'

```

# Adaptive Streaming

- Segmanted media
- Multi-bitrate variants
- Auto-adaptation to changing network conditions

ffprobe -v error seekable-yes-fast-started-yes.mp4 -print_format default=noprint_wrappers=1:nokey=1 -show_entries format=bit_rate

- - File: adaptive.m3u8 (and related files)

Description: Can be generated from nature.mp4 with the following command -
ffmpeg.exe -y -i nature.mp4 -filter_complex "[0:v]split=3[720_in][480_in][240_in];[720_in]scale=-2:720[720_out];[480_in]scale=-2:480[480_out];[240_in]scale=-2:240[240_out]" -map "[720_out]" -map "[480_out]" -map "[240_out]" -map 0:a -map 0:a -map 0:a -b:v:0 3500k -maxrate:v:0 3500k -bufsize:v:0 3500k -b:v:1 1690k -maxrate:v:1 1690k -bufsize:v:1 1690k -b:v:2 326k -maxrate:v:2 326k -bufsize:v:2 326k -b:a:0 128k -b:a:1 128k -b:a:2 128k -x264-params "keyint=60:min-keyint=60:scenecut=0" -var_stream_map "v:0,a:0,name:720p-4M v:1,a:1,name:480p-2M v:2,a:2,name:240p-500k" -hls_list_size 0 -hls_time 2 -hls_segment_filename adaptive-%v-%03d.ts -master_pl_name adaptive.m3u8 adaptive-%v.m3u8

# HLS & DASH

1. HLS

- HTTP Live Streaming
- Developed by Apply
- Released in 2009
- Most popular streaming format
- Proprietary

1. DASH

- Dynamic Adaptive Streaming over HTTP
- MPEG-DASH
- First international standard in 2012
- Collaboration of many companies

# Video Manipulation

1. FFmpeg Trimming
   ffmpeg -y -v error -i in.mp4 -ss 00:03:55.000 -to 240.0 out.mp4 (-to 240.0 means 04:00)
   ffmpeg -y -v error -i in.mp4 -ss 00:03:55.000 -t 5 out.mp4 (-t 5 means 5 seconds)
2. Merging
   ffmpeg -y -v error -f concat -i list.txt merged.mp4
3. Generating thumbnail
   ffmpeg -v error -i in.mp4 -vframes 1 out.jpg
   ffmpeg -v error -i in.mp4 -vframes 1 -vf scale=320:180 out.jpg
   ffmpeg -v error -i in.mp4 -ss 5 -vframes 1 -vf scale=320:180 out.jpg (5s)
   ffmpeg -v error -i in.mp4 -vf fps=1,scale=320:180 out-%02d.jpg
4. Scaling
   ffmpeg -v error -y -i in.mp4 -vf sacle=1280:720 out.mp4
   ffmpeg -v error -y -i in.mp4 -vf sacle=-2:720 out.mp4 (keep aspected ratio)
   ffmpeg -v error -y -i in.mp4 -vf sacle=1280:720:force_original_aspect_ratio=decrease out.mp4 (height auto decrease)
   ffmpeg -v error -y -i in.mp4 -vf "sacle=1280:720:force_original_aspect_ratio=decrease,pad=640,480:(ow-iw)/2:(oh-ih)/2" out.mp4 (bouncing box)
   ow: output width
   iw: input width
5. Overlay
   ffmpeg -v error -y -i input.mp4 -i logo.png -filter_complex "overlay=x=main_w-overlay_w-50:y=50" output.mp4

> main_w : the width of the background video
> overlay_w: the width of the overlay

ffmpeg -v error -y -i input.mp4 -i logo.png -filter_complex "[1:v]colorchanelmixer=aa=0.4[transparent_logo];[0:v][transparent_logo]overlay=x=main_w-overlay_w-50:y=50" output.mp4

ffmpeg -v error -y -i input.mp4 -i logo.png -filter_complex "[1:v]scale=-1:100[smaller_logo];[1:v][smaller_logo]overlay=x=main_w-overlay_w-50:y=50" output.mp4

1. Drawing Text & Timecode
   -vf "drawtext=fontfile='c\:/windows/Fonts/courbd.ttf':text=Birds:fontsize=h/2:x=(w-text_w)/2:y=(h-text_h)/2:fontcolor=green:enable='betwen(t,1,3)'"

- vf "drawtext=fontfile='c\:/windows/Fonts/courbd.ttf':text=Birds:fontsize=h/2:x=(w-text_w)/2:y=(h-text_h)/2:fontcolor=green:enable='betwen(t,1,3)'"

TODOS:

1. Apply transparent athlete's photo
2. Keep Image aspect rate
3. Channel
