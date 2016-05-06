cmake_minimum_required(VERSION 2.8.3)
project(gazebo_msgs)

include(CheckCXXCompilerFlag)
check_cxx_compiler_flag("-std=c++11" COMPILER_SUPPORTS_CXX11)
check_cxx_compiler_flag("-std=c++0x" COMPILER_SUPPORTS_CXX0x)
if(COMPILER_SUPPORTS_CXX11)
  set(CMAKE_CXX_FLAGS "-std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
  set(CMAKE_CXX_FLAGS "-std=c++0x")
else()
  message(FATAL_ERROR "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()

find_package(
  catkin REQUIRED COMPONENTS
    std_msgs
    trajectory_msgs
    geometry_msgs
    sensor_msgs
    std_srvs
    message_generation
)

add_message_files(
  DIRECTORY msg
  FILES
    ApplyJointEfforts.msg
    ContactsState.msg
    ContactState.msg
    LinkState.msg
    LinkStates.msg
    JointStates.msg
    ModelState.msg
    ModelStates.msg
    ODEJointProperties.msg
    ODEPhysics.msg
    WorldState.msg
)

add_service_files(
  DIRECTORY srv
  FILES
    AddForceSensor.srv
    AddJoint.srv
    AddLink.srv
    AddTorqueSensor.srv
    ApplyBodyWrench.srv
    DeleteModel.srv
    GetLinkState.srv
    GetPhysicsProperties.srv
    SetJointProperties.srv
    SetModelConfiguration.srv
    SpawnModel.srv
    ApplyJointEffort.srv
    GetJointProperties.srv
    GetModelProperties.srv
    GetWorldProperties.srv
    StartTimer.srv
    SetLinkProperties.srv
    SetModelState.srv
    BodyRequest.srv
    GetLinkProperties.srv
    GetModelState.srv
    JointRequest.srv
    SetLinkState.srv
    SetPhysicsProperties.srv
    SetJointTrajectory.srv
)

generate_messages(
  DEPENDENCIES
    std_msgs
    geometry_msgs
    sensor_msgs
    trajectory_msgs
)

catkin_package(
  CATKIN_DEPENDS
    message_runtime
    std_msgs
    trajectory_msgs
    geometry_msgs
    sensor_msgs
    std_srvs
    message_generation
)
