cmake_minimum_required(VERSION 3.16)

project (teban)

# Set to C++11
set ( CMAKE_CXX_STANDARD          11 )
set ( CMAKE_CXX_STANDARD_REQUIRED ON )
set ( CMAKE_CXX_EXTENSIONS        OFF )

# Executables
add_executable(main_code
    src/main.cpp
    src/libraries/lib/glad.c
    src/tools/CAMERA.h
    src/tools/SHADER.h
    src/tools/TEXTURES.h
    src/textures/wall.jpg
    src/shaders/main.fs
    src/shaders/main.vs
    src/shaders/light.vs
    src/shaders/light.fs
)

set_target_properties(main_code PROPERTIES
    VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}"
)

file(COPY ${CMAKE_SOURCE_DIR}/src/shaders
     DESTINATION ${CMAKE_BINARY_DIR}/src
)

file(COPY ${CMAKE_SOURCE_DIR}/src/textures
     DESTINATION ${CMAKE_BINARY_DIR}/src
)

target_include_directories(main_code PRIVATE
    src
    src/libraries/includes
    src/libraries/lib
    src/shaders
    src/textures
    src/tools
)

target_link_libraries(main_code PRIVATE
    ${CMAKE_SOURCE_DIR}/src/libraries/lib/libglfw3.a
    gdi32
    opengl32
)




