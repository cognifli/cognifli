# http://ros.org/doc/groovy/api/catkin/html/user_guide/supposed.html
cmake_minimum_required(VERSION 2.8.3)
project(cognifli_gazebo)
# Load catkin and all dependencies required for this package
find_package(catkin REQUIRED COMPONENTS gazebo_ros)


## DEPENDS: system dependencies of this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## INCLUDE_DIRS: 
## LIBRARIES: libraries you create in this project that dependent projects also need
catkin_package(
    DEPENDS 
    CATKIN_DEPENDS
    INCLUDE_DIRS 
    LIBRARIES
)
