message("Configuration Started:")
message("--------------------------------------------")
project(ApolloMetricProcessing CXX C)
cmake_minimum_required(VERSION 2.6)
set(CMAKE_MODULE_PATH "${ApolloMetricProcessing_SOURCE_DIR}/CMakeModules;${CMAKE_MODULE_PATH}")

# Setting up RPATH
set( CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib" )

if(APPLE)
  set( CMAKE_INSTALL_NAME_DIR ${CMAKE_INSTALL_PREFIX}/lib )
endif(APPLE)

set( CMAKE_SKIP_RPATH                   FALSE CACHE BOOL "" )
set( CMAKE_SKIP_BUILD_RPATH             FALSE CACHE BOOL "" )
set( CMAKE_BUILD_WITH_INSTALL_RPATH     FALSE CACHE BOOL "" )
set( CMAKE_INSTALL_RPATH_USE_LINK_PATH  TRUE  CACHE BOOL "" )

mark_as_advanced(
  CMAKE_INSTALL_RPATH
  CMAKE_SKIP_RPATH
  CMAKE_SKIP_BUILD_RPATH
  CMAKE_BUILD_WITH_INSTALL_RPATH
  CMAKE_INSTALL_RPATH_USE_LINK_PATH
)

# Defining packages
find_package(Boost REQUIRED
  COMPONENTS program_options system thread filesystem)
find_package(VisionWorkbench REQUIRED
  COMPONENTS core image math fileio camera interestpoint)
find_package(LAPACK-eigen)

include_directories(
  ${Boost_INCLUDE_DIR}
  ${VisionWorkbench_INCLUDE_DIR}
  ${LAPACK_INCLUDE_DIR} )
link_directories(
  ${Boost_LIBRARY_DIRS}
  ${VisionWorkbench_LIBRARY_DIRS}
  ${LAPACK_LIBRARIES_DIR} )

# Subdirectories
add_subdirectory(src)

set(CMAKE_BUILD_TYPE Release)