cmake_minimum_required(VERSION 3.10)
project(GameSDL2)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# SDL2 路径配置
set(SDL2_DIR "D:/SDL2/SDL2-2.30.6")
set(SDL2_INCLUDE_DIR "${SDL2_DIR}/include")
set(SDL2_LIB_DIR "${SDL2_DIR}/lib/x64")

# 包含 SDL2 头文件
include_directories(${SDL2_INCLUDE_DIR})

# 添加可执行文件
add_executable(${PROJECT_NAME} src/main.cpp)

# 链接 SDL2 库
target_link_directories(${PROJECT_NAME} PRIVATE ${SDL2_LIB_DIR})
target_link_libraries(${PROJECT_NAME} PRIVATE SDL2main SDL2)

# 复制 SDL2.dll 到输出目录
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    "${SDL2_LIB_DIR}/SDL2.dll"
    $<TARGET_FILE_DIR:${PROJECT_NAME}>)

