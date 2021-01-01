cmake_minimum_required(VERSION 3.16.0)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

project(reb)

add_executable(
    ${PROJECT_NAME}
    reb.c
)