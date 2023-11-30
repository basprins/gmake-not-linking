cmake_minimum_required(VERSION 3.1...3.22)

project(unit-tests)

# NOTE: define the dedicated directives BEFORE including the generic CMakeLists, they will be appended!!

set(PROJECT_ROOT            ${CMAKE_SOURCE_DIR}/..)
set(SOURCE                  ${CMAKE_SOURCE_DIR})

set(COMPILER_DIRECTIVES     "$-O0 -g3 -Wall")
set(CMAKE_C_FLAGS           "${COMPILER_DIRECTIVES}")
set(CMAKE_CXX_FLAGS         "${COMPILER_DIRECTIVES}")

# Overrides
set(CMAKE_EXPORT_COMPILE_COMMANDS   ON)
set(CMAKE_VERBOSE_MAKEFILE          ON)

# Project headers
set(project_headers
    ${SOURCE}
)

include_directories(
    ${project_headers}
)

# Source files

file(GLOB_RECURSE unit_test_sources CONFIGURE_DEPENDS
    ${SOURCE}/*.c
    ${SOURCE}/*.cpp
    ${SOURCE}/**/*.c
    ${SOURCE}/**/*.cpp
)

add_executable(${PROJECT_NAME} ${unit_test_sources})
target_link_libraries(${PROJECT_NAME} pthread)
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_20)