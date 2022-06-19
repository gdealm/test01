cmake_minimum_required(VERSION 3.1)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(SimGridTemplateProject) # TODO: give a real name to your project here

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")

find_package(SimGrid 3.22 REQUIRED) # This template requires SimGrid v3.22

include_directories(${SimGrid_INCLUDE_DIR})

find_package(MPI)
set(DMPI_C_COMPILER "/usr/bin/smpicc")

find_package(OpenMP)
IF(OPENMP_FOUND)
  SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
ENDIF()

add_executable(ping-pong ping-pong.cpp)
target_link_libraries(ping-pong ${SimGrid_LIBRARY})

add_executable(master-workers master-workers.cpp)
target_link_libraries(master-workers ${SimGrid_LIBRARY})

add_executable(roundtrip roundtrip.c)
target_link_libraries(roundtrip ${SimGrid_LIBRARY})
