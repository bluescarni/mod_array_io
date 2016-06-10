cmake_minimum_required(VERSION 3.2 FATAL_ERROR)

enable_testing()

project(array_io VERSION 0.1 LANGUAGES CXX)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/mod_cmake")
include(ModularDeps)

add_dependency("array" "https://github.com/bluescarni/mod_array.git")

add_library(array_io src/array_io.cpp)
target_link_libraries(array_io array)

target_include_directories(array_io PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
  PRIVATE src)

install(TARGETS array_io
  ARCHIVE  DESTINATION lib
  LIBRARY  DESTINATION lib
  RUNTIME  DESTINATION bin)
install(DIRECTORY include/ DESTINATION include)

add_executable(array_io_test0 tests/array_io_test0.cpp)

target_link_libraries(array_io_test0 array_io)

add_test(array_io_test0 array_io_test0)
