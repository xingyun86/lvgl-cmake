# CMakeList.txt : Top-level CMake project file, do global configuration
# and include sub-projects here.
#
cmake_minimum_required (VERSION 3.8)

project ("lvgldemo")

# Include sub-projects.
add_subdirectory ("vendor/SDL2")
add_subdirectory ("lvgldemo")
