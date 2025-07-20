cmake_minimum_required(VERSION 3.15)

project(finddoxygen VERSION 0.1.0)

# Add the cmake folder for custom modules
set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})

add_executable(finddoxygen  src/main.cpp)

add_subdirectory(docs/)