# Make sure we use the correct vesion
cmake_minimum_required(VERSION 3.14)

# Add the "src" directory as include directory to allow including all "hal-xxx" modules using include.
include_directories(src)

# Add the common data to the project.
add_subdirectory(src/hal-common)
add_subdirectory(src/hal-feather-m0)

# Add the toolchain projects.
add_subdirectory(hal-toolchain/arm-gcc-link)

# Name the project.
project(blink)

# Set the upload port, use * and ? to select the first matching device.
set(UPLOAD_PORT "/dev/cu.usbmodem*")

# Define the library to build.
add_library(blink STATIC src/Application.cpp src/main.cpp)
target_link_libraries(blink HAL-common HAL-feather-m0)

# Link the firmware
arm_gcc_link(blink)
