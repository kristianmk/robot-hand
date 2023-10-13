# Written by K. M. Knausgård 2023-10. All rights reserved.

cmake_minimum_required(VERSION 3.5.1)
project(RobotHandTest VERSION 0.1.0 LANGUAGES CXX)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Add qbdevice directory to build it as part of this project.
# Clone qbdevice-api-7.x.x so it is located next to our project folder:
# git clone --recurse-submodules https://bitbucket.org/qbrobotics/qbdevice-api-7.x.x.git
# This project was tested with qbdevice-api-7.x.x version 1a744b318d73f32553e578ff9b7ca240b2d45c07 (tag 1.1.13).
add_subdirectory(../qbdevice-api-7.x.x qbrobotics-device)

# Add executable
add_executable(RobotHandTest main.cpp)

# Make sure handTest depends on qbrobotics_driver and Serial
# Serial is not built automatically without this..
add_dependencies(RobotHandTest qbrobotics_driver Serial)

# Link with the driver library
target_link_libraries(RobotHandTest PRIVATE qbrobotics_driver::qbrobotics_driver)

