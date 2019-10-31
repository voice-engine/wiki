# KWS

Keyword Spotting (KWS) or Keyword Search (alsa called Keyword Detection, Wake Word Detection)
is a key technology to implement a hands-free voice assistant. 
It's used to detect words such as "OK, Google", "Hey, Siri" to start a conversation.
Unlike speech recognition, KWS is a always-listening program which should be run locally without and offline.

There are a variety of KWS projects, such as [Snowboy](https://github.com/Kitt-AI/snowboy), [Mycroft Precise](https://github.com/MycroftAI/mycroft-precise), [Porcupine](https://github.com/Picovoice/Porcupine).

## Snowboy
1.  Install Snowboy

    ```bash
    sudo apt install -y libatlas-base-dev swig python3-pyaudio sox
    sudo pip3 install voice-engine
    git clone https://github.com/Kitt-AI/snowboy.git --depth=1
    cd snowboy/swig/Python3
    make
    cd ../..
    python3 setup.py build
    sudo python3 setup.py bdist_wheel
    sudo pip3 install --no-deps dist/snowboy-*-py3-none-any.whl
    ```

2.  Detect a keyword

    ```bash
    echo "
    import time
    from voice_engine.source import Source
    from voice_engine.kws import KWS


    src = Source(rate=16000, channels=1, device_name='default')
    kws = KWS(model='computer', sensitivity=0.6, verbose=True)
    src.pipeline(kws)

    def on_detected(keyword):
        print('\ndetected {}'.format(keyword))

    kws.set_callback(on_detected)
    src.pipeline_start()
    while True:
        try:
            time.sleep(1)
        except KeyboardInterrupt:
            break
    src.pipeline_stop()
    " > kws.py
    python3 kws.py
    ```