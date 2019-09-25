# JACK Audio Connection Kit

![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/3e/LogoJack.png/440px-LogoJack.png)

>JACK Audio Connection Kit (or JACK; a recursive acronym) is a professional sound server daemon that provides real-time, low-latency connections for both audio and MIDI data between applications that use its API. 

There are two JACK implementations (JACK1 and JACK2), see [this comparison for the difference between the two](https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2). In short, JACK1 and JACK 2 are equivalent implementations of the same protocol.
JACK2 uses dbus to talk with other applications such as PulseAudio, X.
Using JACK2 without X requires some additional hacks.
So we use JACK1 instead of JACK2 here.


## Install
```
sudo apt install jackd1
```

## Use JACK as an ALSA PCM
Edit /etc/asound.conf (system wide settings) to have these lines:
```
pcm.rawjack {
    type jack
    playback_ports {
        0 system:playback_1
    }
}

pcm.jack {
    type plug
    slave { pcm "rawjack" }
    hint {
        description "JACK Audio Connection Kit"
    }
}
```

## Run
```
jackd -v -d alsa -d hw:Codec -P
```

## Play audio
```
aplay -v -D jack audio.wav
```



## Configure
```
$ cat /etc/security/limits.d/audio.conf 
# Provided by the jackd package.
#
# Changes to this file will be preserved.
#
# If you want to enable/disable realtime permissions, run
#
#    dpkg-reconfigure -p high jackd

@audio   -  rtprio     95
@audio   -  memlock    unlimited
#@audio   -  nice      -19
```


## Multiple users

To setup JACK for multiple users, we can run JACK in promiscuous mode.

1.  start JACK with a systemd service

    ```shell
    echo '
    [Unit]
    Description=Start the JACK server in promiscuous mode
    After=sound.target

    [Service]
    Type=simple
    Environment="JACK_PROMISCUOUS_SERVER="
    UMask=0
    ExecStart=/usr/bin/jackd -d alsa -d hw:Codec -P -o 1

    [Install]
    WantedBy=multi-user.target

    ' | sudo tee /etc/systemd/system/jackd.service
    sudo systemctl start jackd
    sudo systemctl enable jackd
    ```

2.  export the environment variable `JACK_PROMISCUOUS_SERVER` to let a JACK client use JACK

    ```
    JACK_PROMISCUOUS_SERVER=
    export JACK_PROMISCUOUS_SERVER
    aplay -v audio.wav
    ```

## Reference
1. https://wiki.archlinux.org/index.php/JACK_Audio_Connection_Kit
2. http://jack-audio.10948.n7.nabble.com/Jack-Devel-How-to-use-jackd-as-a-system-wide-server-td20053.html
