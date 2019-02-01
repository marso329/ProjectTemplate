cmake_minimum_required (VERSION 3.9.1)

project (Template VERSION 0.0.1 DESCRIPTION "Template project")

set(CMAKE_BUILD_TYPE Release)

include(GNUInstallDirs)

#All gcc/icc flags, feel free to add flags if necessary
set (CMAKE_CXX_FLAGS "-std=c++17 -O3 ")

#All warning flags, yes we are pedantic
#the reason why -Wstrict-overflow=2 and not -Wstrict-overflow=5 is because of a bug in boost::python
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Werror -Wall -Wextra -pedantic -Wno-undef -Wcast-align -Wcast-qual -Wctor-dtor-privacy -Wdisabled-optimization -Wformat=2 -Winit-self -Wlogical-op -Wmissing-include-dirs -Wnoexcept -Wold-style-cast -Woverloaded-virtual -Wredundant-decls -Wshadow -Wsign-promo -Wstrict-null-sentinel -Wstrict-overflow=2 -Wundef -Wno-unused -Wno-variadic-macros -Wno-parentheses -fdiagnostics-show-option")

#All libraries that must be linked
#set (CMAKE_SHARED_LINKER_FLAGS "-lboost_serialization -lboost_log -lboost_log_setup -lboost_thread  -lboost_system -lrt -lpthread")

#I like the output files to end up in .lib
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin)

add_library(Template SHARED
    src/template.cxx 
)


set_target_properties(Template PROPERTIES VERSION ${PROJECT_VERSION})

#Not needed but libTemplate.so.1 will symlink to libTemplate.so.0.0.1
set_target_properties(Template PROPERTIES SOVERSION 1)

set_target_properties(Template PROPERTIES PUBLIC_HEADER "include/template.h")

#include directory
target_include_directories(Template PUBLIC include)

#Src directory
target_include_directories(Template PUBLIC src)


#Rules on how to install it
install(TARGETS Template
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

add_subdirectory(test)