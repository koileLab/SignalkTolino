# SignalK eReader Solutions 

## SignalK App: singalk-eink (recomended!)

https://github.com/ieb/signalk-eink

tbc

## [AvNav by Wellenvogel](https://www.wellenvogel.net/software/avnav/)  (also recomended!)

### Audio Alarm with Bluetooth Box 

- Make Sure no pulseaudio is installed/running at all! Setting up bluealsa [(HowTo)](https://forum-raspberrypi.de/forum/thread/38887-bluetooth-audio-fuer-headless-raspbian-jessie/)

- Keep in Mind AvNav was coming from standalone an later integrated into SignalK. MOB & Anchorwatch in AvNav are handled by an own system and not by the SignalK Alarm Notification like the [SignalK-Anchorwatch](https://github.com/sbender9/signalk-anchoralarm-plugin)! But you can run them side by side!
- Having AvNav on your Raspi Server you can configure `/home/pi/avnav/data/avnav_server.xml` to play AvNav-Alarms Headless via **mpg123** as described in the [AvNavManual](https://www.wellenvogel.net/software/avnav/docs/hints/configfile.html#h3:AVNCommandHandler) - The manual says it's the default but for me it wasn't:

  `<AVNCommandHandler >`
  `<!-- 	<Command name="sound" command="/bin/sh $BASEDIR/../raspberry/sound.sh 90%" repeat="1"/>
  -->`
  	`<Command name="sound" command="mpg123 -q" repeat="1"/>`
  `</AVNCommandHandler>`

- Save the File and: `sudo systemctl restart avnav`
- Btw: For starting a AvNav-MOB-Alarm from your eReader you have to turn on the "Connected Mode" by hitting the Plug Icon in the main Menu. If your are in Disconnected-Mode you are free to try routings on your client with no effect to the routing on your Server. As AvNav-MOB-Alarm is a routing function you need to be connected... 


## SignalK App: sk-on-kindle(Old Approach)

Not recommended. I failed at Code customization...

Based on SignalK Plugin [sk-on-kindle](https://www.npmjs.com/paSignalkTolinockage/@digitalyacht/sk-on-kindle) erthold  Daum made a working SignalK-App for eBookReaders. Check out his [Blog](https://projekt-kiri.blogspot.com/2018/12/loch-allmahlich-wird-es-zeit-kiri.html) The Code is in his [Dropbox](https://www.dropbox.com/s/pfmssxxjzkpzd5b/kindle.zip?dl=0). We got in touch and he allowd me to modify and publish his code with attributing him. But my skills weren't sophisticated enough...

A Videodemo of his App you can see on [PeerTube](https://diode.zone/videos/watch/b4ac9ba3-72aa-4756-ad32-c580ba9d221c)

