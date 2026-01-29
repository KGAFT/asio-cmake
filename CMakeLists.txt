cmake_minimum_required(VERSION 3.10)

project(asio-sdk)

file(GLOB_RECURSE SRC_FILES asio/common/*.cpp)
file(GLOB_RECURSE PLT_FILES asio/host/*.cpp)


set(FILE_TO_REMOVE "${CMAKE_CURRENT_SOURCE_DIR}/asio/common/asiodrvr.cpp")
list(REMOVE_ITEM SRC_FILES ${FILE_TO_REMOVE})
set(FILE_TO_REMOVE "${CMAKE_CURRENT_SOURCE_DIR}/asio/common/asiodrvr.h")
list(REMOVE_ITEM SRC_FILES ${FILE_TO_REMOVE})
set(FILE_TO_REMOVE "${CMAKE_CURRENT_SOURCE_DIR}/asio/common/dllentry.cpp")
list(REMOVE_ITEM SRC_FILES ${FILE_TO_REMOVE})
set(FILE_TO_REMOVE "${CMAKE_CURRENT_SOURCE_DIR}/asio/host/sample/hostsample.cpp")
list(REMOVE_ITEM PLT_FILES ${FILE_TO_REMOVE})

add_library(asio-sdk STATIC ${SRC_FILES} ${PLT_FILES})
target_compile_definitions(asio-sdk PRIVATE __ASIODRIVER_FWD_DEFINED__)
target_include_directories(asio-sdk PUBLIC asio/common asio/host asio/host/pc)

add_library(asio-link STATIC asio-link/helpers.hpp asio-link/helpers.cpp)
target_link_libraries(asio-link PUBLIC asio-sdk)
