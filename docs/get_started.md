# Get Started

![](assets/images/1/4.jpg)

## Prepare a Micro SD card
1.  Download a VOICEN OS image (.zip)

    + from [OneDrive](https://1drv.ms/u/s!AkzbobHAw5zajjy-e2Aj9UNGSWkw?e=1CEm5m)

    + from [百度网盘](https://pan.baidu.com/s/1dwWxdZixOBVyjwxSJj06eQ#list/path=%2Fsharelink530048537-5237633763359%2FVOICEN%20OS&parentPath=%2Fsharelink530048537-5237633763359)


2.  Download and install [Etcher](https://www.balena.io/etcher/)

3. use Etcher to write the latest VOICEN OS image into a Micro SD card

4. Insert the micro SD card into Nanopi Neo Air and power on the device. It may take 40 seconds to start.


## Setup WiFi

<iframe width="560" height="315" src="https://www.youtube.com/embed/mDg0haANwbM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

1.  Press and hold the touch key for more than 4 seconds to turn the device into WiFi setup mode.
2.  Go to the web app - [Hey WiFi](https://voice-engine.github.io/hey-wifi) to broadcast WiFi settings over sound.
3.  After the device received the WiFi settings and connected to the WiFi network, it sends its IP address to the web app, and then the web app generates a link which is linked to the device dashboard.
4.  Click the link with the device's IP address, we will get the dashboard of the device.

![](assets/images/hey_wifi_web_app.png)

## Device Dashboard

![](assets/images/device_web.png)

## Add a New User Using Web Terminal

We can open a web terminal to add a new user. The default user is `root` and its password is `1234`.
After a new user is created, the user `root` will be no longer allowed to login the web terminal.

![](assets/images/web_terminal.png)

## Play with Jupyter Lab

![](assets/images/jupyterlab.png)

We can also open JupyterLab which is a very powerful web IDE. It allows you to create and share documents that contain live code, equations, visualizations and narrative text. In this document, you can run python code or shell commands to play sound, make a plot and analyze data.