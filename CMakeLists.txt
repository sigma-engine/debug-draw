cmake_minimum_required(VERSION 3.5)
project(debug-draw VERSION 2.0.0 LANGUAGES CXX)

add_library(debug-draw debug_draw.cpp)
add_library(debug-draw::debug-draw ALIAS debug-draw)

target_include_directories(debug-draw PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")

include(GNUInstallDirs)
set(INSTALL_CONFIGDIR ${CMAKE_INSTALL_LIBDIR}/cmake/debug-draw)

install(TARGETS debug-draw
    EXPORT debug-draw-targets
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

install(FILE include/debug_draw.hpp DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

install(EXPORT debug-draw-targets
  FILE
    debug-drawTargets.cmake
  NAMESPACE
    debug-draw::
  DESTINATION
    ${INSTALL_CONFIGDIR}
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    ${CMAKE_CURRENT_BINARY_DIR}/debug-drawConfigVersion.cmake
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY AnyNewerVersion
)

configure_package_config_file(${CMAKE_CURRENT_LIST_DIR}/cmake/debug-drawConfig.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/debug-drawConfig.cmake
    INSTALL_DESTINATION ${INSTALL_CONFIGDIR}
)

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/debug-drawConfig.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/debug-drawConfigVersion.cmake
    DESTINATION ${INSTALL_CONFIGDIR}
)

export(EXPORT debug-draw-targets FILE ${CMAKE_CURRENT_BINARY_DIR}/debug-drawTargets.cmake NAMESPACE debug-draw::)

export(PACKAGE debug-draw)
