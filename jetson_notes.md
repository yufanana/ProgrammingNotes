# Jetson Notes

Author: __*yufanana*__
</br>
____

## Table of Contents <a name="top"></a>
1. [

First Boot
1. Format SD Card with SD Card Formatter
2. Download the Jetson Nano Developer Kit Image and flash it onto the SD Card
3. Load the SD Card onto the Jetson
4. Boot up

- `sudo apt-get install python3-pip` to install python
- `sudo -H pip install -U jetson-stats` to monitor and control the Jetson
- `jtop` to view system performance
- `cheese` to open the webcam software
- `gst-launch-1.0 nvarguscamerasrc ! nvoverlaysink` to run the Gstreamer and test RPi Camera

__Install VS Code__ <br>
```sh
cd Downloads
sudo apt-get install curl
curl -L https://github.com/toolboc/vscode/releases/download/1.32.3/code-oss_1.32.3-arm64.deb
 -o code-oss_1.32.3-arm64.deb
 sudo dpkg -i code-oss_1.32.3-arm64.deb
```

```sh
$ git clone https://github.com/JetsonHacksNano/installVSCode.git
$ cd installVSCode
$ ./installVSCodeWithPython.sh
```

`/usr/bin/python3 -m pip install -U pylint --user`