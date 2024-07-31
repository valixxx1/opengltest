cmake_minimum_required(VERSION 3.30.0)
project(MyProgram)

add_subdirectory(glfw)
add_subdirectory(glad)

add_executable(my_program src/main.cpp)

target_link_libraries(my_program PRIVATE glfw)
target_link_libraries(my_program PRIVATE glad)

target_include_directories(my_program PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/glfw/include/GLFW)

set(SHADER_SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(SHADER_BUILD_DIR "${CMAKE_CURRENT_BINARY_DIR}/shaders")

file(MAKE_DIRECTORY ${SHADER_BUILD_DIR})
file(COPY ${SHADER_SRC_DIR}/vertex.glsl DESTINATION ${SHADER_BUILD_DIR})
file(COPY ${SHADER_SRC_DIR}/fragment.glsl DESTINATION ${SHADER_BUILD_DIR})

target_compile_definitions(my_program PRIVATE SHADER_DIR="${SHADER_BUILD_DIR}")