cmake_minimum_required(VERSION 3.5.0)
project(orocos_kdl)

find_package(orocos_kdl QUIET)
if (NOT orocos_kdl_FOUND OR INSTALL_OROCOS_KDL)
  if (NOT INSTALL_OROCOS_KDL_TAG)
    set(INSTALL_OROCOS_KDL_TAG "1.3.2")
  endif()

  include(ExternalProject)

  ExternalProject_Add(orocos_kdl
    GIT_REPOSITORY    https://github.com/orocos/orocos_kinematics_dynamics.git
    GIT_TAG           ${INSTALL_OROCOS_KDL_TAG}
    GIT_SHALLOW       ON
    SOURCE_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/orocos_kdl-src
    BINARY_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/orocos_kdl-build
    SOURCE_SUBDIR     orocos_kdl
    CMAKE_CACHE_ARGS
            -DCMAKE_INSTALL_PREFIX:STRING=${CMAKE_INSTALL_PREFIX}
            -DCMAKE_BUILD_TYPE:STRING=Release
  )
endif()

install(FILES package.xml DESTINATION share/orocos_kdl)