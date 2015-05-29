cmake_minimum_required(VERSION 2.8.3)
project(mypkg)



## Find catkin and any catkin packages


find_package(catkin REQUIRED COMPONENTS 
    cv_bridge roscpp rospy sensor_msgs std_msgs image_transport genmsg message_filters pcl_ros tf
   )

FIND_PACKAGE(OpenCV REQUIRED) # tested on 2.3.1
FIND_PACKAGE(Qt4 COMPONENTS QtCore QtGui QtNetwork REQUIRED)


SET(INCLUDE_DIRS
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${OpenCV_INCLUDE_DIRS}
	${CMAKE_CURRENT_SOURCE_DIR}/../include
)

INCLUDE(${QT_USE_FILE})

SET(LIBRARIES
	${OpenCV_LIBS} 
	${QT_LIBRARIES} 
)


# Make sure the compiler can find include files from our library.
INCLUDE_DIRECTORIES(${INCLUDE_DIRS})
FIND_PACKAGE(Qt4 COMPONENTS QtCore QtGui QtNetwork REQUIRED)

## Generate added messages and services
generate_messages(DEPENDENCIES std_msgs)

## Declare a catkin package
catkin_package()

## Build talker and listener
include_directories(include ${catkin_INCLUDE_DIRS})

add_executable(Suscriber_Video src/Suscriber_Video.cpp)
target_link_libraries(Suscriber_Video ${catkin_LIBRARIES})

add_executable(Suscriber_findobject3d src/Suscriber_findobject3d.cpp)
target_link_libraries(Suscriber_findobject3d  ${catkin_LIBRARIES})
target_link_libraries(Suscriber_findobject3d  ${QT_LIBRARIES})
