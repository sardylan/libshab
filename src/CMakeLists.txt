include_directories(.)

find_package(Qt5 REQUIRED COMPONENTS Core)

add_library(shab
        protocol/line.cpp
        protocol/line.hpp
        parser/line.cpp
        parser/line.hpp
        parser/exception.cpp
        parser/exception.hpp)

target_include_directories(shab PUBLIC ".")

target_link_libraries(shab
        Qt5::Core)

set_target_properties(shab
        PROPERTIES
        VERSION "${SHAB_LIBSHAB_VERSION}"
        SOVERSION "${SHAB_LIBSHAB_VERSION_MAJOR}.${SHAB_LIBSHAB_VERSION_MINOR}")

add_executable(chechsum16
        tool/checksum16.cpp)

target_link_libraries(chechsum16
        Qt5::Core
        shab)

install(TARGETS shab
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} COMPONENT libshab
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} COMPONENT libshab)

install(FILES
        protocol/line.hpp
        COMPONENT libshab
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/protocol/)

install(FILES
        parser/line.hpp
        parser/exception.hpp
        COMPONENT libshab
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/parser/)

install(TARGETS chechsum16
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} COMPONENT libshab)
