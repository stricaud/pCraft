cmake_minimum_required(VERSION 3.2)

project(ami-project)

SET(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${ami-project_SOURCE_DIR}/cmake)

if(${CMAKE_CURRENT_SOURCE_DIR} STREQUAL ${CMAKE_CURRENT_BINARY_DIR})
message(FATAL_ERROR "CMake generation is not allowed within the source directory!
Remove the CMakeCache.txt file and try again from another folder, e.g.:

   rm CMakeCache.txt
   mkdir build
   cd build
   cmake ..
")
endif()

include(GNUInstallDirs)
enable_testing()

if (APPLE)
      set(CMAKE_MACOSX_RPATH ON)
      set(CMAKE_INSTALL_RPATH "@loader_path/../lib")
      message(STATUS "Dynamic Linking done with rpath")
endif()

find_package(BISON REQUIRED)
find_package(FLEX REQUIRED)
find_package(libcsv REQUIRED)
find_package(Python COMPONENTS Interpreter Development)
find_package(pybind11 REQUIRED)
find_package(LibUUID REQUIRED)

message("Flex found:" ${FLEX_FOUND})
message("Flex executable:" ${FLEX_EXECUTABLE})

set(AMI_INCLUDE_DIRS "${ami-project_SOURCE_DIR}/lib/include/" "${ami-project_BINARY_DIR}/lib/include")

set(AMI_LIBRARY ami)
if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
	set(AMI_LIBRARY "${ami-project_BINARY_DIR}/lib/libami.dylib")
endif()
if(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
	set(AMI_LIBRARY "${ami-project_BINARY_DIR}/lib/libami.so")
endif()

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O0 -ggdb")

add_subdirectory(lib)
add_subdirectory(bin)
add_subdirectory(python)
add_subdirectory(tests)
