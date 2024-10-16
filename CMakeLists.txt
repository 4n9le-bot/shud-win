cmake_minimum_required(VERSION 3.12)
project(shud VERSION 0.1.0 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -static")

set(SRC_DIR ${CMAKE_SOURCE_DIR}/src)


include_directories(${SRC_DIR}/Model)
include_directories(${SRC_DIR}/ModelData)
include_directories(${SRC_DIR}/classes)
include_directories(${SRC_DIR}/Equations)

# Source Files
file(GLOB_RECURSE SRC_FILES
    "${SRC_DIR}/classes/*.cpp"
    "${SRC_DIR}/ModelData/*.cpp"
    "${SRC_DIR}/Model/*.cpp"
    "${SRC_DIR}/Equations/*.cpp"
)

find_package(SUNDIALS REQUIRED)

add_executable(shud_cmake ${SRC_DIR}/main.cpp ${SRC_FILES})

target_link_libraries(shud_cmake PUBLIC SUNDIALS::cvode)

include(CTest)
enable_testing()

