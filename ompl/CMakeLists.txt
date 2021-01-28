cmake_minimum_required(VERSION 3.5.0)
project(ompl)

if (NOT INSTALL_OMPL)
  find_package(ompl QUIET)
endif()

if (NOT ompl_FOUND OR INSTALL_OMPL)

  if (NOT UPDATE_DISCONNECTED)
    set(UPDATE_DISCONNECTED ON)
  endif()

  if (NOT INSTALL_OMPL_TAG)
    set(INSTALL_OMPL_TAG "1.5.0")
  endif()

  include(ExternalProject)

  ExternalProject_Add(ompl
    GIT_REPOSITORY        https://github.com/ompl/ompl.git
    GIT_TAG               ${INSTALL_OMPL_TAG}
    SOURCE_DIR            ${CMAKE_BINARY_DIR}/../tesseract_ext/ompl-src
    BINARY_DIR            ${CMAKE_BINARY_DIR}/../tesseract_ext/ompl-build
    UPDATE_DISCONNECTED   ${UPDATE_DISCONNECTED}
    CMAKE_CACHE_ARGS
            -DCMAKE_INSTALL_PREFIX:STRING=${CMAKE_INSTALL_PREFIX}
            -DCMAKE_BUILD_TYPE:STRING=Release
            -D_USE_MATH_DEFINES:BOOL=ON
            -DOMPL_BUILD_DEMOS:BOOL=OFF
            -DOMPL_BUILD_TESTS:BOOL=OFF
            -DOMPL_REGISTRATION:BOOL=OFF
  )

  install(FILES package.xml DESTINATION share/ompl)
else()
  install(FILES package.xml DESTINATION share/dummy RENAME ompl.xml)
endif()

