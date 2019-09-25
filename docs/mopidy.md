# Mopidy

>Mopidy is an extensible music server written in Python.
Mopidy plays music from local disk, Spotify, SoundCloud, Google Play Music, and more. 
You edit the playlist from any phone, tablet, or computer using a range of MPD and web clients.



## Install
```shell
sudo apt-get install build-essential python-dev python-pip \
    python-setuptools
sudo apt-get install python-gst-1.0 \
    gir1.2-gstreamer-1.0 gir1.2-gst-plugins-base-1.0 \
    gstreamer1.0-plugins-good gstreamer1.0-plugins-ugly \
    gstreamer1.0-tools
sudo pip install mopidy mopidy-musicbox-webclient
```

These commands will install mopidy, its dependencies and mopidy webclient musicbox.

## Configure
By default, Mopidy only listens only on the IPv4 loopback interface.
To make it listen on all interfaces (both IPv4 and IPv6), create a 
configuration file `/etc/mopidy/mopidy.conf`.

```shell
sudo mkdir /etc/mopidy
echo "
[http]
hostname = ::
port = 6680
" | sudo tee /etc/mopidy/mopidy.conf
```

## Run
```shell
mopidy --config /etc/mopidy/mopidy.conf
```

## Music

https://upload.wikimedia.org/wikipedia/en/c/c3/Super_Mario_Bros._theme.ogg



## Run as a service
To make Mopidy autorun, we can create a systemd service.

```
echo "
[Unit]
Description=Mopidy music server
After=avahi-daemon.service
After=dbus.service
After=network.target
After=sound.target

[Service]
User=$USER
ExecStart=/usr/local/bin/mopidy --config /etc/mopidy/mopidy.conf

[Install]
WantedBy=multi-user.target
" | sudo tee /etc/systemd/system/mopidy.service
sudo systemctl start mopidy
sudo systemctl enable mopidy
```

For more details, please read [the official document of Mopdiy](https://docs.mopidy.com/en/latest/)
