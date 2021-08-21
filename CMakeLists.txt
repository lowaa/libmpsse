cmake_minimum_required(VERSION 3.13)

project(libmpsse)

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
find_package(libftdi1 REQUIRED)

add_compile_definitions(LIBFTDI=1)

add_library(${PROJECT_NAME} STATIC)
add_library(${PROJECT_NAME}::framework ALIAS ${PROJECT_NAME})

# Includes ---------------------------------------------------------------------
#include(GNUInstallDirs)
#include(CMakePackageConfigHelpers)

target_include_directories(${PROJECT_NAME}
        PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
        )

target_sources(${PROJECT_NAME}
        PRIVATE
        src/mpsse.c
        src/support.c
        src/fast.c
        )

message("FTDI params ${LIBFTDI_INCLUDE_DIR} ${LIBFTDI_LIBRARIES}")
include_directories(${PROJECT_NAME} ${LIBFTDI_INCLUDE_DIR})
target_link_libraries(${PROJECT_NAME} ${LIBFTDI_LIBRARIES})
