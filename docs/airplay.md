# Shairport-Sync for AirPlay

>Shairport Sync is an AirPlay audio player – it plays audio streamed from iTunes, iOS, Apple TV and macOS devices and AirPlay sources such as Quicktime Player and ForkedDaapd, among others.
Audio played by a Shairport Sync-powered device stays synchronised with the source and hence with similar devices playing the same source. In this way, synchronised multi-room audio is possible for players that support it, such as iTunes.

## Install
```shell
sudo apt install shairport-sync
```

This will install shairport-sync and start the systemd service `shairport-sync.service`.

## Configure
The configuration file is `/etc/shairport-sync.conf`.

After you change the configuration, you should restart `shairport-sync` by running
`sudo systemctl restart shairport-sync`

## Using AirPlay on iOS
1.  play any music and open iOS control center

    ![assets/images/ios_control_center.png]

2.  Choose the AirPlay device

    ![assets/images/ios_airplay.png]