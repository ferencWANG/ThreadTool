
cmake_minimum_required(VERSION 3.0.0)

project(thread_tool_test)

message(STATUS "Project: SERVER")          #打印相关消息消息
message(STATUS "Project Directory: ${PROJECT_SOURCE_DIR}")

# Specifies a path to native header files.
include_directories(${PROJECT_SOURCE_DIR})
include_directories(${PROJECT_SOURCE_DIR}/../src/)
include_directories(${PROJECT_SOURCE_DIR}/gtest-1.10.0/googletest/include/)

#supports c++11
include(CheckCXXCompilerFlag)  
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)  
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)  
if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")  
    message(STATUS "The compiler ${CMAKE_CXX_COMPILER} and flag -std=c++11")  
elseif(COMPILER_SUPPORTS_CXX0X)  
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")  
    message(STATUS "The compiler ${CMAKE_CXX_COMPILER} and flag -std=c++0x")  
else()  
    message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support.Please use a different C++ compiler.")  
endif() 

add_subdirectory(${PROJECT_SOURCE_DIR}/../ ${PROJECT_SOURCE_DIR}/build )
add_subdirectory(${PROJECT_SOURCE_DIR}/gtest-1.10.0)

file(GLOB native_srcs "*.*")

set(3RD_LIBS gtest pthread)

message(STATUS "native_srcs: ${native_srcs}")

#config source group
source_group(test FILES ${native_srcs} )

add_executable(thread_tool_test ${native_srcs} )

target_link_libraries(thread_tool_test thread_tool ${3RD_LIBS})
