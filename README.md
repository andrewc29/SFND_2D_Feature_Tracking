# SFND 2D Feature Tracking

<img src="images/keypoints.png" width="820" height="248" />

The idea of the camera course is to build a collision detection system - that's the overall goal for the Final Project. As a preparation for this, you will now build the feature tracking part and test various detector / descriptor combinations to see which ones perform best. This mid-term project consists of four parts:

* First, you will focus on loading images, setting up data structures and putting everything into a ring buffer to optimize memory load. 
* Then, you will integrate several keypoint detectors such as HARRIS, FAST, BRISK and SIFT and compare them with regard to number of keypoints and speed. 
* In the next part, you will then focus on descriptor extraction and matching using brute force and also the FLANN approach we discussed in the previous lesson. 
* In the last part, once the code framework is complete, you will test the various algorithms in different combinations and compare them with regard to some performance measures. 

See the classroom instruction and code comments for more details on each of these parts. Once you are finished with this project, the keypoint matching part will be set up and you can proceed to the next lesson, where the focus is on integrating Lidar points and on object detection using deep-learning. 

## Dependencies for Running Locally
1. cmake >= 2.8
 * All OSes: [click here for installation instructions](https://cmake.org/install/)

2. make >= 4.1 (Linux, Mac), 3.81 (Windows)
 * Linux: make is installed by default on most Linux distros
 * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
 * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)

3. OpenCV >= 4.1
 * All OSes: refer to the [official instructions](https://docs.opencv.org/master/df/d65/tutorial_table_of_content_introduction.html)
 * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors. If using [homebrew](https://brew.sh/): `$> brew install --build-from-source opencv` will install required dependencies and compile opencv with the `opencv_contrib` module by default (no need to set `-DOPENCV_ENABLE_NONFREE=ON` manually). 
 * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)

4. gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using either [MinGW-w64](http://mingw-w64.org/doku.php/start) or [Microsoft's VCPKG, a C++ package manager](https://docs.microsoft.com/en-us/cpp/build/install-vcpkg?view=msvc-160&tabs=windows). VCPKG maintains its own binary distributions of OpenCV and many other packages. To see what packages are available, type `vcpkg search` at the command prompt. For example, once you've _VCPKG_ installed, you can install _OpenCV 4.1_ with the command:
```bash
c:\vcpkg> vcpkg install opencv4[nonfree,contrib]:x64-windows
```
Then, add *C:\vcpkg\installed\x64-windows\bin* and *C:\vcpkg\installed\x64-windows\debug\bin* to your user's _PATH_ variable. Also, set the _CMake Toolchain File_ to *c:\vcpkg\scripts\buildsystems\vcpkg.cmake*.


## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./2D_feature_tracking`.


Project Submission Report Breakdown:

MP1 -

In order to add in the data buffer, I added in a vector of data frames and push in my most recent frame while popping the oldest. If there is less than 2 frames, simply push the frame in without popping any out.

MP2 - The keypoint detection section was rather simple using the class defined method for HARRIS and Shi-tomasi detectors and then the openCV functions for FAST, BRISK, ORB, AKAZE and SIFT. These can be selected by changing the input string 'detectorType'.

MP3 - The keypoints outside of the vehicle in front of us are not of interest so we remove them. This is done by checking the dimensions of the keypoints we generated during deteciton. If the detection is not within the predefined box of the car in front of us then we throw it out.

MP4 - Descriptor function has been updated to include BRIEF, ORB, FREAK, AKAZE and SIFT. The descriptor type can be changed using the string 'descriptorType'.

MP5 - I updated the matchKeypoints function to allow for both FLANN and k-nearest neighbors.

MP6 - I updated the k-nearest neighbors matching to include a distance ratio of 0.80.

MP7 - To speed up the process for MP7, MP8 and MP9, I added in an outer loop to loop over all the detector types and output the time and number of keypoints per combination. Doing this I was able to test all of the detectors to see the number of keypoints and how each keypoints looks when overlayed on the image. Notes for my findings have been added into the Camera Sensor Fusion Project Performance.csv file included.

MP8 - Using the looping mechanism described in MP7, I was able to loop over all detector/descriptor combinations and output the number of keypoints with a BF approach. Notes for my findings have been added into the Camera Sensor Fusion Project Performance.csv file included.

MP9 - Using the same looping scheme, I was able to see the time it took each detector/descriptor combination to detect, descript and match. I then selected 1) FAST detector / BRIEF descriptor, 2) FAST detector / ORB decsriptor, 3) FAST detector / FREAK descriptor as my best combinations given my measuring stick being keypoints/ms. Notes for my findings have been added into the Camera Sensor Fusion Project Performance.csv file included.

Thank you!

