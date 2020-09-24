# tesseract_ext
[![Build Status](https://travis-ci.com/ros-industrial-consortium/tesseract_ext.svg?branch=master)](https://travis-ci.com/ros-industrial-consortium/tesseract_ext)

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
