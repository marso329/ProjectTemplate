cmake_minimum_required (VERSION 3.5.1)
project (Template)
set(CMAKE_BUILD_TYPE Release)

# The version number.
set (Tutorial_VERSION_MAJOR 1)
set (Tutorial_VERSION_MINOR 0)

include_directories(./include)

file(GLOB SOURCES "./src/*.cpp" "./src/*.c")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ./lib)
set (CMAKE_CXX_FLAGS "-std=c++11 -g")

add_library(Template SHARED ${SOURCES})
target_link_libraries(Template  -lboost_system )


install(TARGETS Template DESTINATION //usr/local/share/template)
add_subdirectory(test)
