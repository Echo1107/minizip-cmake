cmake_minimum_required(VERSION 3.16)

# project name
project(minizip-exe C CXX)

file(GLOB_RECURSE src
        ${CMAKE_CURRENT_LIST_DIR}/*.h
        ${CMAKE_CURRENT_LIST_DIR}/*.hpp
        ${CMAKE_CURRENT_LIST_DIR}/*.cpp)

add_executable(minizip-exe ${src})

target_link_libraries(minizip-exe
        PUBLIC minizip)