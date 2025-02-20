cmake_minimum_required(VERSION 3.16)
project(imgui)

set(CMAKE_CXX_STANDARD 17)

find_package(PkgConfig REQUIRED)
find_package(Freetype REQUIRED)
pkg_search_module(GLFW REQUIRED glfw3)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")

add_library(imgui STATIC
        source/imgui.cpp
        source/imgui_demo.cpp
        source/imgui_draw.cpp
        source/imgui_freetype.cpp
        source/imgui_impl_glfw.cpp
        source/imgui_impl_opengl3.cpp
        source/imgui_tables.cpp
        source/imgui_widgets.cpp

        source/TextEditor.cpp

        source/imgui_imhex_extensions.cpp

        source/imnodes.cpp

        source/implot.cpp
        source/implot_items.cpp
        source/implot_demo.cpp

        fonts/fontawesome_font.c
        fonts/codicons_font.c
        fonts/unifont_font.c
)

add_compile_definitions(IMGUI_IMPL_OPENGL_LOADER_GLAD)

target_include_directories(imgui PUBLIC include fonts ${FREETYPE_INCLUDE_DIRS} ${GLFW_INCLUDE_DIRS})

target_link_directories(imgui PUBLIC ${GLFW_LIBRARY_DIRS})

if (WIN32)
    target_link_libraries(imgui Freetype::Freetype glfw3 opengl32.lib)
elseif (UNIX)
    target_link_libraries(imgui Freetype::Freetype glfw GL)
endif()
