cmake_minimum_required(VERSION 3.5)

project(image_view_ros2)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(std_msgs REQUIRED)
find_package(OpenCV REQUIRED)

include_directories(include)
ament_export_include_directories(include)

# A stand alone node which consumes images and displays them using OpenCV.
add_executable(image_view_node
  src/image_view_node.cpp)
ament_target_dependencies(image_view_node
  "rclcpp"
  "sensor_msgs"
  "OpenCV")

install(TARGETS
  image_view_node
  DESTINATION lib/${PROJECT_NAME})

install(
  DIRECTORY include/
  DESTINATION include
)

ament_package()
