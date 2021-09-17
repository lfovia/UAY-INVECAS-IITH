cmake_minimum_required(VERSION 2.8)

project( sleepDetectionEAR )

include(../../../../../dlib-19.21/dlib/cmake)

find_package( OpenCV REQUIRED )

include_directories( ${OpenCV_INCLUDE_DIRS} )

add_executable( detectSleep sleepDetectionEAR.cpp )

target_link_libraries( detectSleep dlib::dlib ${OpenCV_LIBS} )
