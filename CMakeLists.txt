cmake_minimum_required (VERSION 2.8.12)
set(CMAKE_BUILD_TYPE RELEASE)
set(ENV{XENOMAI_ROOT_DIR} /usr/xenomai)

# Needed Modules
include(CMakePackageConfigHelpers)
include(FindPkgConfig)
include(${PROJECT_SOURCE_DIR}/cmake-modules/CMakeFunctions.cmake)

# Set policy for LINK_INTERFACE
cmake_policy(SET CMP0022 NEW)
set( EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/build/bin )
set( LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib )
set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake-modules)

############### dependencies ##################################

#common commands for building c++ executables and libraries
find_package(Xenomai)
include_directories( ${Xenomai_NATIVE_INCLUDE_DIRS} )
message(STATUS "xenomai path: ${Xenomai_NATIVE_INCLUDE_DIRS}")
link_directories(
    /usr/xenomai/lib
)

find_package(soem)
include_directories( ${soem_INCLUDE_DIRS} )
message(STATUS "soem path: ${soem_INCLUDE_DIRS}")
set(LIB_XENOMAI 
    ${Xenomai_NATIVE_DL_FLAGS}
    ${soem_LIBRARIES}
)

############### source and test ######################
include_directories( ${PROJECT_SOURCE_DIR}/include )
add_subdirectory(src ${EXECUTABLE_OUTPUT_PATH})
######################################################
