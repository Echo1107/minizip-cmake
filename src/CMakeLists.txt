cmake_minimum_required(VERSION 3.16)

# project name
project(minizip-lib C CXX)


# detect operating system
message(STATUS "We are on a ${CMAKE_SYSTEM_NAME} system")
if(${CMAKE_SYSTEM_NAME} STREQUAL "Linux")
    add_definitions(-DSYSTEM_LINUX)
endif()
if(${CMAKE_SYSTEM_NAME} STREQUAL "Darwin")
    add_definitions(-DSYSTEM_DARWIN)
endif()
if(${CMAKE_SYSTEM_NAME} STREQUAL "AIX")
    add_definitions(-DSYSTEM_AIX)
endif()
if(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
    add_definitions(-DSYSTEM_WINDOWS)
endif()

set(src impl/ioapi.c impl/miniunz.c impl/mztools.c impl/unzip.c impl/zip.c)

if(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
    set(src impl/iowin32.c impl/ioapi.c impl/miniunz.c impl/mztools.c impl/unzip.c impl/zip.c)
endif()

add_library(minizip STATIC ${src})

target_include_directories(minizip
    PUBLIC "${CMAKE_CURRENT_LIST_DIR}/include/"
    PUBLIC "${zlib_SOURCE_DIR}"
    PUBLIC "${zlib_BINARY_DIR}"
)

target_link_libraries(minizip
    PUBLIC zlibstatic
)
