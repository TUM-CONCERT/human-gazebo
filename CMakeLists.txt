cmake_minimum_required(VERSION 3.0.2)
project(human-gazebo)

## Add support for C++17, supported in ROS Kinetic and newer
add_definitions(-std=c++17)

find_package(catkin REQUIRED COMPONENTS
  roscpp  
  std_msgs
  geometry_msgs
  concert_msgs
  gazebo_ros
)

find_package(LibXml2 REQUIRED)
include_directories(${LIBXML2_INCLUDE_DIR})

find_package(Eigen3 REQUIRED)
include_directories(${EIGEN3_INCLUDE_DIRS})

find_package(gazebo REQUIRED)
link_directories(${GAZEBO_LIBRARY_DIRS})
include_directories(
  includes
  ${Boost_INCLUDE_DIR} 
  ${catkin_INCLUDE_DIRS} 
  ${GAZEBO_INCLUDE_DIRS}
)

#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GAZEBO_CXX_FLAGS}")

catkin_package(
  #INCLUDE_DIRS ${GAZEBO_INCLUDE_DIRS}
  #LIBRARIES obstacles ${GAZEBO_LIBRARY_DIRS}
  CATKIN_DEPENDS geometry_msgs roscpp std_msgs concert_msgs
  DEPENDS gazebo_ros system_lib
)

add_library(motion_capture SHARED includes/human-gazebo/motion_capture.h includes/human-gazebo/skeleton_node.h
    src/motion_capture.cc)
add_dependencies(motion_capture ${catkin_EXPORTED_TARGETS})
target_link_libraries(motion_capture ${catkin_LIBRARIES} ${GAZEBO_LIBRARIES} ${LIBXML2_LIBRARIES})