cmake_minimum_required(VERSION 3.9)

set(PROJECT_NAME TestOpenCVCmake)
project(${PROJECT_NAME})

set(CMAKE_CXX_STANDARD 11)

set(cmake_build_type release)

add_subdirectory(./dlib dlib_build)

add_subdirectory(./ncnn ncnn_build)
include_directories(./ncnn/src)

find_package(OpenCV REQUIRED)

include_directories(${OpenCV_INCLUDE_DIRS})

add_executable(train_model train_model.cpp)

target_link_libraries(train_model ${OpenCV_LIBS} dlib::dlib stdc++fs)

add_executable(train_model2 train_model2.cpp student.cpp)

target_link_libraries(train_model2 ${OpenCV_LIBS} dlib::dlib stdc++fs)


add_executable(data_view face_data_webcam.cpp)

target_link_libraries(data_view dlib::dlib)

add_executable(detect detect.cpp UltraFace/UltraFace.cpp student.cpp)

target_link_libraries(detect ${OpenCV_LIBS} dlib::dlib ncnn stdc++fs)

add_executable(detect_v2 detect1.cpp UltraFace/UltraFace.cpp student.cpp class.cpp)

target_link_libraries(detect_v2 ${OpenCV_LIBS} dlib::dlib ncnn stdc++fs ${MYSQLCONNECTORCPP_LIBRARY})

