cmake_minimum_required(VERSION 2.8.7)
project(caffetest)

SET(CMAKE_CXX_COMPILER "g++")
SET( CMAKE_BUILD_TYPE Release )
SET( CMAKE_CXX_FLAGS "-O3 -std=c++11" )
SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/build)
SET(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

INCLUDE_DIRECTORIES( ${PROJECT_SOURCE_DIR}/include )
include_directories(/usr/local/cuda-9.0/targets/x86_64-linux/include)
include_directories(/usr/local/cuda/lib64)
include_directories(/home/tricster/caffe/include)
include_directories(/home/tricster/caffe/build/src)
include_directories(/opt/ros/kinetic/include/opencv-3.3.1-dev)
include_directories(/opt/ros/kinetic/include/opencv-3.3.1-dev/opencv)
include_directories(/opt/ros/kinetic/include/opencv-3.3.1-dev/opencv2)
include_directories(/usr/include/boost)


LINK_DIRECTORIES( ${PROJECT_SOURCE_DIR}/lib)
LINK_DIRECTORIES("/usr/lib")
link_directories(/usr/lib/x86_64-linux-gnu/)
link_directories(/home/tricster/caffe/build/lib)

FIND_PACKAGE( OpenCV 3.3 REQUIRED )

add_executable(ssd_detect ssd_detect.cpp)
target_link_libraries(ssd_detect caffe	
		${OpenCV_LIBS}
		boost_system 
		boost_filesystem
		glog
		gflags
		protobuf)

add_executable(ssd_video ssd_video.cpp)
target_link_libraries(ssd_video caffe	
		${OpenCV_LIBS}
		boost_system 
		boost_filesystem
		glog
		gflags
		protobuf)

add_executable(dnn opencv_dnn.cpp)
target_link_libraries(dnn 
		${OpenCV_LIBS}
		)

add_executable(video opencv_video.cpp)
target_link_libraries(video
		${OpenCV_LIBS}
		)
