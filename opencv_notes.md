
# OpenCV

Author: __*yufanana*__

Compilation of OpenCV notes.

</br>
____

6. [Computer Vision with OpenCV](#6) <br>
    6.1 [Applications](#6.1) <br>
    6.2 [Installation](#6.2) <br>
    6.3 [OpenCV](#6.3) <br>
    >   6.3.1 [Executing Python Files](#6.3.1) <br>
        6.3.2 [Open/Save Image](#6.3.2) <br>
        6.3.3 [Image Encoding](#6.3.3) <br>
        6.3.4 [Video Stream Input](#6.3.4) <br>
        6.3.5 [Drawing](#6.3.5) <br>
        6.3.6 [Thresholding](#6.3.6) <br>
        6.3.7 [Color Filtering](#6.3.7) <br>
        6.3.8 [Tennis Ball Example](#6.3.8) <br>
        6.3.9 [Contour Detection](#6.3.9) <br>

    6.4 [OpenCV with ROS](#6.4) <br>
    >  6.4.1 [CV Bridge](#6.4.1) <br>
       6.4.2 [C++ Implementation](#6.4.2) <br>

## Section 6: Computer Vision with OpenCV <a name="6"></a>
[Go to top](#top)

### 6.1 Applications <a name="6.1"></a>
[Go to top](#top)

__Image Segmentation__ <br>
The process of partitioning a digital image into multiple segments. <br>
Used to locate objects and boundaries (e.g. lines, curves) in images. <br>

__Image Thresholding__<br>
Simplest method of image segmentation. <br>
Take a colour as a threshold <br>
- any colour above threshold -> white
- any colour below threshold -> black

This process creates binary images.

__Object Detection and Recognition__ <br>
Detecting instances of semantic objects of a certain class in digital images and videos.

__Drawing__ <br>
Drawing shapes like lines, polygons, text, circles.

__Edge Detection__ <br>
Find the boundaries of objects within images. <br>
Works by detecting discontinuities in brightness. <br>
Used for image segmentation and data extraction. <br>

__Video/Image Input/Output__ <br>
Read/write images and video streams.

### 6.2 Installation <a name="6.2"></a>

__Installation__ <br>
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

### 6.3 OpenCV (no ROS) <a name="6.3"></a>
[Go to top](#top)

numpy is multidimensional array data structure is used to store pixel values of images.

#### 6.3.1 Executing Python Files <br> <a name="6.3.1"></a>
[Go to top](#top)

Include `#!/usr/bin/env python` at the top of the file. Then, enter `./file_name.py` in the terminal to run the specified file in the current directory.

OR

Enter `python3 file_name.py` in the terminal.

#### 6.3.2 Open/Save Image <br> <a name="6.3.2"></a>
[Go to top](#top)

Windows are used as placeholders for images and trackbars.

__Read__ <br>
`color_img = cv2.imread("path/to/img.jpg", CV_LOAD_IMAGE_COLOR)` for colour image. <br>
`gray_img = cv2.imread("path/to/img.jpg", CV_LOAD_IMAGE_GRAYSCALE)` for grayscale image.

__Window Operations__ <br>
`cv2.namedWindow("window_name", cv2.WINDOW_NORMAL)` to create a window holder for image. The window can be referenced later to be moved, resized, closed, etc.  <br>
`cv2.moveWindow("window_name",x_pos,y_pos)` to move the window to specified location.  <br>
`cv2.destroyAllWindows()` to destroy all windows. Usually called after the quit wait key.

__Show__ <br>
`cv2.imshow("window_name",img)` to display image in the specified window.  <br>
`stiched_img = np.concatenate((array1,array2,array3),axis=1)` to concatenate the arrays along its length. Use `axis=0` to concatenate along its height. 

Should call `cv2.waitKey(1)` to allow high GUI some time to process the draw requests from `cv2.imshow()`. waitKey returns the [key code](http://www.foreui.com/articles/Key_Code_Table.htm) of the pressed key. OR use `cv2.waitKey(1) & 0xFF == ord('q')`

__Save__ <br>
`cv2.imwrite("path/to/file"+img_name+".jpg",img)` to save the image as specified file name at specified path.

__Others__ <br>
`height, length, channels = img.shape` gives the dimensions of the numpy array. Channels are for colour images.  <br>
`img[:,:,0]` to return all the values in the first channel.  <br>
`img.dtype` to obtain image datatype.

#### 6.3.3 Image Encoding <br> <a name="6.3.3"></a>
[Go to top](#top)

- Grayscale 
- Red, Green, Blue (RGB)
- Hue, Saturation, Value (HSV)
  - Hue: 0-360, indicates type of colour
  - Saturation: 0-100%, amount of gray in colour
  - Value: 0-100%, brightness level, with 0 as black and 100 as most colour

|Color|Angle|OpenCV Angle|
|-----|-----|------------|
|Red | 0-60 | 0-30 |
|Yellow | 60-120 | 30-60 |
|Green | 120-180 | 60-90 |
|Cyan | 180-240 | 90-120 |
|Blue | 240-300 | 120-150 |
|Magenta | 300-360 | 150-180 |

OpenCV uses different ranges for HSV. <br>
- Hue: 0-180
- Saturation: 0-255
- Value: 0-255

`blue,green,red = cv2.split(color_image)` to split image into the 3 channels. <br>
Then, you can go on to show each channel image.

`gray_image = cv2.cvtColor(color_image, cv2.COLOR_BGR2GRAY)` to convert color to grayscale. <br>
`hsv_image = cv2.cvtColor(color_image, cv2.COLOR_BGR2HSV)` to convert color to HSV.

#### 6.3.4 Video Stream Input <br> <a name="6.3.4"></a>
[Go to top](#top)

`video_capture = cv2.VideoCapture(0)` to open a camera for video capturing. <br>
`video_capture = cv2.VideoCapture('absolute/path/to/video_fil.mp4')` to open a video file from local directory. <br>
`ret,frame = video_capture.read()` where frame is the image from the video, and ret is the return value. ret becomes false if no frames has been grabbed (camera disconnected/end of video file)

`video_capture.release()` Ensure that the capture object is released subsequently before exiting the script. 


Use 'Q' button to break the while-loop and exit the script. <br>
```python
# python
if cv2.waitKey(1) & 0xFF == ord('q'):
    break
```

#### 6.3.5 Drawing <br> <a name="6.3.5"></a>
[Go to top](#top)

Points are represented as tuples: `(x1,y1)`, `(x2,y2)`<br>
Color is represented in BGR tuple: `(255,0,0)` <br>
Thickness is an integer: draws filled if negative, outline if positive

`cv2.rectangle(image,pt1,pt2,color,thickness)` to draw a rectangle. <br>
`cv2.line(image,pt1,pt2,color,thickness)` to draw a line.

Axes is a tuple: (major_axis_length, minor_axis_length) <br>
`cv2.ellipse(image,center_pt,axes,angle,startAngle,endAngle,color,thickness)` to draw an ellipse.  <br>
`cv2.circle(image,center_pt,radius,color,thickness)` to draw a circle.

Origin is the bottom-left corer of the text string. <br>
`cv2.putText(image,text,orgin,font_type,font_size,color,thickness)` to put text on the image.

#### 6.3.6 Thresholding <br> <a name="6.3.6"></a>
[Go to top](#top)

Simplest method of image segmentation. <br>
Take a colour as a threshold to compare against the pixel values. <br>

`cv2.threshold(gray_image,threshold_value,max_value,threshold_style)` to run simple thresholding.<br>
max_value is typically 255 (?)

Threshold styles
- THRESH_BINARY
- THRESH_BINARY_INV
- THRESH_TRUNC
- THRESH_TOZERO
- THRESH_TOZERO_INV

Simple thresholding may not be good in all lighting conditions (e.g. shadow in a section of image) 

Adaptive thresholding:
- calculates threshold for a small region of the image
- different thresholds calculated for different regions of the same image
- greater robustness against varying illumination

`cv2.adaptive_thresholding(gray_image,max_value,adaptive_method,block_size,constant)` to run adaptive thresholding. <br>
Block size: size of neighbourhood area <br>
Constant: constant that is subtracted from the mean/weight mean calculated

Adaptive styles
- ADAPTIVE_THRESH_MEAN_C
- ADAPTIVE_THRESH_GAUSSIAN_C

#### 6.3.7 Color Filtering__ <br> <a name="6.3.7"></a>
[Go to top](#top)

The process displays only a specific color range in the image. <br>
This allows for the detection of objects with specific colors. <br>
HSV is used for filtering because it is more robust against external lighting conditions. <br>
Similar colors will be closer within the a range (angles) in HSV than in RGB.

Algorithm
- Read image as RGB
- Convert image to HSV
- Define upper and lower color ranges
- Create the mask based on color ranges

OpenCV has its own convention to define the ranges of hue, saturation and value.

#### 6.3.8 Tennis Ball Example <br> <a name="6.3.8"></a>
[Go to top](#top)

1. Choose the yellow angle range
```python
yellowLower =(30, 150, 100)
yellowUpper = (50, 255, 255)
```
2. Saturation and value ranges are can be obtained via trial & error. Generally on the higher side.

#### 6.3.9 Contour Detection <br> <a name="6.3.9"></a>
[Go to top](#top)

Contours: curves with the same color/intensity that join all the continuous points along a boundary

To find the boundaries of objects within image. <br>
This is done by detecting discontinuities in brightness. <br>
Useful for shape detection, image segmentation, object detection/recognition.

Algorithm
- Read image as RGB
- Convert image to grayscale
- Convert gray image to binary image
- Find contours using `cv2.findContours()` on the binary image
- Process the contours (e.g. area, centroid, perimeter, moment)

__Contour Hierarchy__ <br>
Outer shape: parent, inner shape: child.

Contour Retrieval Modes (RETR: retrieve)
- `RETR_LIST`: returns all contours without parent-child relationships
- `RETR_EXTERNAL`: returns extreme outer contours only
- `RETR_CCOMP`: returns all contours, arranged in a 2-level hierarchy
- `RETR_TREE`: returns all contours in full family hierarchy

`contours, hierarchy = cv2.findContours(binary_img, contour_retr_mode, contour_approx_method)`

__Contour Processing__ <br>
Can create a blank black image to overlay processed contours and check the results.

Common operations
```python
area = cv2.contourArea(c)
perimeter= cv2.arcLength(c, True)
((x, y), radius) = cv2.minEnclosingCircle(c)  # returns the circle with min area that fully contains the contour

def get_contour_center(contour):
    M = cv2.moments(contour)
    cx=-1
    cy=-1
    if (M['m00']!=0):
        cx= int(M['m10']/M['m00'])
        cy= int(M['m01']/M['m00'])
    return cx, cy
```

__Tennis Ball Detection__ <br>

Steps
1. Read image as RGB
2. Apply color filtering to get a binary image mask
3. Generate contours using the binary image
4. Draw contours that are sufficiently large

__Tennis Ball Tracking__ <br>

Steps
1. Read image as RGB
2. Apply color filtering to get a binary image mask
3. Generate contours using the binary image
4. Draw contours that are sufficiently large

## 6.4 OpenCV with ROS <a name="6.4"></a>
[Go to top](#top)

### 6.4.1 CvBridge <br><a name="6.4.1"></a>
[Go to top](#top)

The image file produced by ROS (ROS Image Message) is not immediately compatible with the OpenCV format (OpenCV cv::Mat). Thus, CvBridge is needed to do the conversion (bidirectional).

<img src="./notes_images/cv_bridge_map.png" height=150>

`bridge = CvBridge()` to make a bridge object.

```python
from cv_bridge import CvBridge, CvBridgeError

# convert ros img_msg to cv_image (e.g. in scubscriber)
try:
    cv_image = bridge.imgmsg_to_cv2(ros_image, "bgr8")
except CvBridgeError as e:
    print(e)
  
# convert cv_image to ros img_msg (e.g. in publisher_)
try:
    ros_img = bridge.cv2_to_imgmsg(cv_image, encoding = "passthrough")
except CvBridgeError as e:
    print(e)
```
OpenCV operations can be applied to cv_image after this step.

### 6.4.2 C++ Implementation__ <br> <a name="6.4.2"></a>
[Go to top](#top)

CMakeList.txt
```
find_package(OpenCV)
include_directories(${OpenCV_INCLUDE_DIRS})
add_executable(read_video_cpp src/topic03_perception/cpp/read_video.cpp)
target_link_libraries(read_video_cpp ${catkin_LIBRARIES})
target_link_libraries(read_video_cpp ${OpenCV_LIBRARIES})
```

`rosrun usb_cam usb_cam_node _pixel_format:= yuyv` to run the usb_cam

__OpenCV & ROS C++ Implementation__ <br>
For C++ OpenCV Implementation with ROS, <br>
a `image_transport::ImageTransport it_;` is used to create a subscriber/advertiser instead of a node to handle images.

CMakeList.txt
```
find_package(
  roscpp
  std_msgs
  OpenCV
  cv_bridge
  image_transport
)

include_directories(${OpenCV_INCLUDE_DIRS})
add_executable(image_pub_sub src/topic03_perception/cpp/image_pub_sub.cpp)
target_link_libraries(image_pub_sub ${catkin_LIBRARIES})
target_link_libraries(image_pub_sub ${OpenCV_LIBRARIES})
```