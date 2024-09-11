cmake_minimum_required(VERSION 3.27)
project(variant VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(variant INTERFACE)

target_include_directories(variant
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include/variant>
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/variantConfig.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/variantConfig.cmake"
  INSTALL_DESTINATION share/variant
)

install(TARGETS variant
  EXPORT variantTargets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY
  "${CMAKE_CURRENT_SOURCE_DIR}/include/mapbox"
  DESTINATION include/variant
)

install(
  EXPORT variantTargets
  DESTINATION share/variant
  NAMESPACE variant::
)

install(
  FILES
  "${CMAKE_CURRENT_BINARY_DIR}/variantConfig.cmake"
  DESTINATION share/variant
)