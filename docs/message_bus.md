# Message Bus

![](assets/images/speaker_top.png)

The VOICEN OS uses MQTT as a message bus. We can control LEDs and AMP via the message bus.
We can also subscribe touch key events from the message bus.

## Turn On/Off the LEDs
```
mosquitto_pub -t /voicen/leds/value -m 0xf
mosquitto_pub -t /voicen/leds/value -m 0x0
```

## Enable or Disable the AMP
```
mosquitto_pub -t /voicen/amp -m 1
mosquitto_pub -t /voicen/amp -m 0
```

## Detect touch key events
```
mosquitto_sub -t /voicen/touch
```

## How it works
`mosquitto` is used as the MQTT broker. A IO service is running at background to receive IO control messages
and send touch key event.

You can enable, disable, start, stop or restart the IO service with `systemctl`:
```
sudo systemctl stop io
sudo systemctl start io
sudo systemctl restart io
sudo systemctl status io
sudo systemctl disable io
sudo systemctl enable io
```

+ the IO program is a python script at `/usr/local/bin/io_service.py`
+ the IO systemd service is at `/etc/systemd/system/io.service`
