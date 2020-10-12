# tesseract_ext

Platform             | CI Status
---------------------|:---------
Linux (Focal)        | [![Build Status](https://github.com/ros-industrial-consortium/tesseract_ext/workflows/Focal-Build/badge.svg)](https://github.com/ros-industrial-consortium/tesseract_ext/actions)
Linux (Bionic)       | [![Build Status](https://github.com/ros-industrial-consortium/tesseract_ext/workflows/Bionic-Build/badge.svg)](https://github.com/ros-industrial-consortium/tesseract_ext/actions)
Linux (Bionic,Clang) | [![Build Status](https://github.com/ros-industrial-consortium/tesseract_ext/workflows/Bionic-Clang-Build/badge.svg)](https://github.com/ros-industrial-consortium/tesseract_ext/actions)
Linux (Xenial)       | [![Build Status](https://github.com/ros-industrial-consortium/tesseract_ext/workflows/Xenial-Build/badge.svg)](https://github.com/ros-industrial-consortium/tesseract_ext/actions)
Windows              | [![Build Status](https://github.com/ros-industrial-consortium/tesseract_ext/workflows/Windows-Build/badge.svg)](https://github.com/ros-industrial-consortium/tesseract_ext/actions)


This contains external dependencies for Tesseract.

Building this repo for the first time will require internet (to pull the necessary repositories). After that, internet will only be required if the downloaded source code is deleted (it is in build/tesseract_ext). If it is desired that cmake check for updated versions of the packages, the flag UPDATE_DISCONNECTED may be set to OFF (it defaults to ON) with `catkin build --force-cmake --cmake-args -DUPDATE_DISCONNECTED=OFF`.

## Required Dependencies
* Bullet3
* FCL
* GTest
* libcdd
* SWIG
* Taskflow

## Optional Dependencies
These are optional and not required for typical operation
* Eigen3 - Bug fixes that are not available in release version are useful in some cases
  * Enable with `-DINSTALL_EIGEN=ON`
  * Select custom git tag with `-DINSTALL_EIGEN_TAG=tag_name`
* Orocos_kdl - Must be built from source when using a custom Eigen version
  * Enable with `-DINSTALL_OROCOS_KDL=ON`
  * Select custom git tag with `-DINSTALL_OROCOS_KDL_TAG=tag_name`
