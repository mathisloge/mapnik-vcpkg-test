cmake_minimum_required(VERSION 3.20)
set(CMAKE_TOOLCHAIN_FILE "D:/dev/vcpkg_mapnik/scripts/buildsystems/vcpkg.cmake" CACHE FILEPATH "vcpkg toolchain")
project(mapnik-demo)

find_package(mapnik CONFIG REQUIRED)

set(MAPNIK_FONTS_DIR ${MAPNIK_FONTS_DIR})
configure_file(config.hpp.in vcpkg_config.h @ONLY)

add_executable(mapnik-demo rundemo.cpp)

target_link_libraries(mapnik-demo PRIVATE mapnik::mapnik mapnik::json mapnik::wkt ICU::data ICU::i18n ICU::uc)
target_include_directories(mapnik-demo PRIVATE ${CMAKE_CURRENT_BINARY_DIR})

file(COPY data DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/demo")
