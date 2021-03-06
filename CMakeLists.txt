CMAKE_MINIMUM_REQUIRED ( VERSION 2.8 )
include(${CMAKE_ROOT}/Modules/ExternalProject.cmake)

PROJECT ( qc )
SET ( SRC_FILES 
    red_tri.cpp
    ogl/common/shader.cpp

    )
SET ( PROJECT_VERSION_MAJOR 0 )
SET ( PROJECT_VERSION_MINOR 1 )

SET ( CMAKE_BUILD_TYPE Release )
SET ( CMAKE_VERBOSE_MAKEFILE true )

SET ( OUTPUT_ELF
    "${CMAKE_PROJECT_NAME}-${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.out"
    ) 

SET ( CMAKE_C_FLAGS_RELEASE "-static" )

find_package(PkgConfig)
pkg_check_modules(X11 x11)
pkg_check_modules(XINERAMA xinerama)
pkg_check_modules(XF86 xxf86vm)
pkg_check_modules(XRANDR xrandr)
pkg_check_modules(XCURSOR xcursor)
pkg_check_modules(OPENGL gl)
INCLUDE_DIRECTORIES ( 
    ${CMAKE_SOURCE_DIR}/glad/include
    ${CMAKE_SOURCE_DIR}/ogl
    )

ADD_EXECUTABLE( ${OUTPUT_ELF} ${SRC_FILES} ) 
TARGET_LINK_LIBRARIES(${OUTPUT_ELF}
    pthread
    GLEW
    glfw
    ${CMAKE_SOURCE_DIR}/glad/libglad.a
    dl
    ${X11_LIBRARIES}
    ${XF86_LIBRARIES}
    ${OPENGL_LIBRARIES}
    ${XRANDR_LIBRARIES}
    ${XCURSOR_LIBRARIES}
    ${XINERAMA_LIBRARIES} 
    )
