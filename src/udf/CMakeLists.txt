project(libUDF)
cmake_minimum_required(VERSION 2.8)
enable_language(CXX)

set_property(GLOBAL PROPERTY RULE_MESSAGES OFF)

set (CMAKE_CXX_STANDARD 14)

set(CMAKE_SHARED_LIBRARY_SUFFIX ".so")

#set(CMAKE_VERBOSE_MAKEFILE on)

set (CMAKE_CXX_STANDARD 14)

set(NEKRS_INSTALL_DIR $ENV{NEKRS_INSTALL_DIR})
set(OGSDIR      ${NEKRS_INSTALL_DIR}/gatherScatter)
set(GSDIR       ${NEKRS_INSTALL_DIR}/gslib)
set(CDSDIR      ${NEKRS_INSTALL_DIR}/cds)
set(INCLUDE_DIRS
  ${CMAKE_CURRENT_SOURCE_DIR}/../..
  ${CDSDIR}
  ${OGSDIR}
  ${GSDIR}
  ${NEKRS_INSTALL_DIR}
  ${NEKRS_INSTALL_DIR}/include
  ${NEKRS_INSTALL_DIR}/include/mesh
  ${NEKRS_INSTALL_DIR}/include/io
  ${NEKRS_INSTALL_DIR}/include/core
  ${NEKRS_INSTALL_DIR}/include/core/utils
  ${NEKRS_INSTALL_DIR}/include/timeStepper
  ${NEKRS_INSTALL_DIR}/include/udf
  ${NEKRS_INSTALL_DIR}/include/lns
  ${NEKRS_INSTALL_DIR}/include/elliptic
  ${NEKRS_INSTALL_DIR}/include/elliptic/parAlmond
  ${NEKRS_INSTALL_DIR}/include/nekInterface
  ${NEKRS_INSTALL_DIR}/include/cds
  ${NEKRS_INSTALL_DIR}/include/linAlg
  ${NEKRS_INSTALL_DIR}/occa/include
)

add_library(UDF SHARED udf.cpp)
target_include_directories(UDF PRIVATE ${INCLUDE_DIRS} ${UDF_DIR})

if(APPLE)
    target_link_libraries(UDF "-Wl,-undefined -Wl,dynamic_lookup")
endif()
set_target_properties(UDF PROPERTIES LINKER_LANGUAGE CXX)
