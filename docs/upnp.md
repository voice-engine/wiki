# UPnP/DLNA

DLNA uses Universal Plug and Play (UPnP) for media management, discovery and control. UPnP defines the types of device that DLNA supports ("server", "renderer", "controller") and the mechanisms for accessing media over a network.

Here We use `Mopidy` + `upmpdcli` as a UPnP media render and a phone as a UPnP media controller to play music.

## Install Mopidy
Go to [Mopidy](/mopidy) to install it.

## Install upmpdcli

```shell
sudo apt-key adv --keyserver pool.sks-keyservers.net --recv-key 7808CE96D38B9201

echo 'deb http://www.lesbonscomptes.com/upmpdcli/downloads/raspbian/ stretch main' | \
sudo tee /etc/apt/sources.list.d/upmpdcli.list
sudo apt update
sudo apt install upmpdcli
```

## Configure
The configuration file is `/etc/upmpdcli.conf`. You can rename the UPnP media render by 
changing `friendlyname` in `/etc/upmpdcli.conf`.


## Stream music
