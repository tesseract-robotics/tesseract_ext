cmake_minimum_required(VERSION 3.5.0)

find_package(Benchmark QUIET)
if ( NOT Benchmark_FOUND )

  include(ExternalProject)

  if (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    set(BENCHMARK_CXX_FLAGS "-w -std=c++14")
    set(BENCHMARK_C_FLAGS "-w")

    ExternalProject_Add(Benchmark
      GIT_REPOSITORY    https://github.com/google/benchmark.git
      GIT_TAG           v1.5.0
      SOURCE_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/benchmark-src
      BINARY_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/benchmark-build
      CMAKE_CACHE_ARGS
              -DCMAKE_INSTALL_PREFIX:STRING=${CMAKE_INSTALL_PREFIX}
              -DCMAKE_BUILD_TYPE:STRING=Release
              -DCMAKE_CXX_FLAGS:STRING=${BENCHMARK_CXX_FLAGS}
              -DCMAKE_C_FLAGS:STRING=${BENCHMARK_C_FLAGS}
              -DBENCHMARK_ENABLE_GTEST_TESTS:Bool=OFF
    )
  elseif (CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
    ExternalProject_Add(Benchmark
      GIT_REPOSITORY    https://github.com/google/benchmark.git
      GIT_TAG           v1.5.0
      SOURCE_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/benchmark-src
      BINARY_DIR        ${CMAKE_BINARY_DIR}/../tesseract_ext/benchmark-build
      CMAKE_CACHE_ARGS
              -DCMAKE_INSTALL_PREFIX:STRING=${CMAKE_INSTALL_PREFIX}
              -DCMAKE_BUILD_TYPE:STRING=Release
              -DBENCHMARK_ENABLE_GTEST_TESTS:Bool=OFF
    )
  endif()

  install(FILES package.xml DESTINATION share/benchmark)
else()
  install(FILES package.xml DESTINATION share/dummy RENAME benchmark.xml)
endif()


