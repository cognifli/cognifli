cmake_minimum_required(VERSION 2.8.3)
project(snapflight)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
set(CMAKE_BUILD_TYPE Release)

find_package(catkin REQUIRED COMPONENTS 
	roscpp
	sensor_msgs
	geometry_msgs
	mavros_msgs
)


set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

catkin_package(
  #INCLUDE_DIRS include
  #LIBRARIES mavros
  CATKIN_DEPENDS roscpp mavros_msgs geometry_msgs
)

include_directories(
	${catkin_INCLUDE_DIRS}
)

add_executable(snapflight main.cpp)
add_dependencies(snapflight mavros_msgs)
add_dependencies(snapflight mavros_msgs_generate_messages_cpp)
add_dependencies(snapflight geometry_msgs_generate_messages_cpp)

target_link_libraries(snapflight
  ${catkin_LIBRARIES}
)
