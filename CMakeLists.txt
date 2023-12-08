cmake_minimum_required(VERSION 3.16)
project(cutienotification VERSION 0.1 LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(Qt6 REQUIRED COMPONENTS Core Quick DBus)
qt_standard_project_setup()

set(lib_SOURCES
    src/cutienotification.h
    src/cutienotification.cpp)

qt6_add_library(cutienotification
    SHARED ${lib_SOURCES}
)

set_target_properties(cutienotification PROPERTIES VERSION ${PROJECT_VERSION})
set_target_properties(cutienotification PROPERTIES SOVERSION 0)
set_target_properties(cutienotification PROPERTIES PUBLIC_HEADER src/cutienotification.h)

target_link_libraries(cutienotification PUBLIC
    Qt::Core
    Qt::Quick
    Qt::DBus
)

configure_file(src/cutienotification.pc.in cutienotification.pc @ONLY)

install(TARGETS cutienotification
    RUNTIME DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    BUNDLE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    PUBLIC_HEADER DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}")

install(FILES ${CMAKE_BINARY_DIR}/cutienotification.pc DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)
