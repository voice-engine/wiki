# IO

![](assets/images/mic+amp.png)


## Used

| name       | number  | usage        |
|------------|---------|--------------|
| PA2        | 2       | AMP PWR_EN   |
| PA3        | 3       | AMP_MUTE     |
| PC0        | 64      | BLUE LED     |
| PC1        | 65      | GREEN LED    |
| PC2        | 66      | YELLOW LED   |
| PC3        | 67      | RED LED      |
| PG11       | 203     | TOUCH KEY    |

To convert IO name to IO number:

```python
# n(PC3) = ('C' - 'A') * 32 + 3 = 2 * 32 + 3 = 67
name = 'PC3'
number = (ord(name[1]) - ord('A')) * 32 + int(name[2])
```

There are several ways to control IO.

## Via IO registers (direct memory access)
```shell
sudo apt install -y sunxi-tools
sudo sunxi-pio -m PC1=1  # turn on green LED
```

Accessing IO registers has the high priority.

## Via IO service
By default, there is a IO service to detect the touch key and to control the LEDs and amplifier. The IO service provides MQTT message bus to access.

```
mosquitto_pub -t /voicen/leds/value -m 0xf
mosquitto_pub -t /voicen/leds/value -m 0x0
```


## Via GPIO sysfs interface

```shell
sudo su
cd /sys/class/gpio
echo 65 > export               # export the IO to userspace
echo out > gpio65/direction    # set IO as output
echo 1 > gpio65/value
echo 0 > gpio65/value
echo 65 > unexport             # Reverses the effect of exporting to userspace
```


## Via gpiod

```shell
sudo apt install -y gpiod
sudo gpioset 0 65=0  # turn on green LED
sudo gpiomon 0 203   # detect touch event 
```



## Reference
1. https://github.com/brgl/libgpiod
2. https://github.com/linux-sunxi/sunxi-tools
3. https://www.kernel.org/doc/Documentation/gpio/sysfs.txt

   

