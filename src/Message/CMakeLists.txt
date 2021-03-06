#//////////////////////////////////////////////////////////////////////////////////////
#// This file is distributed under the University of Illinois/NCSA Open Source License.
#// See LICENSE file in top directory for details.
#//
#// Copyright (c) 2020 QMCPACK developers.
#//
#// File developed by: Ye Luo, yeluo@anl.gov, Argonne National Laboratory
#//
#// File created by: Ye Luo, yeluo@anl.gov, Argonne National Laboratory
#//////////////////////////////////////////////////////////////////////////////////////


SET(COMM_SRCS
  Communicate.cpp
  AppAbort.cpp
  MPIObjectBase.cpp
)

ADD_LIBRARY(message ${COMM_SRCS})
TARGET_LINK_LIBRARIES(message PUBLIC platform_host)

IF(HAVE_MPI)
  TARGET_LINK_LIBRARIES(message PUBLIC MPI::MPI_CXX Boost::boost)
  SET_PROPERTY(TARGET message APPEND PROPERTY INCLUDE_DIRECTORIES "${qmcpack_SOURCE_DIR}/external_codes/mpi_wrapper")
  SET_PROPERTY(TARGET message APPEND PROPERTY INTERFACE_INCLUDE_DIRECTORIES "${qmcpack_SOURCE_DIR}/external_codes/mpi_wrapper")
ENDIF()


ADD_LIBRARY(catch_main catch_main.cpp)
TARGET_INCLUDE_DIRECTORIES(catch_main PUBLIC "${PROJECT_SOURCE_DIR}/external_codes/catch")
TARGET_LINK_LIBRARIES(catch_main message)
