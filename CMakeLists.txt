# CMake最低版本要求
cmake_minimum_required(VERSION 3.1.0)

# 指定编译工具链
set(CMAKE_TOOLCHAIN_FILE "linux-toolchain.cmake")

# 项目类型: 
# EXE: 可执行文件
# STATIC_LIB: 静态库
# SHARED_LIB: 动态库
set(PROJECT_TYPE "EXE")

# 设置项目名称
set(PROJECT_NAME cmk_demo)

# 项目名称
project(${PROJECT_NAME})

# 添加子目录(子目录中有CMakeLists.txt文件)
add_subdirectory(base)

# 头文件路径
include_directories(${PROJECT_SOURCE_DIR})
include_directories(${PROJECT_SOURCE_DIR}/base)

# 库文件路径
#link_directories()

# 源文件
file(GLOB_RECURSE SOURCES
    calc.cpp
    base.cpp
)

if(${PROJECT_TYPE} STREQUAL "EXE")
# 指定编译成可执行文件
add_executable(${PROJECT_NAME} main.cpp ${SOURCES})
# 链接所使用到的库
# target_link_libraries(${PROJECT_NAME} pthread)
elseif(${PROJECT_TYPE} STREQUAL "SHARED_LIB")
add_library(${PROJECT_NAME} SHARED ${SOURCES})
# 链接所使用到的库
target_link_libraries(${PROJECT_NAME} base)
else()
add_library(${PROJECT_NAME} STATIC ${SOURCES})
# 链接所使用到的库
# target_link_libraries(${PROJECT_NAME} pthread)
endif()












