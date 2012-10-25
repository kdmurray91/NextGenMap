cmake_minimum_required(VERSION 2.8)
project(NextGenMap)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/modules/")

#add_definitions(-D INSTANCE_COUNTING) 
#add_definitions(-D VERBOSE)
#add_definitions(-D _DEBUGCS)

SET (CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -g ")
SET (CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g3 -O0 -Wall")

#include(FindOpenMP)
FIND_PACKAGE(OpenMP REQUIRED)
if(OPENMP_FOUND)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()

FIND_PACKAGE(OpenCL REQUIRED)
FIND_PACKAGE(ZLIB REQUIRED)
FIND_PACKAGE(Bamtools QUIET COMPONENTS)

#ADD_DEFINITIONS(-g -O3)

#SET (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,-rpath,'$ORIGIN'" )
#SET (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,-rpath,'$ORIGIN/mason:$ORIGIN/amd-app/lib/x86_64'" )
#SET (CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -Wl,-rpath,'$ORIGIN/mason:$ORIGIN/amd-app/lib/x86_64'" )


set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin/)

include_directories(${OPENCL_INCLUDE_DIRS})

add_subdirectory(lib/mason/opencl)
add_subdirectory(src)