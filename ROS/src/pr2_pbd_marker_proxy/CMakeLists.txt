cmake_minimum_required(VERSION 2.8.3)
project(pr2_pbd_marker_proxy)

find_package(catkin REQUIRED COMPONENTS interactive_markers message_generation visualization_msgs)

include_directories(${catkin_INCLUDE_DIRS})

add_service_files(
FILES GetInit.srv)

generate_messages(
  DEPENDENCIES visualization_msgs std_msgs geometry_msgs
)

add_executable(${PROJECT_NAME} src/proxy.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})
add_dependencies(${PROJECT_NAME} ${PROJECT_NAME}_gencpp)
set_target_properties(${PROJECT_NAME}
  PROPERTIES OUTPUT_NAME proxy )

catkin_package(
    CATKIN_DEPENDS interactive_markers message_runtime visualization_msgs
)

install(TARGETS ${PROJECT_NAME}
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
