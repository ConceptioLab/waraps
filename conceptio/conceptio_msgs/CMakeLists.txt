cmake_minimum_required(VERSION 3.5)
project(conceptio_msgs)

find_package(ament_cmake_ros REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

rosidl_generate_interfaces(${PROJECT_NAME}
  msg/Utm.msg
  msg/Remoteid.msg
  msg/CapellaPropertyValue.msg
  msg/CapellaTrigger.msg
)

ament_export_dependencies(rosidl_default_runtime)

ament_package()
