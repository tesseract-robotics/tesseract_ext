cmake_minimum_required(VERSION 3.5.0)

add_compile_options(-std=c++14 -w)

include(ExternalProject)

ExternalProject_Add(fcl
  GIT_REPOSITORY    https://github.com/flexible-collision-library/fcl.git
  GIT_TAG           master
  SOURCE_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/fcl-src
  BINARY_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/fcl-build
  CMAKE_CACHE_ARGS
          -DCMAKE_INSTALL_PREFIX:STRING=${CMAKE_INSTALL_PREFIX}
          -DCMAKE_BUILD_TYPE:STRING=Release
          -DFCL_BUILD_TESTS:BOOL=OFF
)

install(FILES package.xml DESTINATION share/fcl)
