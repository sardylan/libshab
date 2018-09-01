cmake_minimum_required(VERSION 3.1)

project(libshab)

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

option(BUILD_SHARED_LIBS "Build the shared library" OFF)

add_subdirectory(src)
add_subdirectory(test)
