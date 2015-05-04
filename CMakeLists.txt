cmake_minimum_required (VERSION 2.6)
set(PROJECT_NAME "empty_blendish")
 
project(${PROJECT_NAME} C CXX)

#set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/cmake/") #NOTE: useful to have, here so i won't forget


#TODO: remake into find_package format
SET(BLENDISH "../blendish/" CACHE PATH "Path to blendish")
SET(NANOVG "../nanovg/" CACHE PATH "Path to nanovg")
SET(GL3W "libs/gl3w" CACHE PATH "Path to gl3w")
SET(GLFW "../glfw-3.1.1/install" CACHE PATH "Path to glfw")

find_package(OpenGL REQUIRED)


SET(GLFW_LIBS
    optimized glfw3.lib
    debug glfw3d.lib
    )

SET(SRCS
    ${GL3W}/GL/gl3w.c
    ${NANOVG}/src/nanovg.c
    
    src/main.cpp
)
SET(HDRS
    ${GL3W}/GL/gl3w.h
    ${GL3W}/GL/glcorearb.h

    ${BLENDISH}/blendish.h
    ${BLENDISH}/oui.h

    ${NANOVG}/src/stb_truetype.h
    ${NANOVG}/src/stb_image.h
    ${NANOVG}/src/nanovg.h
    ${NANOVG}/src/nanovg_gl.h
    ${NANOVG}/src/nanovg_gl_utils.h
    ${NANOVG}/src/fontstash.h
    
)

INCLUDE_DIRECTORIES(src)
INCLUDE_DIRECTORIES(${GL3W})
INCLUDE_DIRECTORIES(${GLFW}/include)
INCLUDE_DIRECTORIES(${NANOVG}/src)
INCLUDE_DIRECTORIES(${BLENDISH})

link_directories(${GLFW}/lib)
ADD_EXECUTABLE(${PROJECT_NAME} ${SRCS} ${HDRS})
TARGET_LINK_LIBRARIES(${PROJECT_NAME} ${GLFW_LIBS} ${OPENGL_gl_LIBRARY} ${OPENGL_glu_LIBRARY})


