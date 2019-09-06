# Snips Offline Voice Assistant

>Snips is an AI voice platform for connected devices that animates product interactions with customizable voice experiences.


With Snips, we can create a Private by Design voice assistant that runs offline on the edge.

## Install

```
sudo apt-get install -y dirmngr
sudo bash -c 'echo "deb https://raspbian.snips.ai/stretch stable main" > /etc/apt/sources.list.d/snips.list'

sudo apt-key adv --keyserver pgp.mit.edu --recv-keys D4F50CDCA10A2849
# or sudo apt-key adv --keyserver pgp.surfnet.nl --recv-keys D4F50CDCA10A2849

sudo apt-get update
sudo apt-get install -y libgfortran3
sudo apt-get install -y snips-platform-voice snips-asr snips-dialogue snips-injection snips-tts snips-audio-server snips-hotword snips-nlu snips-watch

sudo apt-get install snips-platform-demo
```