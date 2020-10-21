cmake_minimum_required(VERSION 3.13.4)
  
SET(CMAKE_INSTALL_PREFIX ${CMAKE_CURRENT_SOURCE_DIR})
#will need to update this path to directory of CMakePublic on local computer
SET(CMAKE_PREFIX_PATH /Users/ally/CMaizeExamples/CMaizePublicDepend/${CMAKE_INSTALL_LIBDIR})

project(CMaizePublicDepend2 VERSION 1.0.0 LANGUAGES CXX)

include("${PROJECT_SOURCE_DIR}/cmake/get_cpp.cmake")
include(GNUInstallDirs)

#this function is a work in progress and so the call to cpp_add library below fails
#to find the header file cmake_public_depend.hpp
cpp_find_or_build_dependency(
    CMaizePublicDepend
    #used for testing & dev
    URL github.com/ally3999/CMaizePublicDepend
    #used once PR accepted
    #URL github.com/CMaizeExamples/CMaizePublicDepend
    BUILD_TARGET CMaizePublicDepend
    FIND_TARGET CMakePublic::CMaizePublicDepend
)

cpp_add_library(
    ${PROJECT_NAME}
    SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}"
    INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}"
    DEPENDS CMaizePublicDepend
)

target_include_directories (${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

install(TARGETS ${PROJECT_NAME}
    EXPORT ${PROJECT_NAME}-targets
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_INCLUDEDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_BINDIR}
)

install(EXPORT ${PROJECT_NAME}-targets
    NAMESPACE ${PROJECT_NAME}::
    FILE ${PROJECT_NAME}Config.cmake
    DESTINATION ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}
)

message("CMAKEPUBLICDEPEND2................................................................")
