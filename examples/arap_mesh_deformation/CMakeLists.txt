################################################################################
cmake_minimum_required(VERSION 3.1)
project(ARAP_MESH_DEFORMATION)
################################################################################


## include the source directory
include_directories("${CMAKE_SOURCE_DIR}/src")



## include the shared directory
include_directories("${CMAKE_SOURCE_DIR}/../shared")

file(GLOB SOURCES
"${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp"
)

add_executable(${PROJECT_NAME}_bin ${SOURCES})