cmake_minimum_required(VERSION 3.9)

set(PROJECT_NAME TestOpenCVCmake)
project(${PROJECT_NAME})

set(CMAKE_CXX_STANDARD 11)

set(cmake_build_type release)

add_subdirectory(../Dlib/dlib/dlib dlib_build)

add_subdirectory(../ncnn/ncnn ncnn_build)
include_directories(../ncnn/ncnn/src)

find_package(OpenCV REQUIRED)

include_directories(${OpenCV_INCLUDE_DIRS})

add_executable(train_model_v2 src/train_model2.cpp src/student.cpp)

target_link_libraries(train_model_v2 ${OpenCV_LIBS} dlib::dlib stdc++fs)

add_executable(detect src/detect.cpp src/UltraFace.cpp src/student.cpp)

target_link_libraries(detect ${OpenCV_LIBS} dlib::dlib ncnn stdc++fs)
