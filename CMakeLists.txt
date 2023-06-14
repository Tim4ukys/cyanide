cmake_minimum_required(VERSION 3.19)

project(cyanide VERSION 0.1.0
                DESCRIPTION "Useful utilities and wrappers"
                LANGUAGES CXX)

include(CMakeDependentOption)

option(CYANIDE_FEATURE_ALL "Enable all the library features" ON)

cmake_dependent_option(
    CYANIDE_FEATURE_HOOK
    "Enable hooks support" ON
    "CYANIDE_FEATURE_ALL" OFF
)

if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
    set(CYANIDE_MASTER_PROJECT ON)
endif()

add_subdirectory(src)
