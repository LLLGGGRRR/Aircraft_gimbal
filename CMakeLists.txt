cmake_minimum_required(VERSION 3.22)

#
# This file is generated only once,
# and is not re-generated if converter is called multiple times.
#
# User is free to modify the file as much as necessary
#

# ���ø�����֧��
add_link_options(
    -u _printf_float   # ������ѡ�����Ԥ����������
)
# Setup compiler settings
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS ON)

  
# Define the build type
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Debug")
endif()

# Set the project name
set(CMAKE_PROJECT_NAME Aircraft_gimbal)

# Include toolchain file
include("cmake/gcc-arm-none-eabi.cmake")

# Enable compile command to ease indexing with e.g. clangd
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)

# Core project settings
project(${CMAKE_PROJECT_NAME})
message("Build type: " ${CMAKE_BUILD_TYPE})

# Enable CMake support for ASM and C languages
enable_language(C ASM)

# Create an executable object type
add_executable(${CMAKE_PROJECT_NAME})

# Add STM32CubeMX generated sources
add_subdirectory(cmake/stm32cubemx)

# Link directories setup
target_link_directories(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user defined library search paths
)

# Add sources to executable
target_sources(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user sources here
    Components/Algorithm/QuaternionEKF.c
    Components/Controller/controller.c
    Components/Devices/BMI088driver.c
    Components/Devices/BMI088Middleware.c
    Components/Devices/transfer_function.c
    Components/kalman_filter.c
    Components/user_lib.c
    Application/Src/Sensor_task.c
    BSP/bsp_dwt.c
    BSP/bsp_PWM.c
    BSP/bsp_can.c
    BSP/bsp_usart.c
    User/main_task.c
    Module/damiao.c
    Module/pid.c
    Module/m3508.c
)

# Add include paths
target_include_directories(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user defined include paths
    Components/Algorithm
    Components/Algorithm/Include
    Components/Controller
    Components/Devices
    Components
    Application/Inc
    BSP
    User
    Module
)

# Add project symbols (macros)
target_compile_definitions(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user defined symbols
)

# Add linked libraries
target_link_libraries(${CMAKE_PROJECT_NAME}
    stm32cubemx

    # Add user defined libraries
)

