##Setup
Install Raspberry configuration UI to enable camera
<pre>
sudo aptitude install raspi-config
sudo raspi-config
</pre>
Add driver module for V4L2
<pre>
sudo modprobe bcm2835-v4l2
echo "bcm2835-v4l2" | tee -a /etc/modules
</pre>
Use VLC for streaming
<pre>
sudo apt-get install vlc
raspivid -o - -t 0 -n -w 600 -h 400 -fps 12 | cvlc -vvv stream:///dev/stdin --sout '#rtp{sdp=rtsp://:8554/}' :demux=h264
</pre>
Stream with NetCat
<pre>
raspivid -t 0 -w 1280 -h 720 -hf -ih -fps 20 -o - | nc -k -l -p 5000
</pre>

To play H264 format, we can use mplayer
<pre>
mplayer -fps 200 -demuxer h264es ffmpeg://tcp://raspberrypi.local:5000
</pre>

Now live stream is available at [rtsp://raspberrypilocal:8554](rtsp://raspberrypi.local:8554/)

##Reference
- http://www.ics.com/blog/raspberry-pi-camera-module
- https://www.raspberrypi.org/documentation/usage/camera/README.md
