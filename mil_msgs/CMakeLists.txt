cmake_minimum_required(VERSION 2.8.3)
project(mil_msgs)
find_package(catkin
  REQUIRED COMPONENTS
    message_generation
    message_runtime
    geometry_msgs
    sensor_msgs
    actionlib
    interactive_markers
    std_msgs
    actionlib_msgs
    roscpp
    rospy
    mil_tools
)

add_action_files(FILES
  MoveTo.action
  BagOnline.action
)

add_message_files(FILES
  PoseTwistStamped.msg
  PoseTwist.msg
  VelocityMeasurements.msg
  DepthStamped.msg
  RangeStamped.msg
  VelocityMeasurement.msg
  LabeledObject.msg
  LabeledObjects.msg
  PerceptionObject.msg
  PerceptionObjectArray.msg
  Point2D.msg
  ObjectInImage.msg
  ObjectsInImage.msg
)

add_service_files(FILES
  CameraToLidarTransform.srv
  SetGeometry.srv
  ObjectDBQuery.srv
)

generate_messages(
    DEPENDENCIES std_msgs actionlib_msgs geometry_msgs sensor_msgs
)
catkin_package(
    CATKIN_DEPENDS message_generation message_runtime geometry_msgs actionlib std_msgs actionlib_msgs
)

include_directories(include ${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})

add_executable(move_test src/move_test.cpp)

target_link_libraries(
  move_test
  ${catkin_LIBRARIES}
)

add_dependencies(
  move_test
  ${mil_msgs_EXPORTED_TARGETS}
)
