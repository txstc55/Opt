################################################################################
cmake_minimum_required(VERSION 3.10)
project(ARAP_MESH_DEFORMATION)
################################################################################

## check if we need to use 64 bit release
if (UNIX)
	set(s4 "64")
endif(UNIX)



## include the source directory
include_directories("${CMAKE_SOURCE_DIR}/src")

## get the source files
file(GLOB SOURCES
"${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp"
# "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cu"
)
list(REMOVE_ITEM SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/src/CUDAWarpingSolver.cpp")
message(${SOURCES})

## include the shared directory
include_directories("${CMAKE_SOURCE_DIR}/../shared")

## release stuffs
include_directories(${CMAKE_SOURCE_DIR}/../../API/release/include)
link_directories(${CMAKE_SOURCE_DIR}/../../API/release/lib)

include_directories(${CMAKE_SOURCE_DIR}/../external/mLib/include)
include_directories(${CMAKE_SOURCE_DIR}/../external)

## link the openmesh library
include_directories(${CMAKE_SOURCE_DIR}/../external/OpenMesh/include)
include_directories(${CMAKE_SOURCE_DIR}/../external/OpenMesh/lib/linux)
link_directories(${CMAKE_SOURCE_DIR}/../external/OpenMesh/lib/linux)


## set various homes
set(CUDEHOME /usr/local/cuda-10.2)
set(TERRAHOME ${CMAKE_SOURCE_DIR}/../../../terra)


## include cuda and terra
include_directories(${CUDAHOME}/include)
link_directories(${CUDAHOME}/lib${S4})
include_directories(${TERRAHOME}/include)
link_directories(${TERRAHOME}/lib)

## find ceres
find_package(Ceres REQUIRED)
include_directories(${CERES_INCLUDE_DIRS})


SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -pthread")


add_compile_options(-Wl,-rpath,$(CUDAHOME)/lib$(S4) -pthread)

## add compile options
add_compile_options(-O3 -g -std=c++11 -ldl -lz -lgflags -lglog -lm -llua)


## build the project binary
add_executable(${PROJECT_NAME}_bin ${SOURCES})

## link openmesh
target_link_libraries(${PROJECT_NAME}_bin OpenMeshCore OpenMeshTools cudart terra OptDev ${CERES_LIBRARIES})