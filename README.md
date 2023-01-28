# live-web-site-网站直播
当然假设树莓派已经正确安装了摄像头
开启Youtube频道直播准备（等24小时）得到直播频道ID和直播码
使用命令 os.system('raspivid -o - -t 0 -vf -hf -fps 30 -b 6000000 | ffmpeg -re -ar 44100 -ac 2 -acodec pcm_s16le -f s16le -ac 2 -i /dev/zero -f h264 -i - -vcodec copy -acodec aac -ab 128k -g 50 -strict experimental -f flv rtmp://a.rtmp.youtube.com/live2/[youtube 直播码]') 完成树莓派对Youtube直播。这个命令在文件raspberrypi-youtube-live.py
通过放置在/home/pi/.config/autostart/目录下的auto-start-live-at-boot.desktop文件，使树莓派在启动完成后自动执行raspberrypi-youtube-live.py，
又，在/etc/rc.local文件，放置reboot-and-shutdown.py文件，
树莓派开机后，或者自动进入直播，或者按一下工作按钮，Youtube可见树莓派的现场直播。（硬奸见图Raspberry Pi IO Pins Layout 04.jpg），程序是reboot-and-shutdown.py
在自己的Facebook账户，链接到谷歌云，找到 YouTube Data API v3 （YouTube API 密钥）我的是通过https://console.cloud.google.com/apis/library?project=upbeat-nectar-278508
网站上安装插件：Embed Plus YouTube WordPress Plugin 设置YouTube API Key，是谷歌云的YouTube Data API v3，开通插件直播功能，获得短码[embedyt] https://www.youtube.com/embed/live_stream?channel=频道ID（UC开头的）[/embedyt] 
网站页面贴短码。然后加入其他页面程序。要注意的是，谷歌云的服务（即YouTube Data API v3）是有配额限制的，其实配额很少，几个小时就用完了（好像可以再额外申请？）。
