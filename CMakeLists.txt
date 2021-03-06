#
# @file CMakeLists.txt
# @author 0dayZh
# @date 2015/03/10
#

cmake_minimum_required(VERSION 2.8.4)
project(demo)

message("CMAKE_SYSTEM_NAME: ${CMAKE_SYSTEM_NAME}")

set(SOURCE_FILES src/demo.c src/flv-parser.c)

include_directories("${PROJECT_SOURCE_DIR}/deps" "${PROJECT_SOURCE_DIR}/deps/pili-camera-sdk/src/include" "${PROJECT_SOURCE_DIR}/src" "/usr/local/include" "/usr/include")

if (${OS_ARCH} MATCHES "darwin_amd64")
link_directories("/usr/local/lib" "/usr/lib" "${PROJECT_SOURCE_DIR}/deps/pili-camera-sdk/src/lib/darwin_amd64")
elseif (${OS_ARCH} MATCHES "linux_amd64")
link_directories("/usr/local/lib" "/usr/lib"
    "${PROJECT_SOURCE_DIR}/deps/pili-camera-sdk/src/lib/linux_amd64")
elseif (${OS_ARCH} MATCHES "linux_386")
link_directories("/usr/local/lib" "/usr/lib" "${PROJECT_SOURCE_DIR}/deps/pili-camera-sdk/src/lib/linux_386")
else()
MESSAGE(FATAL_ERROR "cmake -DOS_ARCH=1 ..")
endif()

add_executable(demo ${SOURCE_FILES})

target_link_libraries(demo "libpili_push.a" "libssl.a"
    "libcrypto.a" "libz.a" "pthread" ${CMAKE_DL_LIBS})
