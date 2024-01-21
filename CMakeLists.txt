cmake_minimum_required(VERSION 3.13)
set(CMAKE_CXX_STANDARD 23)
set(project_name pico-template-vscode)
set(CMAKE_VERBOSE_MAKEFILE ON)
include(lib/pico-sdk/pico_sdk_init.cmake)
project(${project_name} C CXX ASM)
pico_sdk_init()

execute_process(COMMAND git describe --tags --always OUTPUT_STRIP_TRAILING_WHITESPACE
        OUTPUT_VARIABLE GIT_REPO_VERSION)
configure_file("src/project_version.h.in" "project_version.h")

add_executable(
        ${project_name}
        src/main.cpp
)

target_include_directories (${project_name} PRIVATE ${CMAKE_BINARY_DIR})

target_link_libraries(${project_name}
        pico_stdlib
)

pico_enable_stdio_uart(${project_name} 1)
pico_add_extra_outputs(${project_name})