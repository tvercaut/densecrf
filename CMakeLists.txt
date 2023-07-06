cmake_minimum_required(VERSION 3.25)
project(densecrf)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Warnings compiler flags
if(MSVC)
  add_compile_options(/W4)
else()
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Default build type
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE RelWithDebInfo)
endif()
message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")

# Get Eigen
include(FetchContent)
FetchContent_Declare(
  Eigen
  GIT_REPOSITORY https://gitlab.com/libeigen/eigen.git
  GIT_TAG        3.4.0
  SYSTEM
)
FetchContent_GetProperties(Eigen)
if(NOT eigen_POPULATED)
  FetchContent_Populate(Eigen)
  include_directories(SYSTEM ${eigen_SOURCE_DIR})
endif()

include_directories(include)

add_subdirectory(src)
add_subdirectory(examples)
add_subdirectory(external)
