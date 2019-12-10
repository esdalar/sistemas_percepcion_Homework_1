### sistemas_percepcion_Homework_1
## Homework_1

# Exercise 1.2. Image manipulation

1- For this exercise first fork the repository https://github.com/beta-robots/webcam_capture.git and clone it inside the ws.

2- Then, modify the file " webcam_capture.cpp" and change some parameters such us colours, area around the central pixel, and so on.

///

~/catkin_ws/webcam_capture/src$ gedit webcam_capture.cpp 

///

3- Then execute the camera to see the changes done.


# Exercise 1.3. Point features

1- For this exercise first fork the repository https://github.com/beta-robots/webcam_point_features
2- Build the point_features example. (mkdir build & cd build & cmake .. & make)


Fist of al we need to install the following packages:
 
 ///
 
$ sudo apt-get install ros-melodic-camera-calibration
$ sudo apt-get install ros-melodic-usb-cam

///

Clone the repository https://github.com/beta-robots/webcam_point_features.
 
 Then, we will need to calibrate the camera. For that, we measure the square and modify in the file:
 
 ///
 
 ~/catkin_ws/src/usb_cam_calibration/launch$ gedit usb_camera_calibration.launch

///

///
 
 <launch>
	<!-- User arguments -->
	<arg name="video_device"  default="/dev/video0" />
	<arg name="show_image"  default="false" />

	<!-- camera capture -->
	<node
		name="usb_cam"
		pkg="usb_cam"
		type="usb_cam_node"
		output="screen" >
		<param name="video_device" value="$(arg video_device)" />
		<param name="image_width" value="640" />
		<param name="image_height" value="480" />
		<param name="pixel_format" value="yuyv" />
		<param name="camera_frame_id" value="usb_cam" />
		<param name="io_method" value="mmap"/>
	</node>

	<!-- camera calibration -->
	<node
		name="camera_calibration"
		pkg="camera_calibration"
		type="cameracalibrator.py"
		output="screen"
		args="--size 8x6 --square 0.1673 image:=/usb_cam/image_raw camera:=usb_cam">
	</node>

	<!-- display raw image -->
	<group if="$(arg show_image)">
		<node
			name="image_view"
			pkg="image_view"
			type="image_view"
			respawn="false"
			output="screen">
			<remap from="image" to="/usb_cam/image_raw"/>
			<param name="autosize" value="true" />
		</node>
	</group>

</launch>

///

We make some changes in the file "point_features.cpp ":

///

~/catkin_ws/src/webcam_point_features/src$ gedit point_features.cpp 

///

After modifying the cpp file, we create a package to be able to run it:

///


~/catkin_ws/src/webcam_point_features$ mkdir build
~/catkin_ws/src/webcam_point_features$ ls
build  CMakeLists.txt  launch  README.md  src
~/catkin_ws/src/webcam_point_features$ cd build/
~/catkin_ws/src/webcam_point_features/build$ cmake ..
~/catkin_ws/src/webcam_point_features/build$ make
~/catkin_ws/src/webcam_point_features/build$ ls
CMakeCache.txt  CMakeFiles  cmake_install.cmake  Makefile  point_features

///

To execute the program with the camera and see the modifications done, we just type:

///

~/catkin_ws/src/webcam_point_features/build$ ./point_features 

///





3- Find out information about ORB features and describe them in your words:


*ORB are the letters for Oriented FAST and rotated BRIEF. This is a fast robust local feature detector presented by Ethan Rublee et al. in 2011, that can be used in computer vision tasks like object recognition or 3D reconstruction.*

*Given a pixel p in an array fast compares the brightness of p to surrounding 16 pixels that are in a small circle around p. This is telling us where our feature is between these pixels.*

*References:*

*https://medium.com/@deepanshut041/introduction-to-orb-oriented-fast-and-rotated-brief-4220e8ec40cf*

*https://www.quora.com/What-is-ORB-in-computer-vision*


4- Try to detect features more sparse over all the image, by using the mask: (http://docs.opencv.org/2.4.11/modules/features2d/doc/common_interfaces_of_feature_detectors.html#featuredetector-detect)


# Exercise 1.4. Circle detection

1- Fork it
2- Build the circle_detector example. (mkdir build & cd build & cmake .. & make)

To start we will fork and clone the repository https://github.com/beta-robots/webcam_circles.git and create a package:

///

gengiro@gengiro-GL552VW:~/catkin_ws/src$ git clone https://github.com/beta-robots/webcam_circles.git
gengiro@gengiro-GL552VW:~/catkin_ws/src$ cd webcam_circles/
gengiro@gengiro-GL552VW:~/catkin_ws/src/webcam_circles$ mkdir build
gengiro@gengiro-GL552VW:~/catkin_ws/src/webcam_circles$ cd build
gengiro@gengiro-GL552VW:~/catkin_ws/src/webcam_circles/build$ make
gengiro@gengiro-GL552VW:~/catkin_ws/src/webcam_circles/build$ ls
circle_detector  CMakeCache.txt  CMakeFiles  cmake_install.cmake  Makefile

///

If needed, we can calibrate the camera like the ast exercise.

Then we change some parameters from the file "circle_detector.cpp":

///

~/catkin_ws/src/webcam_circles/src$ gedit circle_detector.cpp

///

After playing with the parameters, we type to run:

///

gengiro@gengiro-GL552VW:~/catkin_ws/src/webcam_circles/build$ ./circle_detector 

///

4- Find out information about how The Hough Transform works, and interpret and explain  the behaviour when changing the parameters. Document your Readme.md and cite the used references

*The Hough transform is a tool to identify lines*

*The point of this tool resides in the fact that the lines are a collection of points and so,the collection of points is tougher than managing a single point and so it is able to represent a line as a single point, without losing any information about it.*

*References:*

*http://aishack.in/tutorials/hough-transform-basics/*

*https://en.wikipedia.org/wiki/Hough_transform*

