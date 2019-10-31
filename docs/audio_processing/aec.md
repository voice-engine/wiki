# Acoustic Echo Cancellation

In a smart speaker, the algorithm Acoustic Echo Cancellation (AEC)  is used to cancel music, which is played by itself, from the audio captured by its microphones, so it can hear your voice clearly when it is playing music.

![](/assets/images/aec.png)

The open source library `speexdsp` has a AEC algorithm. There are two examples to use it in Python and C.

## using AEC in Python
1.  `pip3 install speexdsp`
2.  create a python script named `ec.py`

    ```
    """Acoustic Echo Cancellation for wav files."""

    import wave
    import sys
    from speexdsp import EchoCanceller


    if len(sys.argv) < 4:
        print('Usage: {} near.wav far.wav out.wav'.format(sys.argv[0]))
        sys.exit(1)

    frame_size = 256

    near = wave.open(sys.argv[1], 'rb')
    far = wave.open(sys.argv[2], 'rb')

    if near.getnchannels() > 1 or far.getnchannels() > 1:
        print('Only support mono channel')
        sys.exit(2)

    out = wave.open(sys.argv[3], 'wb')
    out.setnchannels(near.getnchannels())
    out.setsampwidth(near.getsampwidth())
    out.setframerate(near.getframerate())


    print('near - rate: {}, channels: {}, length: {}'.format(
            near.getframerate(),
            near.getnchannels(),
            near.getnframes() / near.getframerate()))
    print('far - rate: {}, channels: {}'.format(far.getframerate(), far.getnchannels()))
    echo_canceller = EchoCanceller.create(frame_size, 2048, near.getframerate())

    in_data_len = frame_size
    in_data_bytes = frame_size * 2
    out_data_len = frame_size
    out_data_bytes = frame_size * 2

    while True:
        in_data = near.readframes(in_data_len)
        out_data = far.readframes(out_data_len)
        if len(in_data) != in_data_bytes or len(out_data) != out_data_bytes:
            break

        in_data = echo_canceller.process(in_data, out_data)

        out.writeframes(in_data)

    near.close()
    far.close()
    out.close()
    ```

3.  play a music (for example, `music.wav`) and record it as `rec.wav`, and run `python ec.py rec.wav music.wav out.wav`.

Note: only mono music is supported. To get a good result, `music.wav` and `rec.wav` should be aligned.

## using AEC in C
See [ec](https://github.com/voice-engine/ec)
