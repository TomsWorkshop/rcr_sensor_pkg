cmake_minimum_required(VERSION 2.8.3)
project(imu_sensor)

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  rospy
  std_msgs
)

catkin_package(
  # INCLUDE_DIRS include
  CATKIN_DEPENDS 
    geometry_msgs
    std_msgs
)

###########
## Build ##
###########

include_directories(
  # include
  # ${catkin_INCLUDE_DIRS}
)

#############
## Install ##
#############

set(PYTHON_SCRIPTS
  scripts/mpu6050.py
)

foreach(scripts ${PYTHON_SCRIPTS})
  catkin_install_python(PROGRAMS ${scripts}
    DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
endforeach()

#############
## Testing ##
#############

if (CATKIN_ENABLE_TESTING)
  find_package(roslaunch REQUIRED)

  set(DIRECTORIES
    ./launch/
    )

  foreach(dirs ${DIRECTORIES})
    roslaunch_add_file_check(${dirs})
  endforeach()
endif()
