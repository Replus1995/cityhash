cmake_minimum_required(VERSION 3.19.0)
project(cityhash)

configure_file("config.h.in" "${CMAKE_CURRENT_BINARY_DIR}/gen/config.h" @ONLY)
add_library(cityhash 
STATIC 
	"src/city.cc"
)

target_include_directories(cityhash 
PUBLIC 
	"src"
	"${CMAKE_CURRENT_BINARY_DIR}/gen"
)

if(ANDROID)
    find_package(STL REQUIRED)
    target_link_libraries(cityhash STL::Lib)
endif()