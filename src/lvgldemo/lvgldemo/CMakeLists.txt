# CMakeList.txt : CMake project for lvgldemo, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

set(project_name "lvgldemo")
project(${project_name})
include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}
	${CMAKE_SOURCE_DIR}/vendor
	${CMAKE_SOURCE_DIR}/vendor/lvgl
	${CMAKE_SOURCE_DIR}/vendor/lv_config
	${CMAKE_SOURCE_DIR}/vendor/SDL2/include
)
link_directories(
	${CMAKE_CURRENT_BINARY_DIR}
	${CMAKE_BINARY_DIR}/vendor/SDL2
)
# Add source to this project's executable.
file(GLOB LVGL_SRCS 
"${CMAKE_SOURCE_DIR}/vendor/lvgl/src/*.c" "${CMAKE_SOURCE_DIR}/vendor/lvgl/src/*.cpp"
"${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_core/*.c" "${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_core/*.cpp"
"${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_draw/*.c" "${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_draw/*.cpp"
"${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_font/*.c" "${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_font/*.cpp"
"${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_gpu/*.c" "${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_gpu/*.cpp"
"${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_hal/*.c" "${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_hal/*.cpp"
"${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_misc/*.c" "${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_misc/*.cpp"
"${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_themes/*.c" "${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_themes/*.cpp"
"${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_widgets/*.c" "${CMAKE_SOURCE_DIR}/vendor/lvgl/src/lv_widgets/*.cpp"
)
message(STATUS "[LVGL_SRCS]=${LVGL_SRCS}")
file(GLOB DRIV_SRCS 
"${CMAKE_SOURCE_DIR}/vendor/lv_drivers/display/monitor.c"
"${CMAKE_SOURCE_DIR}/vendor/lv_drivers/indev/keyboard.c"
"${CMAKE_SOURCE_DIR}/vendor/lv_drivers/indev/mouse.c"
"${CMAKE_SOURCE_DIR}/vendor/lv_drivers/indev/mousewheel.c"
)
message(STATUS "[DRIV_SRCS]=${DRIV_SRCS}")
file(GLOB SRCS "*.c" "*.cpp")
file(GLOB DEMO_SRCS "${CMAKE_SOURCE_DIR}/vendor/lv_examples/src/lv_demo_widgets/*.c")
add_executable (${project_name} ${SRCS} ${LVGL_SRCS} ${DRIV_SRCS} ${DEMO_SRCS})
target_compile_definitions(${project_name} 
PRIVATE -DLV_USE_DEMO_WIDGETS=1
PRIVATE -DUSE_MONITOR=1
PRIVATE -DUSE_MOUSE=1
PRIVATE -DMONITOR_SDL_INCLUDE_PATH=<SDL.h>
)
target_link_libraries(${project_name} 
PRIVATE SDL2main
PRIVATE SDL2_static
)
# TODO: Add tests and install targets if needed.
