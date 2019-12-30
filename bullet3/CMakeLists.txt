cmake_minimum_required(VERSION 3.5.0)

include(ExternalProject)

set(BULLET_CXX_FLAGS "-w -std=c++14")
set(BULLET_C_FLAGS "-w")

ExternalProject_Add(Bullet
  GIT_REPOSITORY    https://github.com/bulletphysics/bullet3.git
  GIT_TAG           master
  SOURCE_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/bullet3-src
  BINARY_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/bullet3-build
  CMAKE_CACHE_ARGS
          -DCMAKE_INSTALL_PREFIX:STRING=${CMAKE_INSTALL_PREFIX}
          -DCMAKE_BUILD_TYPE:STRING=Release
          -DCMAKE_CXX_FLAGS:STRING=${BULLET_CXX_FLAGS}
          -DCMAKE_C_FLAGS:STRING=${BULLET_C_FLAGS}
          -DBUILD_UNIT_TESTS:BOOL=OFF
          -DBUILD_SHARED_LIBS:BOOL=ON
          -DBULLET2_MULTITHREADING:BOOL=ON
          -DUSE_MSVC_RUNTIME_LIBRARY_DLL:BOOL=ON
)

install(FILES package.xml DESTINATION share/bullet3)
