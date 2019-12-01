cmake_minimum_required(VERSION 3.5.0)

add_compile_options(-std=c++14 -w)

include(ExternalProject)
ExternalProject_Add(libccd
  GIT_REPOSITORY    https://github.com/danfis/libccd.git
  GIT_TAG           master
  SOURCE_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/libccd-src
  BINARY_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/libccd-build
  CMAKE_CACHE_ARGS
          -DCMAKE_INSTALL_PREFIX:STRING=${CMAKE_INSTALL_PREFIX}
          -DCMAKE_BUILD_TYPE:STRING=Release
          -DENABLE_DOUBLE_PRECISION:BOOL=ON
)

install(FILES package.xml DESTINATION share/libccd)
