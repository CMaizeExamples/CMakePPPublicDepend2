cmake_minimum_required(VERSION 3.13.4)
project(CMaize_Public_Depend2)

include("${PROJECT_SOURCE_DIR}/cmake/get_cpp.cmake")

cpp_find_or_build_dependency(
    CMaizePublicDepend
    URL github.com/ally3999/CMaizePublicDepend
    BUILD_TARGET CMaizePublicDepend
    FIND_TARGET CMaizePublicDepend::CMaizePublicDepend
)

cpp_add_library(
    CMaizePublicDepend2
    SOURCE_DIR "${CMAKE_CURRENT_LIST_DIR}"
    INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}"
    DEPENDS CMakePublic CMaizePublicDepend
)

message("Processing public depend2...")
