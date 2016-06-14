##Setup

sudo modprobe bcm2835-v4l2
echo "bcm2835-v4l2" | tee -a /etc/modules
sudo apt-get install vlc
raspivid -o - -t 0 -n -w 600 -h 400 -fps 12 | cvlc -vvv stream:///dev/stdin --sout '#rtp{sdp=rtsp://:8554/}' :demux=h264
