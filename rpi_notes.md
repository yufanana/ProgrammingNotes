# RPi Notes

Author: __*yufanana*__
</br>
____

## Setup

Install the official [RPi Imager](https://www.raspberrypi.org/software/) software. <br>
Choose the Raspberry Pi OS (32-bit). <br>
Advised to use 32GB MicroSD card. <br>
Prepare mouse and keyboard to connect to RPi directly.

After installation of RPi OS, open the terminal.

`sudo raspi-config` to configure VNC, SSH, Camera, boot-up options etc.

`hostname -I` to get IP address.

## Image Backup
Based on instructions from [magpi](https://magpi.raspberrypi.org/articles/back-up-raspberry-pi).

__Copy SD Card Image__ <br>
RPi Image can be backed up on Windows using WindowsDiskImager.

OR

__Schedule Backups with Déjà Dup__ <br>
```
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install deja-dup
```

## Misc Notes

Higher screen resolution will impair processing power.

`df -h` to view *disk free* in *human* readable view.

## GPIO
<img src="./notes_images/rpi_gpio_pinout.jpg" height=200>

## OpenCV Installation

I followed the instructions [here](http://www.codebind.com/cpp-tutorial/install-opencv-ubuntu-cpp/) to build OpenCV. Below is a summary of the instructions in the link. Building allows you to choose the dependencies you need. [Here](https://www.pyimagesearch.com/2019/09/16/install-opencv-4-on-raspberry-pi-4-and-raspbian-buster/) is a supplementary link for RPi. <br>

Update
```
$ sudo apt-get update && sudo apt-get upgrade
```

Free up space
```
$ sudo apt-get purge wolfram-engine libreoffice*
$ sudo apt-get clean && sudo apt-get autoremove -y
```

Install dependencies: `sudo apt-get install <dependency>`

The following section breaks down the usage of the dependencies. A full command for copy and paste is found at the end.

1. Developer tools to configure OpenCV build process
```
build-essential cmake git pkg-config libopencv-dev unzip
```

2. Python & numpy
```
python3.7-dev python3-numpy 
```

3. Image I/O Packages
```
libjpeg-dev libpng-dev
```

4. Video I/O Packages, Video Streams
```
libavcodec-dev libavformat-dev libavutil-dev libavfilter-dev libavresample-dev libswscale-dev libxvidcore-dev libv4l-dev libx264-dev
``` 

5. Highgui to display images
```
libgtk2.0-dev libgtk-3-dev libfontconfig1-dev libpango1.0-dev libcanberra-gtk*
```

6. Optimise OpenCV operations
```
libatlas-base-dev gfortran
```

Full Command of the above dependencies
```
$ sudo apt-get install build-essential cmake git pkg-config libopencv-dev unzip python3.7-dev python3-numpy libjpeg-dev libpng-dev libavcodec-dev libavformat-dev libavutil-dev libavfilter-dev libavresample-dev libswscale-dev libxvidcore-dev libv4l-dev libx264-dev libgtk2.0-dev libgtk-3-dev libfontconfig1-dev libpango1.0-dev libatlas-base-dev gfortran
```

Additional dependencies (unknown usage)
```
libcairo2-devlibgdk-pixbuf2.0-dev libtbb2 libtbb-dev libdc1394-22-dev libeigen3-dev libtheora-dev libvorbis-dev sphinx-common libtbb-dev yasm libfaac-dev libopencore-amrnb-dev libopencore-amrwb-dev libopenexr-dev libgstreamer-plugins-base1.0-dev libhdf5-dev libhdf5-serial-dev libhdf5-103 libqtgui4 libqtwebkit4 libqt4-test python3-pyqt5 
```

Get OpenCV Method 1
```
$ sudo -s
$ cd /opt
/opt$ git clone https://github.com/Itseez/opencv.git && git clone https://github.com/Itseez/opencv_contrib.git
```

Get OpenCV Method 2
```
$ wget -O opencv.zip https://github.com/opencv/opencv/archive/4.0.0.zip
$ wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.0.0.zip
$ unzip opencv.zip && unzip opencv_contrib.zip
$ mv opencv-4.0.0 opencv && mv opencv_contrib-4.0.0 opencv_contrib
```

Configure Python3 in Virtual Environment
```
$ wget https://bootstrap.pypa.io/get-pip.py && sudo python3 get-pip.py
$ sudo pip install virtualenv virtualenvwrapper && sudo rm -rf ~/get-pip.py ~/.cache/pip
$ nano ~/.profile
```

Add the following lines to the end of the file
```
# virtualenv and virtualenvwrapper
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source /usr/local/bin/virtualenvwrapper.sh
```

```
$ source ~/.profile && mkvirtualenv py3cv4 -p python3
$ pip install numpy
$ cd ~/opencv && mkdir build && cd build
```

Build & install OpenCV without Virtual Environment
```
/opt$ cd opencv && mkdir release && cd release

/opt/opencv/release$ cmake -D BUILD_TIFF=ON -D WITH_CUDA=OFF -D ENABLE_AVX=OFF -D WITH_OPENGL=OFF -D WITH_OPENCL=OFF -D WITH_IPP=OFF -D WITH_TBB=ON -D BUILD_TBB=ON -D WITH_EIGEN=OFF -D WITH_V4L=OFF -D WITH_VTK=OFF -D BUILD_TESTS=OFF -D BUILD_PERF_TESTS=OFF -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=/opt/opencv_contrib/modules /opt/opencv/

# most time-consuming part
/opt/opencv/release$ make -j4 && make install && ldconfig

/opt/opencv/release$ exit && cd
```

Check OpenCV
```
$ pkg-config --modversion opencv
```


