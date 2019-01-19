cmake_minimum_required(VERSION 3.12)
project(glfw_sample)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

find_package(glfw3 3.2 REQUIRED)
find_package(OpenGL REQUIRED)

include_directories(glfw_sample ${OPENGL_INCLUDE_DIR} include)

add_executable(glfw_sample glad.c main.cpp)

target_link_libraries(glfw_sample glfw ${OPENGL_gl_LIBRARY} ${OPENGL_glu_LIBRARY})

if (UNIX)
    # Need to link libdl on Linux:
    # - https://github.com/Dav1dde/glad/issues/78#issuecomment-277487098
    # - https://cmake.org/cmake/help/v3.0/variable/CMAKE_DL_LIBS.html
    target_link_libraries(glfw_sample ${CMAKE_DL_LIBS})
endif()