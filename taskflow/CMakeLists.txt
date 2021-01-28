cmake_minimum_required(VERSION 3.5.0)
project(taskflow)

if (NOT INSTALL_TASKFLOW)
  find_package(Taskflow QUIET)
endif()

if (NOT Taskflow_FOUND OR INSTALL_TASKFLOW)
    # Taskflow requires 3.9
    if(${CMAKE_VERSION} VERSION_GREATER "3.8.99")

        if (NOT UPDATE_DISCONNECTED)
          set(UPDATE_DISCONNECTED ON)
        endif()

        # Taskflow tag can be overwritten using INSTALL_TASKFLOW_TAG
        if (NOT INSTALL_TASKFLOW_TAG)
            set(INSTALL_TASKFLOW_TAG v2.6.0)
        endif()

        include(ExternalProject)

        ExternalProject_Add(Taskflow
            GIT_REPOSITORY        https://github.com/taskflow/taskflow.git
            GIT_TAG               ${INSTALL_TASKFLOW_TAG}
            SOURCE_DIR            ${CMAKE_BINARY_DIR}/../tesseract_ext/Taskflow-src
            BINARY_DIR            ${CMAKE_BINARY_DIR}/../tesseract_ext/Taskflow-build
            UPDATE_DISCONNECTED   ${UPDATE_DISCONNECTED}
            CMAKE_CACHE_ARGS
            -DCMAKE_INSTALL_PREFIX:STRING=${CMAKE_INSTALL_PREFIX}
            -DCMAKE_BUILD_TYPE:STRING=Release
            -DCMAKE_EXPORT_NO_PACKAGE_REGISTRY:BOOL=ON
            -DTF_BUILD_BENCHMARKS:BOOL=OFF
            -DTF_BUILD_CUDA:BOOL=OFF
            -DTF_BUILD_TESTS:BOOL=OFF
            -DTF_BUILD_EXAMPLES:BOOL=OFF
            )

        install(FILES package.xml DESTINATION share/Taskflow)
    else()
        message(WARNING "Taskflow not found and could not be installed due to CMake version < 3.9.0")
        install(FILES package.xml DESTINATION share/dummy RENAME taskflow.xml)
    endif()
else()
    install(FILES package.xml DESTINATION share/dummy RENAME taskflow.xml)
endif()



