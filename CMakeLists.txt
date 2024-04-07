cmake_minimum_required(VERSION 3.8)
project(ros2_msgs)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

# Generate message and service sources
rosidl_generate_interfaces(${PROJECT_NAME}
  "srv/RequestResult.srv"
)

# Include Cpp "include" directory
include_directories(include)

# Create Cpp executable for each node
#add_executable(input_publisher src/input_publisher_node.cpp)
#ament_target_dependencies(input_publisher rclcpp std_msgs)

#add_executable(output_subscriber src/output_subscriber_node.cpp)
#ament_target_dependencies(output_subscriber rclcpp std_msgs)

# Install Cpp executables
install(TARGETS
  DESTINATION lib/${PROJECT_NAME}
)

# Install launch files
install(FILES
  DESTINATION share/${PROJECT_NAME}/
)

ament_export_dependencies(ament_cmake)
ament_export_dependencies(rclcpp)
ament_export_dependencies(std_msgs)
ament_export_dependencies(rosidl_default_generators)

ament_package()