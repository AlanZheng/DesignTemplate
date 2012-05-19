cmake_minimum_required(VERSION 2.6)
 
PROJECT(DistanceBetweenPoints)
 
ADD_EXECUTABLE(DistanceBetweenPoints DistanceBetweenPoints.cxx)
INSTALL(TARGETS DistanceBetweenPoints DESTINATION distance)
 
SET(CPACK_GENERATOR "RPM")
SET(CPACK_DEBIAN_PACKAGE_MAINTAINER "David Doria") #required
 
INCLUDE(CPack)
 
# To use this:
# make package
# sudo dpkg -i DistanceBetweenPoints-0.1.1-Linux.deb
 
# This will result in the file:
#/usr/distance/DistanceBetweenPoints
