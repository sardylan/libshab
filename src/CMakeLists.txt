include_directories(.)

find_package(Qt5 REQUIRED COMPONENTS Core)

add_library(shab
        protocol/line.cpp
        protocol/line.hpp
        parser/line.cpp
        parser/line.hpp
        parser/exception.cpp
        parser/exception.hpp)

target_include_directories(shab PUBLIC .)

target_link_libraries(shab
        Qt5::Core)

set_target_properties(shab
        PROPERTIES
        VERSION ${SHAB_LIBSHAB_VERSION}
        SOVERSION ${SHAB_LIBSHAB_VERSION_MAJOR}.${SHAB_LIBSHAB_VERSION_MINOR})

add_executable(chechsum16
        tool/checksum16.cpp)

target_link_libraries(chechsum16
        Qt5::Core
        shab)
