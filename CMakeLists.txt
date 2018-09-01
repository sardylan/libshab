cmake_minimum_required(VERSION 3.1)

project(libshab)

include(GNUInstallDirs)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

set(QT5_PREFIX "$ENV{QTDIR}" CACHE PATH "Qt5 prefix path")

find_program(QT5_QMAKE_BIN
        qmake
        PATHS "${QT5_PREFIX}/bin"
        NO_CMAKE_PATH
        NO_CMAKE_ENVIRONMENT_PATH
        NO_SYSTEM_ENVIRONMENT_PATH
        NO_CMAKE_SYSTEM_PATH)

if (NOT QT5_QMAKE_BIN)
    message(FATAL_ERROR "Wrong Qt5 directory: ${QT5_PREFIX}")
endif ()

message(STATUS "Qt5 directory: ${QT5_PREFIX}")

set(CMAKE_PREFIX_PATH "${QT5_PREFIX}/lib/cmake")

set(SHAB_LIBSHAB_NAME "SHAB Server")

set(SHAB_LIBSHAB_VERSION_MAJOR "1")
set(SHAB_LIBSHAB_VERSION_MINOR "0")
set(SHAB_LIBSHAB_VERSION_BUGFIX "0")

set(SHAB_LIBSHAB_ORGANIZATION_NAME "The HellNet.org")
set(SHAB_LIBSHAB_ORGANIZATION_DOMAIN "thehellnet.org")

set(SHAB_LIBSHAB_VERSION "${SHAB_LIBSHAB_VERSION_MAJOR}.${SHAB_LIBSHAB_VERSION_MINOR}.${SHAB_LIBSHAB_VERSION_BUGFIX}")

message(STATUS "Version: ${SHAB_LIBSHAB_VERSION}")

if (NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Choose the type of build." FORCE)
    set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "MinSizeRel" "RelWithDebInfo")
endif ()

message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")

option(libshab_BUILD_SHARED_LIBS "Build libshab as a shared library" ON)
set(BUILD_SHARED_LIBS ${libshab_BUILD_SHARED_LIBS})
message(STATUS "Build libshab as a shared library: ${BUILD_SHARED_LIBS}")

message(STATUS "Install root: ${CMAKE_INSTALL_PREFIX}")

add_subdirectory(src)
add_subdirectory(test)
