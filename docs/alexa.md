# Alexa Voice Service

## Get started
1.  [Connect to Amazon Alexa](https://dev.voicen.io/connect/alexa) to get authorized, and then save the oauth json string as `avs.json`

    [![](https://dev.voicen.io/static/alexa.svg)](https://dev.voicen.io/connect/alexa)

2.  Install python package avs

    ```
    sudo pip3 install avs
    ```

3.  Run a tap-n-talk voice assistant

    ```
    alexa-tap avs.json
    ```

4.  Setup Run a hands-free voice assistant using Snowboy as keyword detector

    a.  [setup snowboy](/kws)

    b.  run the python script

        ```
        import os
        import signal
        import time

        from voice_engine.source import Source
        from voice_engine.kws import KWS
        from avs.alexa import Alexa


        def leds_on():
            os.system("mosquitto_pub -t '/voicen/leds/value' -m '0xf'")

        def leds_off():
            os.system("mosquitto_pub -t '/voicen/leds/value' -m '0x0'")

        def main():
            logging.basicConfig(level=logging.DEBUG)

            src = Source(rate=16000, channels=4, device_name='capture')
            kws = KWS(model='alexa')
            alexa = Alexa()

            alexa.state_listener.on_listening = leds_on
            alexa.state_listener.on_finished = leds_off

            src.pipeline(kws, alexa)

            def on_detected(keyword):
                logging.info('\ndetected {}'.format(keyword))
                alexa.listen()

            kws.set_callback(on_detected)

            is_quit = []
            def signal_handler(sig, frame):
                is_quit.append(True)
                print('quit')
            signal.signal(signal.SIGINT, signal_handler)

            src.pipeline_start()
            while not is_quit:
                time.sleep(1)

            src.pipeline_stop()


        if __name__ == '__main__':
            main()
        ```

## SDKs
+ [avs python sdk](https://github.com/respeaker/avs)
+ [avs c++ sdk](https://github.com/alexa/avs-device-sdk)
