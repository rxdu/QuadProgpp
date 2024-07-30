cmake_minimum_required(VERSION 3.16)

project(QuadProg++ CXX)

if (NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Build type (default Release)" FORCE)
endif ()

# This software may be modified and distributed under the terms
# of the MIT license.  See the LICENSE file for details.

add_library(quadprog STATIC src/Array.cc src/QuadProg++.cc)
set_property(TARGET quadprog PROPERTY POSITION_INDEPENDENT_CODE 1)
set_property(TARGET quadprog PROPERTY PUBLIC_HEADER ${headers})
target_include_directories(quadprog PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>)

add_executable(quadprog_sample src/main.cc)
target_link_libraries(quadprog_sample quadprog)

install(TARGETS quadprog
    EXPORT quadprog-targets
    RUNTIME DESTINATION bin
    PUBLIC_HEADER DESTINATION include/quadprog++
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib)

install(EXPORT quadprog-targets DESTINATION cmake)

