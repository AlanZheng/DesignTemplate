cmake_minimum_required(VERSION 2.8)

# project name
set(PROJECT_NAME_STR cmake_example)
project(${PROJECT_NAME_STR})

# compile flags
SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb -std=c++0x")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")

# compile type
SET(CMAKE_BUILD_TYPE Debug)

# don't compile project in source path
if(${CMAKE_SOURCE_DIR} STREQUAL ${CMAKE_BINARY_DIR})
	if(NOT DEFINED WITH_IN_SOURCE_BUILD)
		message(FATAL_ERROR
			"CMake generation for project is not allowed within the source directory!"
			"\n Remove the CMakeCache.txt file and try again from another folder, e.g.:"
			"\n "
			"\n rm CMakeCache.txt"
			"\n cd .."
			"\n mkdir build"
			"\n cd build"
			"\n cmake .."
			"\n "
			"\n Alternately define WITH_IN_SOURCE_BUILD to force this option (not recommended!)"
		)
	endif()
endif()

# Redirect output files
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin CACHE INTERNAL "" FORCE )
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/lib CACHE INTERNAL "" FORCE )

set(GTEST_LIBRARY ${PROJECT_SOURCE_DIR}/../../googletest-svn/build-aux)
set(GTEST_MAIN_LIBRARY ${PROJECT_SOURCE_DIR}/../../googletest-svn/build-aux)
set(GTEST_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/../../googletest-svn/include)

add_definitions(-Wall -pthread)

set(COMMON_INCLUDES ${PROJECT_SOURCE_DIR}/include ${PROJECT_SOURCE_DIR}/../../googletest-svn/include)

#enable_testing()

add_subdirectory(src)
add_subdirectory(src_test)

#INSTALL(TARGETS bin/* DESTINATION ${PROJECT_NAME_STR})
 
SET(CPACK_GENERATOR "RPM")
SET(CPACK_DEBIAN_PACKAGE_MAINTAINER "Alan Zheng") #required
 
INCLUDE(CPack)
