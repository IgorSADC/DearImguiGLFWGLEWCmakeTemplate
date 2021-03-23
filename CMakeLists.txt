# Projects Settings
cmake_minimum_required (VERSION 3.1)
project (opengl-skeleton)


# The main executable
add_executable(main
src/imguiexample_opengl.cpp
# .
)

set(imgui_DIR ${CMAKE_CURRENT_SOURCE_DIR}/lib/imgui)
set(imgui_backends_DIR ${CMAKE_CURRENT_SOURCE_DIR}/lib/imgui/backends)

set(imgui_SOURCES
  ${imgui_DIR}/imgui_draw.cpp
  ${imgui_DIR}/imgui.cpp
  ${imgui_backends_DIR}/imgui_impl_glfw.cpp
  ${imgui_backends_DIR}/imgui_impl_opengl3.cpp
  ${imgui_DIR}/imgui_demo.cpp
  ${imgui_DIR}/imgui_widgets
  ${imgui_DIR}/imgui_tables.cpp
  )
set(imgui_HEADERS
  ${imgui_DIR}/imconfig.h
  ${imgui_DIR}/imgui.h
  ${imgui_backends_DIR}/imgui_impl_glfw.h
  ${imgui_backends_DIR}/imgui_impl_opengl3.h
  ${imgui_DIR}/imstb_rectpack.h
  ${imgui_DIR}/imstb_truetype.h
  ${imgui_DIR}/imgui_internal.h
  ${imgui_DIR}/imstb_textedit.h
  )

# glfw
add_subdirectory(lib/glfw EXCLUDE_FROM_ALL)
#target_link_libraries(main PUBLIC glfw)

# glew
add_definitions(-DGLEW_STATIC)
add_subdirectory(lib/glew EXCLUDE_FROM_ALL)
#target_link_libraries(main PUBLIC libglew_static)

# glm
add_subdirectory(lib/glm EXCLUDE_FROM_ALL)
target_link_libraries(main PRIVATE glm)

#imgui
add_library(imgui STATIC ${imgui_SOURCES} ${imgui_HEADERS})
target_link_libraries(imgui PUBLIC glfw)
target_link_libraries(imgui PUBLIC libglew_static)
target_include_directories(imgui PUBLIC ${imgui_DIR} ${imgui_backends_DIR}) #${GLFW_SOURCE_DIR}/deps)

find_package(OpenGL REQUIRED)
#target_include_directories(imgui PUBLIC ${OPENGL_INCLUDE_DIRS}  ${GLUT_INCLUDE_DIRS} )
#target_link_libraries(imgui PUBLIC opengl32)


# target_include_directories(imgui PUBLIC
#   $<BUILD_INTERFACE:${imgui_DIR}>
#   $<BUILD_INTERFACE:${imgui_backends_DIR}>)
  #$<BUILD_INTERFACE:${GLFW_SOURCE_DIR}/deps>
 # $<BUILD_INTERFACE:${imgui_backends_DIR}>)
#target_link_libraries(imgui glfw)

target_link_libraries(main PRIVATE imgui)
