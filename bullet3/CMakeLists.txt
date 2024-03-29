cmake_minimum_required(VERSION 3.5.0)

include(ExternalProject)

if (NOT UPDATE_DISCONNECTED)
  set(UPDATE_DISCONNECTED ON)
endif()

if (NOT INSTALL_BULLET)
  find_package(Bullet QUIET CONFIGS BulletConfig-float64.cmake BulletConfig.cmake)
endif()

if(NOT Bullet_FOUND OR NOT ${BULLET_DEFINITIONS} MATCHES ".*-DBT_USE_DOUBLE_PRECISION.*" OR Bullet_VERSION VERSION_LESS "2.89" OR INSTALL_BULLET)
  if (CMAKE_CXX_COMPILER_ID STREQUAL "GNU" OR CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    set(BULLET_CXX_FLAGS "-w -std=c++14")
    set(BULLET_C_FLAGS "-w")

    ExternalProject_Add(Bullet
      GIT_REPOSITORY        https://github.com/bulletphysics/bullet3.git
      GIT_TAG               master
      SOURCE_DIR            ${CMAKE_BINARY_DIR}/../tesseract_ext/bullet3-src
      BINARY_DIR            ${CMAKE_BINARY_DIR}/../tesseract_ext/bullet3-build
      UPDATE_DISCONNECTED   ${UPDATE_DISCONNECTED}
      CMAKE_CACHE_ARGS
              -DCMAKE_INSTALL_PREFIX:STRING=${CMAKE_INSTALL_PREFIX}
              -DCMAKE_BUILD_TYPE:STRING=Release
              -DCMAKE_CXX_FLAGS:STRING=${BULLET_CXX_FLAGS}
              -DCMAKE_C_FLAGS:STRING=${BULLET_C_FLAGS}
              -DBUILD_UNIT_TESTS:BOOL=OFF
              -DBUILD_SHARED_LIBS:BOOL=ON
              -DBULLET2_MULTITHREADING:BOOL=ON
              -DUSE_DOUBLE_PRECISION:BOOL=ON
              -DBUILD_CPU_DEMOS:BOOL=OFF
              -DBUILD_BULLET2_DEMOS:BOOL=OFF
              -DBUILD_BULLET_ROBOTICS_GUI_EXTRA:BOOL=OFF
              -DBUILD_BULLET_ROBOTICS_EXTRA:BOOL=OFF
              -DBUILD_INVERSE_DYNAMIC_EXTRA:BOOL=OFF
              -DBUILD_OBJ2SDF_EXTRA:BOOL=OFF
              -DBUILD_SERIALIZE_EXTRA:BOOL=OFF
              -DBUILD_OPENGL3_DEMOS:BOOL=OFF
    )
  elseif(CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
    ExternalProject_Add(Bullet
      GIT_REPOSITORY        https://github.com/bulletphysics/bullet3.git
      GIT_TAG               master
      SOURCE_DIR            ${CMAKE_BINARY_DIR}/../tesseract_ext/bullet3-src
      BINARY_DIR            ${CMAKE_BINARY_DIR}/../tesseract_ext/bullet3-build
      UPDATE_DISCONNECTED   ${UPDATE_DISCONNECTED}
      CMAKE_CACHE_ARGS
              -DCMAKE_INSTALL_PREFIX:STRING=${CMAKE_INSTALL_PREFIX}
              -DCMAKE_BUILD_TYPE:STRING=Release
              -DBUILD_UNIT_TESTS:BOOL=OFF
              -DBULLET2_MULTITHREADING:BOOL=ON
              -DUSE_MSVC_RUNTIME_LIBRARY_DLL:BOOL=ON
              -DINSTALL_LIBS:BOOL=ON
              -DUSE_DOUBLE_PRECISION:BOOL=ON
              -DUSE_MSVC_DISABLE_RTTI:BOOL=OFF
              -DBUILD_CPU_DEMOS:BOOL=OFF
              -DBUILD_BULLET2_DEMOS:BOOL=OFF
              -DBUILD_BULLET_ROBOTICS_GUI_EXTRA:BOOL=OFF
              -DBUILD_BULLET_ROBOTICS_EXTRA:BOOL=OFF
              -DBUILD_INVERSE_DYNAMIC_EXTRA:BOOL=OFF
              -DBUILD_OBJ2SDF_EXTRA:BOOL=OFF
              -DBUILD_SERIALIZE_EXTRA:BOOL=OFF
              -DBUILD_OPENGL3_DEMOS:BOOL=OFF
    )
  endif()

  install(FILES package.xml DESTINATION share/bullet3)
else()
  install(FILES package.xml DESTINATION share/dummy RENAME bullet.xml)
endif()

