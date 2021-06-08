cmake_minimum_required(VERSION 2.8.3)
project(abseil_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(ExternalProject)

set(VERSION d902eb869bcfacc1bad14933ed9af4bed006d481)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)

ExternalProject_Add(abseil-cpp
  GIT_REPOSITORY https://github.com/abseil/abseil-cpp.git
  GIT_TAG ${VERSION}
  UPDATE_COMMAND ""
  CMAKE_ARGS
    -G Ninja
    -DCMAKE_BUILD_TYPE:STRING=Release
    -DCMAKE_POSITION_INDEPENDENT_CODE=ON
    -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX} -DBUILD_SHARED_LIBS=ON
  ../abseil-cpp
  BUILD_COMMAND make -j8
  INSTALL_COMMAND make install -j8
)

cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include)
cs_install()
