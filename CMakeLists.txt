cmake_minimum_required(VERSION 2.8.3)
project(nao_pose_controller)

set(CMAKE_CXX_FLAGS "-std=gnu++0x ${CMAKE_CXX_FLAGS}")

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  naoqi_msgs
  roscpp
  tf
  actionlib
  std_srvs
  std_msgs
  move_base_msgs
  nav_msgs
)

catkin_package(
    INCLUDE_DIRS include
    CATKIN_DEPENDS geometry_msgs roscpp tf naoqi_msgs std_srvs actionlib move_base_msgs nav_msgs std_msgs
)

include_directories(
    include
    ${catkin_INCLUDE_DIRS}
    ${Boost_INCLUDE_DIRS}
)

set(NAOPOSECONTROLLER_SOURCES
  src/nao_pose_controller_node.cpp
  src/nao_pose_controller.cpp
)


add_executable(nao_pose_controller ${NAOPOSECONTROLLER_SOURCES})
target_link_libraries(nao_pose_controller     
   ${catkin_LIBRARIES}
   ${Boost_LIBRARIES}
)

add_dependencies(nao_pose_controller ${catkin_EXPORTED_TARGETS})

install(TARGETS nao_pose_controller
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)