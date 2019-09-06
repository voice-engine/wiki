# ALSA

>The Advanced Linux Sound Architecture (ALSA) provides audio and MIDI functionality to the Linux operating system. ALSA has the following significant features: Efficient support for all types of audio interfaces, from consumer sound cards to professional multichannel audio interfaces. Fully modularized sound drivers.

>Advanced Linux Sound Architecture (ALSA) is a software framework and part of the Linux kernel that provides an application programming interface (API) for sound card device drivers.

## ALSA devices
run `arecord -l` to list capture devices or run `aplay -l` to list playback devices.

## Capture
`arecord -f S16_LE -c 4 -r 16000 -d 3 -v audio.wav`

