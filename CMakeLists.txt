cmake_minimum_required(VERSION 2.8.3)

include(cmake/HunterGate.cmake)
HunterGate(
  URL "https://github.com/ruslo/hunter/archive/v0.20.50.tar.gz"
  SHA1 "f119fdbbab3638472840464abb68b440ce5883da"
)

project(gencpp)

hunter_add_package(catkin)
hunter_add_package(ros_genmsg)

find_package(catkin REQUIRED COMPONENTS genmsg)

catkin_package(
  CATKIN_DEPENDS genmsg
  CFG_EXTRAS gencpp-extras.cmake
)

add_subdirectory(scripts)

file(WRITE ${CATKIN_DEVEL_PREFIX}/${GENMSG_LANGS_DESTINATION}/gencpp "C++")
install(FILES ${CATKIN_DEVEL_PREFIX}/${GENMSG_LANGS_DESTINATION}/gencpp
  DESTINATION ${GENMSG_LANGS_DESTINATION})

catkin_python_setup()
