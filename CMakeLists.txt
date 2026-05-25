cmake_minimum_required(VERSION 3.16)

project(heheap)

# OpenGL
#-------------------------------
find_package(OpenGL REQUIRED)
#-------------------------------


# GLFW
#-------------------------------
add_subdirectory(lib/glfw)
#-------------------------------

# IMGUI
#-------------------------------
set(IMGUI_SRC
	lib/imgui/imgui.cpp
	lib/imgui/imgui_demo.cpp
	lib/imgui/imgui_draw.cpp
	lib/imgui/imgui_tables.cpp
	lib/imgui/imgui_widgets.cpp
)

set(IMGUI_HDRS
	lib/imgui/imgui.h
	lib/imgui/imgui_internal.h
	lib/imgui/imstb_rectpack.h
	lib/imgui/imstb_textedit.h
	lib/imgui/imstb_truetype.h
)

set(IMGUI_BACKEND_SRC
	lib/imgui/backends/imgui_impl_opengl3.cpp
	lib/imgui/backends/imgui_impl_glfw.cpp
)

set(IMGUI_BACKEND_HDRS
	lib/imgui/backends/imgui_impl_opengl3.h
	lib/imgui/backends/imgui_impl_opengl3_loader.h
	lib/imgui/backends/imgui_impl_glfw.h
)

add_library(imgui STATIC
		  ${IMGUI_SRC}
		  ${IMGUI_HDRS}
		  ${IMGUI_BACKEND_SRC}
		  ${IMGUI_BACKEND_HDRS}
)
target_include_directories(imgui PRIVATE lib/imgui)
target_include_directories(imgui PRIVATE lib/imgui/backends)
target_include_directories(imgui PRIVATE lib/glfw/include)
#-------------------------------

#-------------------------------
set(HEHEAP_SRC src/main.cpp)

add_executable(heheap ${HEHEAP_SRC})

target_link_libraries(heheap OpenGL::GL)
target_link_libraries(heheap glfw)
target_link_libraries(heheap imgui)
target_include_directories(heheap PRIVATE lib/imgui)
target_include_directories(heheap PRIVATE lib/imgui/backends)
target_include_directories(heheap PRIVATE lib/glfw/include)
#-------------------------------
